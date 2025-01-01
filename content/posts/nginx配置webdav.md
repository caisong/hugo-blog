---
title: Nginx配置webdav
date: 2024-12-20T21:41:58+08:00
lastmod: 2024-12-20T21:41:58+08:00
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
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
## nginx配置webdav

* nginx配置
```nginx
server {
	listen 10080;
	server_name localhost;
	charset utf-8;
	root /home/dav;
	# root /home/dav/$remote_addr;

	auth_basic realm_name;
	auth_basic_user_file /etc/nginx/.passwords.list;

	dav_methods PUT DELETE MKCOL COPY MOVE;
	dav_ext_methods PROPFIND OPTIONS;

	dav_access user:rw group:rw all:r;

	client_body_temp_path /tmp;
	client_max_body_size 0;
	create_full_put_path on;
}
```

* 设置用户名/密码
```bash
echo -n 'lpwm:' | sudo tee /etc/nginx/.passwords.list
openssl passwd -apr1 | sudo tee -a /etc/nginx/.passwords.list
```

* 设置挂载目录权限
```bash
sudo chown -r www-data:www-data /home/dav
```

* 启动
```bash
nginx -t 
nginx -s reload
nginx
```

## 验证
```bash
sudo apt install cadaver
cadaver http://127.0.0.1:10080
```

**使用curl未尝试成功，使用的cadaver客户端**

Tags:
  webdav