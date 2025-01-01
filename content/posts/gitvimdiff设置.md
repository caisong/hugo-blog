---
title: Gitvimdiff设置
date: 2024-12-10T21:40:50+08:00
lastmod: 2024-12-10T21:40:50+08:00
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
# git vimdiff设置
```bash
git config diff.tool vimdiff
git config diftool.vimdiff.cmd=vim -d $LOCAL $REMOTE

git config alias.df difftool
git config alias.st status
```

# git crlf 设置  
```bash
// 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true   

// 提交时转换为LF，检出时不转换
git config --global core.autocrlf input   

// 提交检出均不转换
git config --global core.autocrlf false


// 拒绝提交包含混合换行符的文件 （一般设置为true）
git config --global core.safecrlf true   

// 允许提交包含混合换行符的文件
git config --global core.safecrlf false   

// 提交包含混合换行符的文件时给出警告
git config --global core.safecrlf warn

```