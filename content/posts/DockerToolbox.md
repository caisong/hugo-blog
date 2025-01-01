---
title: DockerToolbox
date: 2021-09-03T21:42:09+08:00
lastmod: 2021-09-03T21:42:09+08:00
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
Docker Toolbox

在Windows、Mac系统上使用Docker Toolbox使用Docker的话
推荐做法是在创建Linux虚拟机的时候，就将加速器的地址配置进去
docker-machine create --engine-registry-mirror=<your accelerate address> -d virtualbox default
docker-machine env default
eval "$(docker-machine env default)"
docker info


如果你已经通过docker-machine创建了虚拟机的话，则需要通过登录机器修改配置了
首先通过docker-machine ssh <machine-name>登录虚拟机
然后修改/var/lib/boot2docker/profile文件，将--registry-mirror=<your accelerate address>添加到EXTRA_ARGS中
最后sudo /etc/init.d/docker restart重启Docker服务就可以了

Tags:
  docker, windows