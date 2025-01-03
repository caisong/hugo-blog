---
title: Makefile通用模板
date: 2022-09-23T21:41:09+08:00
lastmod: 2022-09-23T21:41:09+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 编程
tags:
  - makefile
# nolastmod: true
draft: false
---

简单makefile套用模板

```shell
# 编译当前文件夹下的所有cpp文件
CC=g++ -std=c++11
objects := $(patsubst %.cpp,%.o,$(wildcard *.cpp))
target := $(basename $(objects))

all: $(target)

$(target): $(objects)
        $(CC) -o $@ $@.o

$(objects): %.o: %.cpp
        $(CC) -c $(CLFAGS) $< -o $@

.PHONY : clean
clean:
        rm $(target) $(objects)
```

```shell
CC=g++ -std=c++11
target := $(patsubst %.cpp,%,$(wildcard *.cpp))
all: $(target)
clean:
	rm $(target)
```
