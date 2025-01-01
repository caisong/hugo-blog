---
title: Sony隐藏虚拟按键
date: 2021-09-03T20:58:14+08:00
lastmod: 2021-09-03T20:58:14+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - phone
tags:
  - phone
  - sony xp
# nolastmod: true
draft: true
---

```shell
# 隐藏
 adb shell settings put global policy_control immersive.navigation=*
#恢复
 adb shell settings put global policy_control null
```

