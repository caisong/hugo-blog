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
  - 运维
tags:
  - centos
  - syslog
# nolastmod: true
draft: false
---

centos 7 默认不携带mmnormlize这个module,需要额外安装

<!--more-->

```bash
curl -O http://rpms.adiscon.com/v8-stable/rsyslog.repo 

yum install rsyslog rsyslog-mmnormalize rsyslog-kafka rsyslog-openssl rsyslog-pgsql
```