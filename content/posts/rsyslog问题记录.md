---
title: Rsyslog 问题记录
date: 2024-12-24T21:42:22+08:00
lastmod: 2024-12-24T21:42:22+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - rsyslog
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
rsyslog问题记录
* 特殊字符编码
`/etc/rsyslog.conf` 关闭相关配置 `$EscapeControlCharactersOnReceive off`

* msg 空格开头
索引默认从1开始
$template MYFORMAT,"%msg:2:$%\n"

* 系统属性使用
那些属性就是要$开头，即使在%%内

 $template DynamicFile,"/var/log/test_logs/%timegenerated%-test.log"
     *.* ?DynamicFile

**使用 timegenerated 生成文件名，使用该模板则在前面加上 ?。**

