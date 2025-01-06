---
title: Salt docker cluster
date: 2024-07-16T21:42:23+08:00
lastmod: 2024-07-16T21:42:23+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - saltstack
  - docker
  - dockerfile
# nolastmod: true
draft: false
---

salt docker cluster dockerfile
```yaml
version: "3"
services:
  master:
    image: saltstack/salt
    hostname: salt-master
    ports:
      - 60080:8000
    environment: 
      - SALT_MASTER_CONFIG={"netapi_enable_clients":["local", "local_aysnc", "local_batch", "local_subset", "runner", "wheel", "runner_async"], "file_roots":{"base":["/srv/salt"], "formula":["/srv/formula/my-formula-0.0.2"]}}
    volumes:
      - ./srv:/srv
    networks:
      - backend
  
  minion1:
    image: saltstack/salt
    hostname: minion1
    environment:
      - SALT_MINION_CONFIG={"master":"salt-master"}
    networks:
      - backend
    
  minion2:
    image: saltstack/salt
    hostname: minion2
    environment:
      - SALT_MINION_CONFIG={"master":"salt-master"}
    networks:
      - backend

networks:
  backend:
```