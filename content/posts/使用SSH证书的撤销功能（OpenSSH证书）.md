---
title: 使用SSH证书的撤销功能（OpenSSH证书）
date: 2024-12-30T21:41:52+08:00
lastmod: 2024-12-30T21:41:52+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - ssh
  - 证书
# nolastmod: true
draft: false
---

## ssh 证书CA授权

```shell
# 授权给用户
ssh-keygen -s /path/to/ca_key -I 标识 -n username -V +52w -z <serial number> /path/to/client.pub
```
* 52w 一年, 另外还支持授权给`host`

`/etc/ssh/sshd_config`中添加`ca` 证书公钥
```shell
# 用户信任列表
TrustedUserCAKeys /path/to/pub-cert.pub
```

## 撤销授权
```shell
ssh-keygen -k -f krl_file -z <serial number> xk-cert.pub
# -s 指定ca公钥
# -k 指定撤销
```
ps. 不要使用ca 公钥去撤销，要使用授权时的序列表，否则该ca证书的所有授权都不被取消

`/etc/ssh/sshd_config`中添加撤销文件
```plain
# 撤销列表 
RevokedKeys /path/to/crl_file
```