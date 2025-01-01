---
title: Alpinevsftp搭建
date: 2024-07-18T21:42:06+08:00
lastmod: 2024-07-18T21:42:06+08:00
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
alpine vsftp  搭建
```ini
anonymous_enable=NO
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
listen=YES
local_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
background=NO
ftpd_banner=Welcome to FTP Server
dirmessage_enable=YES
max_clients=10
max_per_ip=5
write_enable=YES
local_umask=022
passwd_chroot_enable=yes
listen_ipv6=NO
seccomp_sandbox=NO
log_ftp_protocol=YES
xferlog_enable=YES
xferlog_std_format=NO
dual_log_enable=YES
xferlog_file=/var/log/vsftpd/xferlog.log
vsftpd_log_file=/var/log/vsftpd/vsftpd.log
```

创建用户
```bash
addgroup -S ftpuser
adduser -D -G ftpuser -h /home/vsftpd/ftpuser -s /bin/false ftpuser
mkdir -p /home/vsftpd/ftpuser
chown -R ftpuser:ftpuser /home/vs

echo "$FTP_USER:$FTP_PASS" | /usr/sbin/chpasswd
```

启动服务
```bash
rc-service vsftpd start
```