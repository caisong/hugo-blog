---
title: Nginx添加module
date: 2024-12-18T21:41:13+08:00
lastmod: 2024-12-18T21:41:13+08:00
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
# nginx 添加module

```bash
# 先编译nginx，nginx编译成功后，再重新configure
末尾添加你需要的编译的module
--with-http_dav_module --add-dynamic-module=/root/nginx-dav-ext-module-3.0.0
```


```conf
# 添加module，so 放在 /usr/lib64/nginx/modules
load_module modules/ngx_http_dynamic_etag_module.so;
```
