---
title: ltp telnet测试错误
date: 2021-09-03T21:41:35+08:00
lastmod: 2021-09-03T21:41:35+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - LTP
tags:
  - telnet
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
root telnet登录失败

`tail -20 /var/log/secure`日志如下：

```plain
Apr 24 17:32:58 localhost login: pam_securetty(remote:auth): access denied: tty 'pts/1' is not secure !
Apr 24 17:33:03 localhost login: FAILED LOGIN 1 FROM localhost FOR root, Authentication failure
```
**access denied: tty 'pts/1' is not secure !**

方法一：所以将‘pts/1’添加到/etc/securetty中，即可实现telnet的root用户登录。

方法二：修改/etc/pam.d/remote，注释掉：auth       required     pam_securetty.so
```plain
1 #%PAM-1.0
2 #auth       required     pam_securetty.so
3 auth       include      system-auth
```

