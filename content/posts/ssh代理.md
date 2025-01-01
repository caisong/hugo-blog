---
title: Ssh代理
date: 2024-10-28T21:42:25+08:00
lastmod: 2024-10-28T21:42:25+08:00
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
ssh代理
```bat
@echo off
start /b ssh -N -f -D 10080 caisong@190.92.245.8 -i 190.92.245.8_3
```