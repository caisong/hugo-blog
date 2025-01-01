---
title: Python换行符处理
date: 2021-09-03T21:41:22+08:00
lastmod: 2021-09-03T21:41:22+08:00
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
# python换行符处理

##  Python 2（PEP 278 -- Universal Newline Support）
  1. 如果不是txt文件，建议用wb和rb来读写。通过二进制读写，不会有换行问题。
  2. 如果需要明文内容，请用rU来读取（**强烈推荐**），即**U通用换行模式（Universal new line mode）。该模式会把所有的换行符（\r \n \r\n）替换为\n**。只支持读入，但是也足够了。这是Python 提供给我们的最好的选择，没有之一。

  对比r和rU的结果：
  ```python
  content = file(fn, 'r').read()
  # test\r\ntest2
  # 这里的换行会因不同系统而不同                       
  content = file(fn, 'rU').read()
  # test\ntest2
  # 所有的换行都被统一，不分系统
```

## Python 3(Open函数: 2. Built-in Functions)
** 请注意：Python 3不推荐用rU模式！**

```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True)
```
在Python 3，可以通过open函数的**newline**参数来控制**Universal new line mode**：读取时候，不指定newline，则默认开启Universal new line mode，所有\n, \r, or \r\n被默认转换为\n ；写入时，不指定newline，则换行符为各系统默认的换行符（\n, \r, or \r\n, ），指定为newline='\n'，则都替换为\n（相当于Universal new line mode）；不论读或者写时，newline=''都表示不转换。

作者：知乎用户
链接：https://www.zhihu.com/question/19751023/answer/19909758
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

Tags:
  python