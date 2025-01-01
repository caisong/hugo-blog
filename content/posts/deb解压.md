---
title: Deb解压
date: 2021-09-03T21:40:37+08:00
lastmod: 2021-09-03T21:40:37+08:00
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
# deb 解压

获取deb包：
apt-get    download 包名

解压deb包：
ar -x pakname.deb

解压deb完毕后会发现多出几个文件，这里主要用到data.tar.gz等包，这个是放着二进制文件的包，用tar解压这个包
tar -zxf data.tar.gz


Tags:
  deb, linux