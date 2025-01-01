---
title: Change Partion Size
date: 2017-05-18T17:41:05+08:00
lastmod: 2017-05-18T17:41:05+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - linux
  - 磁盘
# nolastmod: true
draft: false
---

修改分区大小

<!--more-->

```shell
lsblk
fdisk /dev/mmcblk0
# delte partion and create
resize2fs /dev/mmcblk0p2 
```
