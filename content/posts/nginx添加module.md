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
  - nginx
tags:
  - nginx
  - module
# nolastmod: true
draft: false
---

1. 直接`nginx -V`查看运行的nginx的编译参数
2. 下载源码，使用对应的nginx参数编译nginx
3. 下载module，编译

```bash
# 先编译nginx，nginx编译成功后，再重新configure
末尾添加你需要的编译的module
--with-http_dav_module --add-dynamic-module=/root/nginx-dav-ext-module-3.0.0
```

4. 部署


```conf
# 添加module，so 放在 /usr/lib64/nginx/modules
load_module modules/ngx_http_dynamic_etag_module.so;
```
