---
title: Tpm Env
date: 2017-05-21T17:44:32+08:00
lastmod: 2017-05-21T17:44:32+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - tpm
  - shell
# nolastmod: true
draft: false
---

tpm使用相关命令

<!--more-->

## tpm emulator
```shell
# init tpm emulator
tpmd deactivated
killall tpmd
tpmd clear
# start tpm emulator
modprobe tpmd_dev
# 如果遇到问题，使用tpmd -f -d clear启动
tpmd -f -d 
```

一直出现
tpmd.c:310: Debug: waiting for connections...
表示成功了

### 常见问题对策
  1. module tpmd_dev not found
  ```shell
  depmod -a 
  ```

  2. failed: address alread in use
  ```shell
  rm /var/run/tpm/tpmd_socket:0
  ```

## trousers
```shell
#　must start tpm emlator beftor star tcsd
tcsd -e -f
```
出现TCSD trousers 0.3.13: TCSD up and running.

## openCryptoki [optional]
if you want to install tpmtoken_* command, you shoud install it

## tpm-tools
```shell
tpm_selftest
```

## tpmtoken manual
use tpm_takeownership
tpmtoken_init (需要`ld  /usr/lib/opencryptoki/stdll/libpkcs11_sw.so`)
