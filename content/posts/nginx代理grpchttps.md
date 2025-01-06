---
title: Nginx同时代理grpc和https
date: 2024-08-28T21:42:16+08:00
lastmod: 2024-08-28T21:42:16+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - golang
  - nginx
tags:
  - grpc
  - nginx
  - https
# nolastmod: true
draft: false
---

nginx 同时代理grpc和https  。基于`grpc`创建了服务端和客户端，使用`echo`创建了https服务器，nginx分别代理`grpc`请求和`https`请求。

<!-- MarkdownTOC -->

* TLS证书
* GRPC
* https
* nginx代理



##  tls证书  
```bash
openssl req -new -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem -subj "/CN=10.1.19.100" -addext "subjectAltName=IP:10.1.19.100"
```
## grpc

### 消息
1. proto文件
```plain
syntax = "proto3";

// 根据自己module name写就行，然后直接拷贝过去
option go_package = "mygrpc/message/helloworld";

// 官方示例里没注释，不过对go应该也没啥作用
//option java_multiple_files = true;
//option java_package = "io.grpc.examples.helloworld";
//option java_outer_classname = "HelloWorldProto";

package helloworld;

// The greeting service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
```
2. 代码生成
```bash
sudo apt install rotoc-gen-go protoc-gen-go-grpc
# 生成
protoc --go_out=. --go-grpc_out=. ./helloworld.proto 
```

### 服务端
```go
package main

import (
	"context"
	"log"
	"net"
    "fmt"
    "flag"

	pb "mygrpc/message/helloworld"
	"google.golang.org/grpc"
    "google.golang.org/grpc/credentials"
    #"google.golang.org/grpc/interceptor"
)

type server struct {
	pb.UnimplementedGreeterServer
}

func (s *server) SayHello(ctx context.Context, req *pb.HelloRequest) (*pb.HelloReply, error) {
	return &pb.HelloReply{Message: "Hello " + req.Name}, nil
}

func main() {
    certFile:="/data/code/grpc/cert.pem"
    keyFile:="/data/code/grpc/key.pem"

    creds, err:=credentials.NewServerTLSFromFile(certFile, keyFile)
    if err!=nil {
        log.Fatalf("Failed to generated credentials: %v", err)
    }

    grpcServer := grpc.NewServer(grpc.Creds(creds))
	// 注册 Greeter 服务
	pb.RegisterGreeterServer(grpcServer, &server{})

    var port int
    flag.IntVar(&port, "port", -1, "listten port")
    flag.Parse()

	// 监听端口
    listener, err := net.Listen("tcp", fmt.Sprintf(":%d", port))

	if err != nil {
		log.Fatalf("Failed to listen on port %d: %v", port, err)
	}

	// 启动 gRPC 服务器
	log.Println("gRPC server is listening on port", port)
	if err := grpcServer.Serve(listener); err != nil {
		log.Fatalf("Failed to serve: %v", err)
	}
}
```

### 客户端
```go
package main 

import (
    "context"
    "log"

	"google.golang.org/grpc"
    "google.golang.org/grpc/credentials"
	pb "grpcclient/message/helloworld"
)

func main() {
    certFile := "/data/code/grpc/cert.pem"

    creds, err:=credentials.NewClientTLSFromFile(certFile,"")
    if err!=nil{
        log.Fatalf("Failed to load credentials %v", err)
    }

    conn, err:=grpc.Dial("10.1.19.100:443", grpc.WithTransportCredentials(creds))
    if err!=nil{
        log.Fatalf("Faield to connect %v", err)
    }

    defer conn.Close()

    client:= pb.NewGreeterClient(conn)
    
    resp, err:= client.SayHello(context.Background(), &pb.HelloRequest{Name:"grpc"})
    if err!=nil {
        log.Fatalf("Faield to say hello %v", err)
    }
    log.Printf("Response %s", resp.Message)
}
```

## https
### 服务端
```go
package main

import (
    "log"
    "net/http"
    "fmt"
    "flag"

    "github.com/labstack/echo/v4"
)

func main(){
    e := echo.New()

    var port int
    flag.IntVar(&port, "port", -1, "listen port")
    flag.Parse()

    e.GET("/h/", func(c echo.Context) error {
        return c.String(http.StatusOK, "Hello, Https World")
    })

    err := e.StartTLS(fmt.Sprintf(":%d", port), "/data/code/grpc/cert.pem", "/data/code/grpc/key.pem")
    if err!=nil {
        log.Fatalf("failed to start server: %v", err)
    }
}
```

## nginx代理
原来想给grpc添加前缀的，但是grpc添加前缀有点麻烦，就给http添加前缀了。
```config
pstream grpc_backend {
    server 10.1.19.100:50051;
    #server grpc_backend2:50051;
}

upstream http_backend {
    server 10.1.19.100:60010;
    # server http_backend2:60011;
}

server {
    listen 443 ssl http2;
    server_name 10.1.19.100;

    ssl_certificate /data/code/grpc/cert.pem;
    ssl_certificate_key /data/code/grpc/key.pem;


# 处理普通 HTTPS 流量
    location /h/ {
        proxy_pass https://http_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
    
    grpc_ssl_verify off;
    # grpc_ssl_session_reuser on;
    # 处理 gRPC 流量
    location / {
        # grpcs 表示grpc + tls
        grpc_pass grpcs://grpc_backend;
        error_page 502 = /error502grpc;
    }
    
    location = /error502grpc {
        internal;
        add_header content-type application/grpc;
        add_header grpc-status 14;
        add_header content-length 0;
        add_header grpc-message "Unreachable";
        add_header x-grpc-error-deailts "service unavailable";
        return 204;
    }

# 自定义错误页面
    location = /error502 {
        internal;
        add_header content-type text/plain;
        return 502 "Bad Gateway";
    }
}
```

