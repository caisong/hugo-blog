---
title: ovs-dpdk验证
date: 2021-09-23T21:40:43+08:00
lastmod: 2021-09-23T21:40:43+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - dpdk
tags:
  - open vswitch
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# dpdk 验证
ubuntu 环境验证较简单
[Using Docker* Containers with Open vSwitch* and DPDK on Ubuntu* 17.10](https://software.intel.com/content/www/us/en/develop/articles/using-docker-containers-with-open-vswitch-and-dpdk-on-ubuntu-1710.html)  
以下内容暂不涉及**docker**

```bash
sudo apt install openvswitch-switch-dpdk
# 好像ubunt默认自带了一个openvswitch，不带dpdk 的，此处需要更新下
sudo update-alternatives --set ovs-vswitchd /usr/lib/openvswitch-switch
-dpdk/ovs-vswitchd-dpdk
sudo systemctl restart openvswitch-switch.service

# 设置2M的大页内存，太小了启动不了。。。。
echo 256 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages

# 设置完毕后直接使用dpdk-hugepage.py的脚本设置大页内存
dpdk-hugepages.py -p 2M --setup 512M

# 加载 mod
apt install dpdk-kmods-dkms
modprobe uio
modprobe igb_uio

# 查看序号
dpdk-debind.py -s 

# 绑定网卡
dpdk-devbind.py --bind=igb_uio 0000:00:08.0

# 启动ovs-dpdk
/usr/share/openvswitch/scripts/ovs-ctl start

# 设置openvswitch参数
# 此处好像是数据库
ovs-vsctl --no-wait set Open_vSwitch . other_config:dpdk-init=true

 # 清除删除，remove比较难用，直接clear 
 # ovs-vsctl clear Open_vSwitch . other_config

# 设置预分配内存大小，默认值过大起不来，改小点，单位M
ovs-vsctl --no-wait set Open_vSwitch . other_config:dpdk-socket-mem="128"

# 可以设置dpdk-lcore-mask，虚拟机没那么多核心，设备的值如何配置也没搞清，暂不设置
# ovs-vsctl --no-wait set Open_vSwitch . other_config:pmd-cpu-mask=0x2

# 创建一个支持 dpdk 的网桥
ovs-vsctl add-br ovs-br0 -- set bridge ovs-br0 datapath_type=netdev

# 创建 dpdk 接口并绑定到物理网卡
ovs-vsctl add-port ovs-br0 dpdkprot01 -- set Interface dpdkprot01 type=dpdk options:dpdk-devargs=0000:00:08.0

# 创建 dpdk vhost-user 接口
ovs-vsctl add-port ovs-br0 vhost-user0 -- set Interface vhost-user0 type=dpdkvhostuser
ovs-vsctl add-port ovs-br0 vhost-user1 -- set Interface vhost-user1 type=dpdkvhostuser

# 创建流表
ovs-ofctl add-flow ovs-br0 in_port=1,idle_timeout=0,action=output:2
ovs-ofctl add-flow ovs-br0 in_port=2,idle_timeout=0,action=output:1
```
[Running Containers With OVS-DPDK](https://www.cnblogs.com/dream397/p/13964154.html "ovs-dpdk")

目前操作成功了，但是据体作用不清楚

- [ ] vhostuser、viritio-user
- [x] testpmd作用
- [ ] port br作用
- [ ] 流表查看、验证（testpmd）
