---
title: deb解压
date: 2021-09-03T21:40:37+08:00
lastmod: 2021-09-03T21:40:37+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - deb
# nolastmod: true
draft: false
---

deb 格式还是基于zip封装的，有自己的头部，后部分内容还是zip。可以直接使用7zip打开。linux终端下可以按以下操作：
<!--more-->

获取deb包：
```shell
apt-get    download 包名
```

解压deb包：`ar -x pakname.deb`

解压deb完毕后会发现多出几个文件，这里主要用到data.tar.gz等包，这个是放着二进制文件的包，用tar解压这个包
`tar -zxf data.tar.gz`

