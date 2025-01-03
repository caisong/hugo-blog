---
title: GPG错误NOPUBLICKEY
date: 2021-09-03T21:42:15+08:00
lastmod: 2021-09-03T21:42:15+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - gpg
# nolastmod: true
draft: false
---

GPG错误 NO PUBLIC KEY
[no pulic key 修复](https://my.oschina.net/emptytimespace/blog/83633)

ubuntu有效
```shell
apt-get install debian-keyring debian-archive-keyring
apt-key update
apt-get upgrade
```
