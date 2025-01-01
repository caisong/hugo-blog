---
title: Docker容器基于宿主机内核，容器的内核和宿主机的内容相同。
date: 2024-07-04T21:42:10+08:00
lastmod: 2024-07-04T21:42:10+08:00
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
docker容器基于宿主机内核，容器的内核和宿主机的内容相同。

1. elrepo 升级 centos 7 kernel
2. centos 7 创建 centos 8 容器
3. 验证centos 8 容器中能够正常运行dpdk 、目标程序
dpdk 主要是module

如果centos7 升级内核，可以不用高版本glibc，直接使用汇编实现系统调用