---
title: Pip install UnicodeDecodeError
date: 2021-09-03T21:41:18+08:00
lastmod: 2021-09-03T21:41:18+08:00
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
  - pip
# nolastmod: true
draft: false
---

## pip install UnicodeDecodeError

解决方法：
python目录 `Python27\Lib\site-packages` 建一个文件`sitecustomize.py`
内容为：

```python
import sys
sys.setdefaultencoding('gbk')
```