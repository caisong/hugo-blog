---
title: Golang sftp
date: 2024-12-24T21:40:53+08:00
lastmod: 2024-12-24T21:40:53+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

golang 连接 sftp
```go
package main

import (
	"fmt"
	"log"
	"os"

	"golang.org/x/crypto/ssh"
	"github.com/pkg/sftp"
)

func main() {
	// 配置 SSH 客户端
	sshConfig := &ssh.ClientConfig{
		User: "your-username", // 目标服务器的用户名
		Auth: []ssh.AuthMethod{
			// 使用私钥认证
			ssh.PublicKeysCallback(func() ([]ssh.PublicKey, error) {
				// 加载私钥文件
				privateKeyPath := "/path/to/your/private/key"
				key, err := os.ReadFile(privateKeyPath)
				if err != nil {
					return nil, fmt.Errorf("unable to read private key: %v", err)
				}

				// 解密私钥文件（如果私钥有密码保护）
				signer, err := ssh.ParsePrivateKey(key)
				if err != nil {
					return nil, fmt.Errorf("unable to parse private key: %v", err)
				}

				// 返回公钥认证方法
				return []ssh.PublicKey{signer.PublicKey()}, nil
			}),
		},
		HostKeyCallback: ssh.InsecureIgnoreHostKey(), // 忽略主机密钥验证（适用于开发，生产环境需要提供真实的公钥验证）
	}

	// 连接到远程主机
	sshClient, err := ssh.Dial("tcp", "remote-server.com:22", sshConfig)
	if err != nil {
		log.Fatalf("Failed to dial: %v", err)
	}
	defer sshClient.Close()

	// 创建 SFTP 客户端
	client, err := sftp.NewClient(sshClient)
	if err != nil {
		log.Fatalf("Failed to create SFTP client: %v", err)
	}
	defer client.Close()

	// 进行文件操作，例如列出远程目录
	files, err := client.ReadDir("/path/to/remote/directory")
	if err != nil {
		log.Fatalf("Failed to list directory: %v", err)
	}

	// 打印远程目录中的文件
	for _, file := range files {
		fmt.Println(file.Name())
	}
}

```
