---
title: Centos更新rsyslog
date: 2024-12-27T21:40:34+08:00
lastmod: 2024-12-27T21:40:34+08:00
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
# centos 更新rsyslog
```bash
curl -O http://rpms.adiscon.com/v8-stable/rsyslog.repo 

yum install rsyslog rsyslog-mmnormalize rsyslog-kafka rsyslog-openssl rsyslog-pgsql
```