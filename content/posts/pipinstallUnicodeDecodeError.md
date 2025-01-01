---
title: PipinstallUnicodeDecodeError
date: 2021-09-03T21:41:18+08:00
lastmod: 2021-09-03T21:41:18+08:00
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
# pip install UnicodeDecodeError

解决方法：
python目录 Python27\Lib\site-packages 建一个文件sitecustomize.py
内容为：
import sys
sys.setdefaultencoding('gbk')

Tags:
  python