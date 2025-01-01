---
title: Shell打印
date: 2024-12-13T21:41:32+08:00
lastmod: 2024-12-13T21:41:32+08:00
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
# shell 打印
```bash
#!/bin/bash

# 红色
printf "\033[31mThis is red text\033[0m\n"

# 绿色
printf "\033[32mThis is green text\033[0m\n"

# 黄色
printf "\033[33mThis is yellow text\033[0m\n"

# 蓝色
printf "\033[34mThis is blue text\033[0m\n"
```