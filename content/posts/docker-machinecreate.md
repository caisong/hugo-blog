---
title: Docker Machinecreate
date: 2024-10-09T21:40:41+08:00
lastmod: 2024-10-09T21:40:41+08:00
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
# docker-machine create
```shell
docker-machine create --engine-registry-mirror=http://hub-mirror.c.163.com --engine-opt -d virtualbox default
```

# docker user&passwd
| username | passwd | how to enter |
|:--|:--|--|
| docker | tcuser | ssh |
| root |  | sudo -i (under docker user) |
| docker |  | docker-machine ssh <machine-name> |

# docker container gdb problem
> warning: Error disabling address space randomization: Operation not permitted

```shell
  docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined
```

Tags:
  docker, windows