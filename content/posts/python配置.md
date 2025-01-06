---
title: pip配置、命令
date: 2021-09-03T21:41:21+08:00
lastmod: 2021-09-03T21:41:21+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - python
tags:
  - pip
# nolastmod: true
draft: false
---

## 镜像配置

```shell
# windows 路径 C:\Users\username\pip\pip.ini
# linux  路径 ~/.pip/pip.conf 

[global]
index-url = https://mirrors.aliyun.com/pypi/simple/
```

## pip 命令
pip list --outdated #列出所有过期的库
pip install --upgrade 库名 #升级库

## 一键升级过期源
```python
import pip
from subprocess import call
 
for dist in pip.get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)
```

