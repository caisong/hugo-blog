---
title: Shell 常用函数
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
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
## 带颜色打印
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

## 忘记干啥的了

```shell
awk '{for(i=0;++i<=NF;)a[i]=a[i]?a[i] FS $i:$i}END{for(i=0;i++<NF;)print a[i]}' 
```

## `++i`操作
```shell
a=1  
a=$(($a+1))  
a=$[$a+1]  
a=`expr $a + 1`  
let a++  
let a+=1
```