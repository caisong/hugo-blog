---
title: Install nodejs
date: 2021-09-03T21:41:01+08:00
lastmod: 2021-09-03T21:41:01+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - nodejs
tags:
  - nodejs
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# install nodejs

1. 官网下载nodejs安装

2. 修改环境配置
  ```cmd
  npm config set prefix "C:\Program Files\nodejs\node_global"
  npm config set cache "C:\Program Files\nodejs\node_cache"
  ```

3. 添加`D:\Program Files\nodejs\node_global\`至`PATH`，新安装的包会在该`node_global`下建立link

4. 安装cnpm
  ```cmd
  # 这个域名已经失效了
  # npm install -g cnpm --registry=https://registry.npm.taobao.org
  # 新的
  npm config set registry https://registry.npmmirror.com
  ```
