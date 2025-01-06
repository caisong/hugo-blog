---
title: nginx双向代理
date: 2024-09-23T21:41:15+08:00
lastmod: 2024-09-23T21:41:15+08:00
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
# nolastmod: true
draft: false 
---

使用nginx当双向代理

```nginx
server{
	server_name 10.10.110.10 ssl;
	listen 16002;
	
	ssl_certificate /path/to/your_certificate.crt;
	ssl_certificate_key /path/to/your_private.key;
	ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
	ssl_session_cache shared:SSL:10m;
	ssl_session_timeout 10m;
	ssl_prefer_server_ciphers on;

	# 转发node --> center
	location /webchat/openapi/v1 {
		proxy_pass https://10.10.110.12:16002;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
	}
	
	# center --> node	
	location /webChatClient/openapi/v1 {
		proxy_pass https://10.10.110.20:8123;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
	}
}
```