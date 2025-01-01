---
title: Disablediskcache
date: 2021-09-03T21:40:38+08:00
lastmod: 2021-09-03T21:40:38+08:00
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
# disable disk cache
```shell
hdparm -W 0 /dev/sda1 #disable
hdparm -W 1 /dev/sda1 #enable
```


Tags:
  linux