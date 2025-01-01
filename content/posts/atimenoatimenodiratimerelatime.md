---
title: Atimenoatimenodiratimerelatime
date: 2021-09-03T21:41:56+08:00
lastmod: 2021-09-03T21:41:56+08:00
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
## atime/noatime/nodiratime/relatime
- atime(缺省) - 每次读取档案/目录内容时，更新档案/目录 inode 上的最后存取时间 (access time)
- noatime - 不会更新档案 inode 上的最后存取时间。可以大大减轻档案系统的负荷，但会令如 mutt 之类需要存取时间的应用程序不能正常运作。
- nodiratime - 不会更新目录 inode 上的最后存取时间
- relatime - 每次读取档案/目录内容时，只在档案/目录 inode 上原先的最后存取时间旧于最后修改时间 (modify time) 或更新时间 (change time) 才更新最后存取时间。可以减少对档案系统的负荷，但不影响如 mutt 之类需要存取时间的应用程序。Linux 2.6.20 开始支援


Tags:
  linux