---
title: Lisp
date: 2021-09-03T21:42:01+08:00
lastmod: 2021-09-03T21:42:01+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - lisp
tags:
  - emacs
  - tag2
# nolastmod: true
draft: false
---

忘记干啥的，先留着吧

```lisp
(setq backup-directory-alist '(("." . "~/.emacs.d/backup"))
  backup-by-copying t    ; Don't delink hardlinks
  version-control t      ; Use version numbers on backups
  delete-old-versions t  ; Automatically delete excess backups
  kept-new-versions 20   ; how many of the newest versions to keep
  kept-old-versions 5    ; and how many of the old
  )
```