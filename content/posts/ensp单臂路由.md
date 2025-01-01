---
title: Ensp单臂路由
date: 2022-08-16T21:40:47+08:00
lastmod: 2022-08-16T21:40:47+08:00
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
# ensp单臂路由
```shell
# 关闭提示信息
# undo info-center enable
un in en

# 进入system view
sys
# 创建vlan，批量创建待补充
vlan 10
vlan 20

# 交换机
# 端口操作
int g0/0/1
port link-type access
port default vlan 10

int g0/0/2
port link-type access
port default vlan 20

int g0/0/3
port link-type trunk
port trunk allow-pass vlan 10 20

# 路由器
int e0/0/0.1
dot1q termination vid 10
ip address 192.168.1.254 24
arp broadcast enable

int e0/0/0.2
dot1q termination vid 20
ip address 192.168.2.254 24
arp br en
```

Tags:
  ensp