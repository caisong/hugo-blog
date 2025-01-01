---
title: Rsyslogmmnormalizemodule
date: 2024-12-24T21:41:27+08:00
lastmod: 2024-12-24T21:41:27+08:00
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
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# rsyslog mmnormalize module

## 相关语法
### 规则语法
```config
rule=[<tag1>[,<tag2>...]]:<match description>
# match descirption 可以出现N次
match description=<string literals><field selectors>
# extra data是根据field type类型决定的
fileld selectors=%<field name>:<field type>[:<extra data>]%
```

### filed type
mmnormalize版本2的语法没有使用正则，内置了一套字段类型，与正则差不多。
* number:  数字
    %field_name:number% === [0-9]+
* word:  到空格或者行末截止
    %field_name:word% ===  \S+
* alpha:   up to the next whitespace, punctuation, decimal digit or ctrl
    %field_name:alpha% === \w+
* char-to: 表示直到某个字符
    %field_name:char-to:,% === [^,]+
* char-sp: 表示直到某个字符，可以空。
    %field_name:char-sep:,% === [^,]*
* rest：一直匹配到行结束
* quoted-string: 匹配双引号中的内容
* date-iso ： YYYY-MM-DD格式日期
* time-24hr： HH:MM:SS 24小时制时间
* time-12hr： HH:MM:SS 12小时制时间
* ipv4: 点分制ipv4地址
* date-rfc3164： Oct 29 09:47:08 格式日期
* date-rfc5424：1985-04-12T19:20:50.52-04:00 格式日期
* iptables：匹配Name=value，空格分隔的kv对
    %-:iptables% 不使用字段名，匹配内容中的name替代字段名


### 前置规则
```config
# 设置前缀，可复用
prefix=<match description>
# 取消前缀
prefix=
```
### 引用
mmnormalize匹配的内容都在`$!`命名空间内，可通过`$!field_name`引用

### 示例
```config
# Prefix sample:
# myhostname: code=23
prefix=%host:char-to:\x3a%: 
rule=prefixed_code:code=%code:number%
# myhostname: name=somename
rule=prefixed_name:name=%name:word%
# Reset prefix to default (empty value):
prefix=
```


