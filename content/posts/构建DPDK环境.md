---
title: 构建DPDK环境
date: 2024-10-09T21:41:46+08:00
lastmod: 2024-10-09T21:41:46+08:00
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
# 构建DPDK环境  
```dockerfile
FROM ccr.ccs.tencentyun.com/library/centos:latest

LABEL RUN docker run -it --privileged -v /sys/bus/pci/drivers:/sys/bus/pci/drivers -v /sys/kernel/mm/hugepages:/sys/kernel/mm/hugepages -v /sys/devices/system/node:/sys/devices/system/node -v /dev:/dev --name NAME -e NAME=NAME -e IMAGE=IMAGE IMAGE"

WORKDIR /root

COPY ./dpdk-23.11.1.tar.xz ./libpcap-1.10.4.tar.xz dpdk-kmods-linux.tar.gz pktgen-dpdk-pktgen-24.05.5.tar.gz /root

# repo

RUN sed -e "s|^mirrorlist=|#mirrorlist=|g" -e "s|^#baseurl=http://mirror.centos.org/\$contentdir/\$releasever|baseurl=http://mirror.nju.edu.cn/centos-vault/8.5.2111|g" -i.bak /etc/yum.repos.d/CentOS-*.repo

RUN dnf makecache && dnf install epel-release -y

RUN sed -e 's!^metalink=!#metalink=!g' \
        -e 's!^#baseurl=!baseurl=!g' \
        -e 's!https\?://download\.fedoraproject\.org/pub/epel!http://mirror.nju.edu.cn/epel!g' \
        -e 's!https\?://download\.example/pub/epel!http://mirror.nju.edu.cn/epel!g' \
        -i /etc/yum.repos.d/epel{,-testing}.repo && dnf makecache

RUN dnf install python39 python39-pyelftools -y && python3 -m pip install -i https://mirrors.cernet.edu.cn/pypi/web/simple --upgrade pip && pip config set global.index-url https://mirrors.cernet.edu.cn/pypi/web/simple && pip install ninja meson

RUN dnf install bison flex gcc make autoconf numactl-devel openssl openssl-devel libatomic-devel libatomic zlib-devel libbsd-devel which -y
RUN tar xvf libpcap-1.10.4.tar.xz && cd libpcap-1.10.4 && ./configure && make && make install

WORKDIR /root

RUN tar xvf dpdk-23.11.1.tar.xz && cd dpdk-stable-23.11.1 && meson build && ninja -C build && ninja -C build install && export PKG_CONFIG_PATH=/usr/local/lib64/pkgconfig && ldconfig

WORKDIR /root

RUN tar xvf pktgen-dpdk-pktgen-24.05.5.tar.gz  && cd pktgen-dpdk-pktgen-24.05.5 && sed -i "168s/%l'd/%d/" app/pktgen-port-cfg.c && meson build && ninja -C build && ninja -C build install

CMD [" /sbin/init"]
```