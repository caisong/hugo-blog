---
title: PXELiveCD
date: 2024-05-22T21:41:19+08:00
lastmod: 2024-05-22T21:41:19+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - PXE
  - tag2
# nolastmod: true
draft: false
---

基于linux live cd 镜像，使用pxe批量安装

## 主要流程
** 个人理解，不一定准确 **
1. 使用DHCP 引导入PXE
2. PXE 使用tftp 引导syslinux？
3. 加载nfs或http的系统

# virtualbox环境配置
主要就是必须保证pxe server 和client在同一网段。（dhcp支持replay的忽略）
pxe server 使用两张网卡，一张nat用于下载包，一张内部网络
pxe client 使用一张网卡，使用内部网络。
也可以使用host-only模式，但是要关闭dhcp服务，因为pxe server要作为dhcp服务引导pxe。

## 注意事项  
1. 关闭防火墙  
```bash
systemctl stop firewalld
```

2. 禁用selinux
```bash
setenforce 0
```

## 部署流程
1. 安装tftp
**tftp支持xinet.d启动和systemctl启动，只能用一个，建议`systemctl`**  
```bash
dnf install tftp-server
# tftp-server 路径挂载在/var/lib/tftpboot，服务路径使用systemctl status查看
```

pxe相关内容安装至tftp挂载路径
```bash
# 这个包直接建syslinux相关内容放在/tftpboot目录下了（出现过直接放在/var/lib/tftpboot的，自己查看下。最终都要拷贝到自己的挂载路径。）
dnf install syslinux-tftpboot
```

2. 安装dhcp
`dhcp`是引导pxe的关键，其实如果客户端使用ipxe，也能不使用`dhcp`，目前还有`uefi`的方式，暂未研究。
不用使用dnsmasq，没配置出来。
```bash
dnf install dhcpd
```

```conf
allow bootp;
allow booting;
max-lease-time 1200;
default-lease-time 900;
log-facility local7;

option ip-forwarding    false;
option mask-supplier    false;
#192.168.10.1 pxe server的ip
   subnet 192.168.10.0 netmask 255.255.255.0 {
       option  routers   192.168.10.1;
       option  domain-name-servers  127.0.0.1;
       range 192.168.10.100 192.168.10.200;
       next-server 192.168.10.1;
       filename "pxelinux.0";
   }
```

3. 安装httpd或nfs
```bash
dnf install httpd nfs-utils
```
httpd默认root目录是/var/www/html
想偷懒的，直接将iso镜像挂载到该目录。

nfs的配置在 /etc/exports
```conf
#直接配置挂载目录
/centos *(ro,sync,no_root_squash)
```

4. PXE配置
dhcp 中配置了直接调用pxelinux.0，该文件调用pxelinux.cfg/default。default中配置的就是远程加载的目录。
```conf
#  一般如下，但是centos livecd不支持直接远端启动，需要使用工具改造。ubuntu 好像可以。
LABEL CentOS 6.8 LiveCD
MENU LABEL CentOS 6.8 Live CD
KERNEL linux/centos-6.8/live/isolinux/vmlinuz0 rdshell
APPEND initrd=linux/centos-6.8/live/isolinux/initrd0.img boot=live fetch=tftp://192.168.1.1/linux/centos-6.8/live/LiveOS/squashfs.img root=/dev/ram0 ramdisk_size=10000000 ip=dhcp
```

5. 适配
```bash
dnf install livecd-tools
livecd-iso-to-pxeboot  <iospath>
```

以上命令会产生tftpboot目录，直接盖你自己的tftpboot就行。这个命令将镜像内容都加载到了initrd.img文件中，这样导致pxe启动比较慢。

centos无法远端启动就是因为 initrd0.img文件中没有livenet 、squash，可以将这两个module加进去。
```bash
# 判断方法
dracut --list-modules /export/uefi/LiveDisklessRamfs.img | grep livenet
dracut --list-modules /export/uefi/LiveDisklessRamfs.img | grep squash

#  以下两条都没试过，后期试过了再更新
# dracut -N --nomdadmconf --nolvmconf --xz --add-fstab /tinkeredOSStructure/etc/fstab --tmpdir /mytmpspace --logfile /mytempspace/MakeInitRamfs.log --force-add "nfs network base dmsquash-live livenet kernel-modules uefi-lib rootfs-block" /mytmpspace/LiveDisklessRamfs.img 3.10.0-327.36.3.el7.x86_64

# 新增方法
#i40e igb 是网卡驱动
 dracut -N --nomdadmconf --nolvmconf --xz -d "i40e igb" --filesystems "ext4" --force-add "nfs network base dnsquash-live livenet kernel-modules uefi-lib rootfs-block" initrd0.img

6. ipxe启动
正常dhcp能分配IP就能启动了。
不使用dhcp，可以使用ipxe.iso镜像，直接配置IP地址，chain 命令启动。


## 总结
1. Linux启动流程还是了解太少
2. 有问题先检查selinux和防火墙
3. 了解方案原理，才能更好的排查问题

## TODO
如何制作启动时执行指定命令的LiveCD镜像
