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
  - docker
tags:
  - webdav
# nolastmod: true
draft: false
---

基于容器创建webdav服务

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