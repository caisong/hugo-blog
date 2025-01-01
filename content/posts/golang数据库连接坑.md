---
title: Golang数据库连接坑
date: 2024-08-30T21:40:55+08:00
lastmod: 2024-08-30T21:40:55+08:00
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
# golang 数据库连接坑

1. sql.Open 只是解析了连接表达式，实际并未连接。验证是否能够连通，需要使用Ping操作  
2. queryRow实际也未执行查询，查询需要等到scan时才执行  