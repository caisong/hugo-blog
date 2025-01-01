---
title: Shell实现++i操作
date: 2021-09-03T21:42:25+08:00
lastmod: 2021-09-03T21:42:25+08:00
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
* shell 实现`++i`操作
```shell
a=1  
a=$(($a+1))  
a=$[$a+1]  
a=`expr $a + 1`  
let a++  
let a+=1
``` 

Tags:
  shell