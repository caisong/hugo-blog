---
title: PG数据库、用户操作
date: 2024-11-28T21:41:17+08:00
lastmod: 2024-11-28T21:41:17+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - database
tags:
  - postgresql
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# PG 数据库、用户相关
```sql
-- 创建数据库
CREATE DATABASE mydatabase;

-- 创建用户
CREATE USER myuser WITH PASSWORD 'mypassword';

-- 授予用户数据库的所有权限
GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;

-- 切换到目标数据库
\c mydatabase

-- 授予用户所有现有表的所有权限
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO myuser;

-- 授予用户对新表的默认权限
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL PRIVILEGES ON TABLES TO myuser;

-- 授予用户视图和序列的权限（可选）
GRANT ALL PRIVILEGES ON ALL VIEWS IN SCHEMA public TO myuser;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO myuser;
```