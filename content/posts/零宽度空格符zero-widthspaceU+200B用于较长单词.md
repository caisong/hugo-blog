---
title: 常用零宽字符
date: 2021-09-06T21:42:30+08:00
lastmod: 2021-09-06T21:42:30+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 其他
tags:
  - 零宽字符
  - 水印
# nolastmod: true
draft: false
---

**零宽字符**是字节宽度为0的特殊字符，可以用于文本加密、文章水印等。记录下常见的零宽字符。

<!--more-->

* 零宽度空格符 (zero-width space) U+200B : 用于较长单词的换行分隔
* 零宽度断字符 (zero-width non-joiner) U+200C : 用于阿拉伯文，德文，印度语系等文字中，阻止会发生连字的字符间的连字效果
* 零宽度连字符 (zero-width joiner) U+200D : 用于阿拉伯文与印度语系等文字中，使不会发生连字的字符间产生连字效果
* 左至右符 (left-to-right mark) U+200E : 用于在混合文字方向的多种语言文本中（例：混合左至右书写的英语与右至左书写的希伯来语），规定排版文字书写方向为左至右
* 右至左符 (right-to-left mark) U+200F : 用于在混合文字方向的多种语言文本中，规定排版文字书写方向为右至左
* U+202A LEFT-TO-RIGHT EMBEDDING
* U+202C POP DIRECTIONAL FORMATTING
* U+202D LEFT-TO-RIGHT OVERRIDE
* U+2062 INVISIBLE TIMES
* U+2063 INVISIBLE SEPARATOR
* 零宽度非断空格符 (zero width no-break space) U+FEFF : 用于阻止特定位置的换行分隔
