---
title: Spider基础
date: 2021-09-03T21:41:34+08:00
lastmod: 2021-09-03T21:41:34+08:00
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
# spider 基础
* 基础代码
```python
import urllib.request
import urllib.parse
data = urllib.parse.urlencode({'spam': 1, 'eggs': 2, 'bacon': 0})
# urlopen 传入参数是bytes，urlencode返回的是str，必须encode
data = data.encode('ascii')
with urllib.request.urlopen("http://requestb.in/xrbl82xr", data) as f:
	print(f.read().decode('utf-8'))
```

* urlencode 接口
```plain
urllib.parse.urlencode(query, doseq=False, safe='', encoding=None, errors=None, quote_via=quote_plus)
Convert a mapping object or a sequence of two-element tuples, which may contain str or bytes objects, to a percent-encoded ASCII text string. If the resultant string is to be used as a data for POST operation with the urlopen() function, then it should be encoded to bytes, otherwise it would result in a TypeError.
```

Tags:
  python, spider, 爬虫