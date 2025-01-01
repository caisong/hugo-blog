---
title: Setiponstartup
date: 2021-09-03T21:41:31+08:00
lastmod: 2021-09-03T21:41:31+08:00
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
# set ip on startup
1. update-rc.d
	* the script (setipaddr.sh)
``` shell
#! /bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/bin:$PATH
ipconfig eth0 192.168.10.1/24
```
	* update-rc.d setting
```shell
chmod +x setipaddr.sh
mv setipaddr.sh /etc/init.d
update-rc.d setipaddr.sh defaults
```
	* run level
```shell
# If defaults is used then update-rc.d will make links to start the service in runlevels 2345 and to stop the service in runlevels 016
runlevel # get current level
```

2. systemctl
	*  service file (/etc/systemd/system/setipaddr.service)  
	
```shell
[Unit]
Description=set ip on boot
After=network.target

[Service]
Type=oneshot
ExecStart=/opt/bin/setipaddr.sh

[Install]
WantedBy=multi-user.target
```

```shell
systemctl enable vgaoff.service
```



Tags:
  ciat