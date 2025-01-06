---
title: Wireshark编译、打包
date: 2021-09-03T21:41:40+08:00
lastmod: 2021-09-03T21:41:40+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - wireshark
tags:
  - wireshark
# nolastmod: true
draft: false
---

**构建wireshark发布包，必须先生成user guide,并下载以下软件**

* htmlhelp （微软官网已经下不到了，直接百度找个）
* nsis 发布exe包用的
```bat
rem wireshark源码路径
set WIRESHARK_BASE_DIR=E:\code
rem QT编译库路径
set QT5_BASE_DIR=D:\Qt\5.15.2\msvc2019_64
rem 编译目录
cd E:\code\wsbuild64
cmake -G "Visual Studio 16 2019" -A x64 ..\wireshark
rem wirehsark vs工程文件
msbuild /m /p:Configuration=RelWithDebInfo Wireshark.sln
rem set PATH="%PATH%;E:\code\wsbuild64\run\RelwithDebInfo"

rem wirehark user guide 项目
msbuild /p:Configuration=RelWithDebInfo .\docbook\user_guide_chm.vcxproj

rem 构建发布包
msbuild /m /p:Configuration=RelWithDebInfo nsis_package_prep.vcxproj

msbuild /m /p:Configuration=RelWithDebInfo nsis_package.vcxproj
```
