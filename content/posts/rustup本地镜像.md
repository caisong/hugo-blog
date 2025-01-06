---
title: windows romt构建rustup本地镜像
date: 2024-10-09T21:41:30+08:00
lastmod: 2024-10-09T21:41:30+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - rustup
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

基于外部工具`romt`实现的,不过最终也没成功。。。。。

```cmd
# 下载toolchain
e:\romt-0.4.0-x86_64-windows.exe toolchain -v -s stable -t x86_64-pc-windows-gnu --url https://mirror.nju.edu.cn/rustup/dist --no-signature download

#下载rustup
# nju镜像路径不同，ustc镜像一样的
e:\romt-0.4.0-x86_64-windows.exe toolchain -v -s stable -t x86_64-pc-windows-gnu --url https://mirror.nju.edu.cn/rustup/rustup --no-signature download
# rustup缺少校验文件，直接下载后放对应目录

# create mirror
# 不使用镜像速度比较慢
e:\romt-0.4.0-x86_64-windows.exe crate init --index-url https://mirror.nju.edu.cn/git/crates.io-index.git

#同步
e:\romt-0.4.0-x86_64-windows.exe crate -v --keep-going --index-url https://mirror.nju.edu.cn/git/crates.io-index.git update 


E:\mirror>e:\romt-0.4.0-x86_64-windows.exe crate -v --keep-going --index-url https://mirror.nju.edu.cn/git/crates.io-index.git --crates-url https://mirror.nju.edu.cn/git/crates.io-index.git/ --assume-ok --bundle-path=e:\mirror\crates.tar.gz
```

````powershell
# 打包
# rustup缺少256文件，powershell执行
Get-FileHash -Algorithm SHA256 -Path .\rustup-init.exe|out-file -Encoding ASCII .\rustup-init.exe.sha256

romt rustup -v -s stable -t x86_64-pc-windows-gnu --assume-ok pack


# toolchains缺少asc文件，直接no-signature
romt toolchain -v -s stable -t x86_64-pc-windows-gnu --no-signature pack
```
