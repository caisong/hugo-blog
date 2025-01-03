---
title: golang 编译动态参数
date: 2024-07-22T21:40:55+08:00
lastmod: 2024-07-22T21:40:55+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - golang
tags:
  - 条件编译
# nolastmod: true
draft: false
---

golang 编译时指定变量值

<!--more-->

```shell
go build -ldflags "-w -s -X main.Version=${VERSION} -X github.com/demo/version.BuildNo=${BUILD_NO}"

参数说明：

-w 删除DWARF信息：编译出来的程序无法用gdb进行调试。

-s 删除符号表：panic的stack trace没有文件名/行号信息，等价于C/C++程序被strip。

-X 替换包中的变量的值。
```