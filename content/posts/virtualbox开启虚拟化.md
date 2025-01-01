---
title: Virtualbox开启虚拟化
date: 2024-10-09T21:41:39+08:00
lastmod: 2024-10-09T21:41:39+08:00
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
# virtualbox开启虚拟化
```bash
F:\VirtualBox>VBoxManage.exe list vms
"rhel64" {240f96d8-6535-431d-892e-b70f3dc464e8}

F:\VirtualBox>VBoxManage.exe modifyvm "rhel64" --nested-hw-virt on
```