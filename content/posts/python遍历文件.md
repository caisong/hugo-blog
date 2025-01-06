---
title: Python遍历文件
date: 2021-09-03T21:42:18+08:00
lastmod: 2021-09-03T21:42:18+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - python2
tags:
  - python2
# nolastmod: true
draft: false
---

python 遍历文件
```python
import os

s = os.sep
root = "d:" + s + "ll" + s 

for rt, dirs, files in os.walk(root):
    for f in files:
        fname = os.path.splitext(f)
        new = fname[0] + 'b' + fname[1]
        os.rename(os.path.join(rt,f),os.path.join(rt,new))
```

