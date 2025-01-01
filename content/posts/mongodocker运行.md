---
title: Mongodocker运行
date: 2024-11-04T21:41:12+08:00
lastmod: 2024-11-04T21:41:12+08:00
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
# mongo docker运行
```bash
docker run -d -p 27017:27017 -v mongo-data:/data/db -e MONGODB_INITDB_ROOT_USERNAME=username -e MONGODB_INITDB_ROOT_PASSWORD=password mongo
```
