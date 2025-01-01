---
title: Ipv6地址设定
date: 2021-09-03T21:41:59+08:00
lastmod: 2021-09-03T21:41:59+08:00
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
### ipv6地址设定

```shell
ifconfig eth0 inet6 add 3ffe:ffff:0:f101::1/64 
ip -6 addr add 3ffe:ffff:0:f101::1/64 dev eth0 
```
### 路由设置
```shell
route add –host 192.168.168.110 dev eth0
route add –host 192.168.168.119 gw 192.168.168.1
# 添加到网络的路由
route add –net IP netmask MASK eth0
route add –net IP netmask MASK gw IP
route add –net IP/24 eth1
# 添加默认网关
route add default gw IP
#删除路由
route del –host 192.168.168.110 dev eth0
```

Tags:
  ip, linux