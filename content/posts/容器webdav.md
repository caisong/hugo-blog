---
title: 容器webdav
date: 2024-12-24T21:41:51+08:00
lastmod: 2024-12-24T21:41:51+08:00
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
# 容器 webdav
```Dockerfile
version: '3'
services:
  webdav:
    image: bytemark/webdav
    restart: always
    ports:
      - "80:80"
    environment:
      AUTH_TYPE: Digest
      USERNAME: alice
      PASSWORD: secret1234
    volumes:
      - /srv/dav:/var/lib/dav
```