---
title: Enspacl
date: 2022-08-23T21:40:45+08:00
lastmod: 2022-08-23T21:40:45+08:00
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
# ensp acl

```shell
# 不知道指令直接输入？会有提示
acl name test
# 进入acl
rule deny ip source 192.168.10.0 0.0.0.255 destination 192.168.30.0 0.0.0.255
rule permit ip source any dentination any
q


int g0/0/03
traffic-filter inbound acl name test
```