---
title: Gdb多线程调试
date: 2021-09-03T20:51:41+08:00
lastmod: 2021-09-03T20:51:41+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - gdb
  - 编程
  - 多线程
# nolastmod: true
draft: false
---

* `info threads` 显示当前可调试的所有线程，每个线程会有一个GDB为其分配的ID，后面操作线程的时候会用到这个ID。 前面有*的是当前调试的线程。
* `thread ID` 切换当前调试的线程为指定ID的线程。
* `break thread_test.c:123 thread all` 在所有线程中相应的行上设置断点
* `thread apply ID1 ID2 command` 让一个或者多个线程执行GDB命令command。 
* `thread apply all command` 让所有被调试线程执行GDB命令command。
* `set scheduler-locking off|on|step` 估计是实际使用过多线程调试的人都可以发现，在使用step或者continue命令调试当前被调试线程的时候，其他线程也是同时执行的，怎么只让被调试程序执行呢？通过这个命令就可以实现这个需求。off 不锁定任何线程，也就是所有线程都执行，这是默认值。 on 只有当前被调试程序会执行。 step 在单步的时候，除了next过一个函数的情况(熟悉情况的人可能知道，这其实是一个设置断点然后continue的行为)以外，只有当前线程会执行。

