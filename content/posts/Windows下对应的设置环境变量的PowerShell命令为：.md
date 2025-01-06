---
title: PowerShell 设置环境变量
date: 2023-12-27T21:42:28+08:00
lastmod: 2023-12-27T21:42:28+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - windows
tags:
  - powershell
# nolastmod: true
draft: false
---

一般cmd命令行设置环境变量使用`set`, 但是在powershell环境下不生效，特地查询了下，记录于此。
Windows 下对应的设置环境变量的 PowerShell 命令为：
```powershell
$env:RUSTUP_DIST_SERVER="https://mirror.nju.edu.cn/rustup"
$env:RUSTUP_UPDATE_ROOT="https://mirror.nju.edu.cn/rustup/rustup"
```

