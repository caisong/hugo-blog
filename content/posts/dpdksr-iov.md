---
title: Dpdksr Iov
date: 2024-12-30T21:40:42+08:00
lastmod: 2024-12-30T21:40:42+08:00
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
# dpdk sr-iov
## 检查网卡是否支持
```bash
ifconfig
ethtool -i <nic>
lspci -vs <pci>
```
支持的网卡，`lspci`会展示以下信息:
```plain
capabilities: [160] Single Root I/O Virtualization (SR-IOV)
```

## 开启sr-iov
```bash
# 1. 开机启动
grubby --args="intel_iommu=on iommu=pt" --update-kernel DEFAULT
# 2. 加载module
modprobe <nic_module>
modprobe iavf
modprobe vfio
# 3. 设置vf数量
cat /sys/class/net/<nic name>/device/sriov_totalvfs
echo 4 > /sys/class/net/<nic name>/device/sriov_numvfs
# 4.开启网卡特性
# 开启vf混杂模式
ethtool --set-priv-flags oct1 vf-true-promisc-support on

# vf相关设置
#设置vf一直在线，默认继承pf在线状态
ip link set <pf nic name>  vf <vf num> state enable
ip link set <pf nic name>  vf <vf num> trust on
ip link set <pf nic name>  vf <vf num> spoofchk off

#设置vf mac地址
ip link set <pf nic name> vf <vf num> mac <mac addr>
```

## 容器映射
```bash
docker run -itd --privileged -v /sys/buc/pci/devices:/sys/bus/pci/devices -v /dev:/dev centos;7 /sbin/init
```
