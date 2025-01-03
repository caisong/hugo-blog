---
title: sql server数据转存mongodb
date: 2021-09-03T21:41:11+08:00
lastmod: 2021-09-03T21:41:11+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - python2
tags:
  - sql server
  - mongodb
# nolastmod: true
draft: false
category: database
---

写得比较简单，直接查询插入了

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-


import pymssql
import pymongo

sql = '''SELECT [Name]
      ,[CardNo]
      ,[Descriot]
      ,[CtfTp]
      ,[CtfId]
      ,[Gender]
      ,[Birthday]
      ,[Address]
      ,[Zip]
      ,[Dirty]
      ,[District1]
      ,[District2]
      ,[District3]
      ,[District4]
      ,[District5]
      ,[District6]
      ,[FirstNm]
      ,[LastNm]
      ,[Duty]
      ,[Mobile]
      ,[Tel]
      ,[Fax]
      ,[EMail]
      ,[Nation]
      ,[Taste]
      ,[Education]
      ,[Company]
      ,[CTel]
      ,[CAddress]
      ,[CZip]
      ,[Family]
      ,[Version]
  FROM cdsgus'''

ms_conn = pymssql.connect(host="127.0.0.1", user="sa",
                          password="root", database="database", charset="utf8")
ms_cur = ms_conn.cursor(as_dict=True)
ms_cur.execute(sql)

row = ms_cur.fetchone()

mongo_conn = pymongo.MongoClient('127.0.0.1', 27017)
mongo_db = mongo_conn['test']

while row:
    mongo_db.kf_data.insert_one(row)
    row = ms_cur.fetchone()

ms_conn.commit()
ms_conn.close()

```

