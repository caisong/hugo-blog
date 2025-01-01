---
title: Alpine无法使用minikube，具体原因未知
date: 2021-12-21T21:42:07+08:00
lastmod: 2021-12-21T21:42:07+08:00
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
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
* alpine 无法使用minikube，具体原因未知

* docker安装
debian 最新版impish没有对应包，无法安装，debian上用上衣发行版 **bullseye**
软件源啥的可以参考中科大源

* minikube 启动
```shell
# CPU 和 memroy在VM中未成功，好像依赖cgroup
# --vm-driver=none --driver=docker 参数可能只有driver有用了，minikube可以不基于dcoker
minikube start --image-mirror-country='cn' --cpus 4  --memory 2048M 
```

* kubectl安装
直接按照官方手册就行

* Q&A
1. 虚拟机执行`minikube dashboard`后监听`127.0.0.1`如何访问
```bash
# 获取URL
kubectl dashboard --url
# 代理？
# accept-host 在虚拟机中可不加，virtual box靠端口映射，就是本机IP
kubectl proxy --address 0.0.0.0 --accpept-hosts <your-host_external-ip>
```
2. 镜像获取 （部分镜像找不到会失败）
```bash
images=(
    kube-apiserver-amd64:v1.18.4
    kube-controller-manager-amd64:v1.18.4
    kube-scheduler-amd64:v1.18.4
    kube-proxy-amd64:v1.18.4
    pause:3.2
    etcd-amd64:3.4.3
    coredns:1.6.7
)

for imageName in ${images[@]} ; do
    docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
    docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName
done
```

3 kubectl自动补全
```bash
apt-get install bash-completion
# yum install bash-completion
kubectl completion bash >/etc/bash_completion.d/kubectl
source /usr/share/bash-completion/bash_completion
```



Tags:
  kubectl, minikube