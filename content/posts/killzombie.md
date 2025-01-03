---
title: Kill zombie
date: 2024-10-09T21:41:03+08:00
lastmod: 2024-10-09T21:41:03+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - linux
  - zombie
# nolastmod: true
draft: false
---


```bash
ps -A -o stat,ppid,pid,cmd | grep -e '^[Zz]' | awk '{print $2}' | xargs kill -9
```
