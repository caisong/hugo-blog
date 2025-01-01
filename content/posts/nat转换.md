---
title: Nat转换
date: 2022-08-27T21:41:13+08:00
lastmod: 2022-08-27T21:41:13+08:00
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
# nat 转换
```shell
# 交换机内网端口
int g0/0/1
ip address 192.168.10.254 255.255.255.0
# 交换机外网端口
int g0/0/20/0/2
ip address 137.25.10.1 255.255.255.0

# 端口允许通过
acl 1000
rule permit source 192.168.10.0. 0.0.0.255

# 与互联网互联的端口添加nat映射
# nat 转换IP不要与已有IP冲突
nat address-group 1 137.25.10.2 137.25.10.4
int g0/0/1
nat ountbound 1000 address-group 1
```