---
title: Docker fuse
date: 2024-12-24T21:40:39+08:00
lastmod: 2024-12-24T21:40:39+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - docker
tags:
  - fuse
# nolastmod: true
draft: false
---

docker fuse权限问题

<!--more-->

# docker fuse

At first, you should have docker image with installed fuse package inside container. For allow mount inside container need to run docker run command with `--cap-add SYS_ADMIN --device /dev/fuse:/dev/fuse --security-opt apparmor:unconfined`

For docker-compose need to put inside docker-compose.yml file: 
```yaml
cap_add:
  - SYS_ADMIN
devices:
  - /dev/fuse:/dev/fuse
security_opt:
  - apparmor:unconfined
```
