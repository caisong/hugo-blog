---
title: Make modules
date: 2021-09-03T21:41:10+08:00
lastmod: 2021-09-03T21:41:10+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 编程
tags:
  - module
# nolastmod: true
draft: false
---

编译module
```shell
make -C {kernel src} -M=`pwd` modules
```
