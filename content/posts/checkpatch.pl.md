---
title: Checkpatch.pl
date: 2021-09-03T20:42:08+08:00
lastmod: 2021-09-03T20:42:08+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - checkpatch.pl
# nolastmod: true
draft: false
---

$ ./checkpatch.pl --no-tree -f sample_module.c

```shell
# ignore file mode
git config --global core.filemode false
git config --global core.filemode false
```

1. git rebase -i xxxxxx
2. change pick --> edit
3. git commit --amend -s --author " "
4. git rebase --continue


```shell
#openssl cross compile
 ./Configure --openssldir=/home/<your user>/workbench/openssl-1.0.1g/final shared os/compiler:arm-none-linux-gnueabi-
```

