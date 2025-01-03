---
title: 自签HTTPS证书
date: 2022-08-30T21:40:59+08:00
lastmod: 2022-08-30T21:40:59+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - https
  - linux
# nolastmod: true
draft: false
---

# HTTPS证书

```shell
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
```