---
title: Rsh 配置
date: 2021-09-03T21:41:26+08:00
lastmod: 2021-09-03T21:41:26+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - rsh
# nolastmod: true
draft: false
---
基于LTP做测试用的，现在rsh较少使用了，仅记录
1. 安装xinetd
2. 添加rsh rexec rlogin 至/etc/securetty (root权限问题参考其他文档)
3. 配置conf文件，位于/etc/xinetd.d/
4. 配置hosts
5. 添加“machine_name user_name” >> ~/.rhosts
6. 重启服务
