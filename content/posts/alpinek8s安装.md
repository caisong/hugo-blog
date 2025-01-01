---
title: Alpinek8s安装
date: 2022-03-17T21:40:27+08:00
lastmod: 2022-03-17T21:40:27+08:00
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

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# alpine k8s安装
[安装参考](https://dev.to/xphoniex/how-to-create-a-kubernetes-cluster-on-alpine-linux-kcg)
## 配置vagrant
## master节点安装
1. 添加edge软件源
```shell
https://mirrors.ustc.edu.cn/alpine/latest-stable/main
https://mirrors.ustc.edu.cn/alpine/latest-stable/community
@testing http://mirrors.ustc.edu.cn/alpine/edge/testing
@community http://mirrors.ustc.edu.cn/alpine/edge/community
```
2. apk更新后，重启，否则docker启动失败，报iptables相关错误  
```shell
# 重启后失败再尝试以下命令
sudo modprobe ip_tables
sudo echo 'ip_tables' >> /etc/modules
```

3. 安装软件包
```shell
# mater节点
sudo apk add kubernetes@testing
sudo apk add docker@community
sudo apk add cni-plugins@testing
sudo apk add kubelet@testing
# node节点
sudo apk add docker@community
sudo apk add kubelet@testing
```

3. kubeadm init 的时候指定镜像源
```shell
# 先查看IP和kubernetes的版本
kubeadm version
# init的时候指定registry源
sudo kubeadm init --kubernetes-version=v1.23.4 --image-repository registry.aliyuncs.com/google_containers   --apiserver-advertise-address=192.168.33.10
```

记录命令执行后返回的结果
```shell
kubeadm join 192.168.33.10:6443 --token 1pqsgh.sj4qorf22r5ad9sn \
        --discovery-token-ca-cert-hash sha256:e85a489c6999bb9e57db41864190a53d60222358b51d604c7da627f23ee58163
````

4. 执行kubectl 命令失败 **port 8080 refused**错误
```shell
# /etc/kubernetes/admin.conf  默认使用该路径下配置文件执行命令存在以上问题，遂修改
  mkdir -p ~/.kube
  sudo cp -i /etc/kubernetes/admin.conf ~/.kube/config
  sudo chown $(id -u):$(id -g) ~/.kube/config
  export KUBECONFIG=~/.kube/config
```

5. weave （该步骤作用不清楚，使用weave创建了什么）
```shell
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
````

6. 执行`kubeadm join`操作

6. 其他
* 修改主机名，默认主机名一致



Tags:
  k8s