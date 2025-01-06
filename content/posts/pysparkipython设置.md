---
title: Pyspark ipython 设置
date: 2024-01-12T21:41:20+08:00
lastmod: 2024-01-12T21:41:20+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - python
tags:
  - spark
  - ipython
# nolastmod: true
draft: false
---

```shell
export JAVA_HOME="具体路径"
export SPARK_HOME="具体路径"
export PYSPARK_DRIVER_PYTHON=ipython3
source ${venv}/bin/active
source ${SPARK_HOME}/bin/pyspark
```