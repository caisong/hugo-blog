---
title: Rsyslogrfc3164
date: 2024-12-26T21:41:28+08:00
lastmod: 2024-12-26T21:41:28+08:00
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
# rsyslog rfc3164
```plaintext
# RFC 3164

<PRI><HEADER> <MSG>

PRI和HEADER之间无空格

PRI = "<"Priority">"
Priority = (Facility<<3)+Severity
Facility = 0~23
Serverity = 0~7

HEADER = <TIMESTAMP> <HOSTNAME>

TIMESTAMP = Mmm  dd hh:mm:ss 
Mmm 代表月份，与dd之间有2个空格
时间使用24小时制

HOSTNAME 就是正常的hostname，不能有空格，或者使用IPv4 IPv6地址。

MSG = <TAG><CONTENT>
TAG就是程序名，不操作32字节，tag中的非字母符号就代表结束。因此CONTENT开头经常使用“[“、“：”或者空格表示内容的开始。
```

Tags:
  rsyslog