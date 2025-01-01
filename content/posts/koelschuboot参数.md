---
title: Koelschuboot参数
date: 2021-09-03T21:41:04+08:00
lastmod: 2021-09-03T21:41:04+08:00
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
# koelsch uboot参数
## init env
```shell
setenv ethaddr 2e:09:0a:00:6c:e1
setenv ipaddr 192.168.10.5
setenv serverip 192.168.10.2
```
## bootcmd
```shell
# zImage
setenv bootcmd 'tftp 0x40007fc0 zImage;tftp 0x40f00000 r8a7791-koelsch.dtb;bootz 0x40007fc0 - 0x40f00000'

# uImage
setenv bootcmd 'tftp 0x40007fc0 uImage;tftp 0x40f00000 r8a7791-koelsch.dtb;bootm 0x40007fc0 - 0x40f00000'
```

## bootargs
```shell
# nfs
setenv bootargs 'console=ttySC6,38400 vmalloc=384M ip=192.168.10.5 root=/dev/nfs nfsroot=192.168.10.2:/opt/koelsch'

# sd
setenv bootargs 'console=ttySC6,38400 vmalloc=384M root=/dev/mmcblk0p1'
```

## optional
```shell
#kernel 写入flash
setenv bootcmd 'tftp 0x40007fc0 zImage;tftp 0x40f00000 r8a7791-koelsch.dtb;bootz 0x40007fc0 - 0x40f00000'
tftpboot 0x41000000 r8a7791-koelsch.dtb
sf probe
sf erase 0x100000 0x40000
sf write 0x41000000 0x100000 0x40000
setenv bootargs 'console=ttySC6,38400 vmalloc=384M ip=192.168.10.5 root=/dev/nfs nfsroot=192.168.10.2:/opt/koelsch'
tftpboot 0x41000000 zImage

# 0x340000 - 内核大小256向上取整
setenv kern_size 0x340000
sf probe
sf erase 0x140000 ${kern_size}
sf write 0x41000000 0x140000 ${kern_size}
setenv bootcmd 'sf probe;sf read 0x40007fc0 0x140000 ${kern_size};sf read 0x40f00000 0x100000 0x40000;bootz 0x40007fc0 - 0x40f00000'
saveenv
```


Tags:
  koelsch