---
title: Ensp三层路由
date: 2022-08-22T21:40:46+08:00
lastmod: 2022-08-22T21:40:46+08:00
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
# ensp 三层路由
```shell
# 两个交换机
# 第二层交换机配置网关
vlan batch 10 to 20
int g0/0/1
port link-type trunk
port trunk allow-pass vlan 10 20 30 

int vlanif 10
ip address 192.168.10.254 255.255.255.0

int vlanif 20
ip address 192.168.20.254 255.255.255.0

int vlanif 30
ip address 192.168.30.254 255.255.255.0
```
