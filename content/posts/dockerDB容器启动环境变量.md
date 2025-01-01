---
title: DockerDB容器启动环境变量
date: 2024-07-22T21:40:38+08:00
lastmod: 2024-07-22T21:40:38+08:00
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
# docker DB 容器启动环境变量  

```shell
#PG
docker run --rm -e POSTGRES_USER=caisong -e POSTGRES_PASSWORD=1111111111 -e POSTGRES_DB=test -p 5432:5432 postgres
```

```shell
# REDIS
docker run --name myredis -p 6379:6379 --rm redis:latest redis-server --requirepass "root123456"
```

mongodb 需要容器启动后，创建用户名和密码
```shell
# mongodb
# 创建容器
docker run --rm -p 27017:27017 mongo --auth
# 进入容器
docker exec -it {container_name} mongo admin
```

```mongodb
db.createUser({user:"admin", pwd:"admin123456", roles:[{role:"userAdminAnyDatabase", db:"admin"}]});
```