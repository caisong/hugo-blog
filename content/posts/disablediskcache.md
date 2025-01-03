---
title: Disable disk cache
date: 2021-09-03T21:40:38+08:00
lastmod: 2021-09-03T21:40:38+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - linux
# nolastmod: true
draft: false
---

disable disk cache
```shell
hdparm -W 0 /dev/sda1 #disable
hdparm -W 1 /dev/sda1 #enable
```
