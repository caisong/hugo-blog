---
title: Excel条件变色
date: 2017-02-09T17:28:58+08:00
lastmod: 2017-02-09T17:28:58+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 编程
  - excel
tags:
  - excel
  - python2
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->


```plain
=EXACT(INDIRECT(ADDRESS(ROW(), COLUMN()-1)), "FAIL")
```
```plain
=EXACT(INDIRECT(ADDRESS(2, COLUMN()+1)), "Rate")
=INDIRECT(ADDRESS(ROW(),COLUMN()+1))>INDIRECT(ADDRESS(ROW(),4))
=INDIRECT(ADDRESS(ROW(),COLUMN()+1))<INDIRECT(ADDRESS(ROW(),5))
```

# excel python
```python
#!/usr/bin/python
# --*--coding:utf-8 --*--
from openpyxl import Workbook
from openpyxl.compat import range
from openpyxl.utils import get_column_letter
from openpyxl.styles import Font
from openpyxl.styles.colors import RED

wb = Workbook()

dest_filename = 'empty_book.xlsx'

ws1 = wb.active
ws1.title = "range names"

for row in range(1, 40):
    ws1.append(range(600))

ws2 = wb.create_sheet(title="Pi")
font = Font(color=RED)
ws2['F5'] = 3.14
ws2['F5'].font = font

ws3 = wb.create_sheet(title="Data")
for row in range(10, 20):
    for col in range(27, 54):
        _ = ws3.cell(column=col, row=row, value="{0}".format(get_column_letter(col)))
wb.save(filename = dest_filename)
```
