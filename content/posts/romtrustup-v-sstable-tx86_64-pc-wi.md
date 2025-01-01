---
title: Romtrustup v Sstable Tx86_64 Pc Wi
date: 2024-01-04T21:42:21+08:00
lastmod: 2024-01-04T21:42:21+08:00
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
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
romt rustup -v -s stable -t x86_64-pc-windows-gnu -t linux --url https://mirror.nju.edu.cn/rustup/rustup download

需要预先将日期目录内下载stable的toml和对应sha256验证文件
romt toolchain -v -s stable -t x86_64-pc-windows-gnu -t linux --url https://mirror.nju.edu.cn/rustup/dist --no-signature download

romt crate -v --index-url https://mirrors.aliyun.com/crates.io-index.git  init

romt crate -v --keep-going --crates-url https://mirrors.aliyun.com/crates/api/v1/crates/{crate}/{version}/download update



https://crates-io.proxy.ustclug.org/api/v1/crates

0e3b3b0db16628fc9644f46be8b6774bf8e6026f

romt crate -v --index-url https://mirrors.aliyun.com/crates.io-index.git init

https://mirrors.aliyun.com/crates.io-index.git

https://rsproxy.cn/crates.io-index

romt crate --index-url https://mirrors.aliyun.com/crates.io-index.git --crates-url https://mirrors.aliyun.com/crates/api/v1/crates/{crate}/{version}/download   -v --keep-going export


# 导入
romt toolchains -v import
romt rustup -v iport
romt crate init-import
romt crate config
romt crate -v import
romt crate serve



