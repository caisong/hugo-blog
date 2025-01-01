---
title: Linux查看库信息常用命令
date: 2021-09-03T21:41:06+08:00
lastmod: 2021-09-03T21:41:06+08:00
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
# linux 查看库信息常用命令

```bash
# file 查看so文件是32位还是64位
$file libhadoop.so.1.0.0

libhadoop.so.1.0.0: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, not stripped
```

nm用来列出目标文件的符号清单.

ar命令可以用来创建、修改库，也可以从库中提出单个模块。


objdump：显示目标文件中的详细信息
objdump -d <command>，可以查看这些工具究竟如何完成这项任务
ldd  查看可执行文件链接了哪些  系统动态链接库
-d是ldd的缩写

readelf 显示关于 ELF 目标文件的信息

readelf -d libffmpeg.so | grep NEEDED

Tags:
  linux