---
title: Ubuntuqemuarm
date: 2024-10-10T21:41:38+08:00
lastmod: 2024-10-10T21:41:38+08:00
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
# ubuntu qemu arm

```bash
#  检验CPU是否支持
grep -E --color '(vmx|svm)' /proc/cpuinfo

# 安装qemu
sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virtinst libvirt-daemon

# 启动
sudo systemctl enable --now libvirtd
sudo systemctl start libvirtd

# 添加用户至相关组(否则virt-manager无权限)
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
sudo usermod -aG libvirt-qemu $USER

# 安装virt-manager（图形界面，可选）
sudo adduser $USER libvirt
sudo apt install virt-manager

# 重新登陆后使用
```

# 创建空镜像文件
```bash
qemu-img create -f qcow2 centos-arm.qcow2 20G
```

# qemu-efi下载
[QEMU_EFI.fd](https://releases.linaro.org/reference-platform/enterprise/17.12/uefi/release/qemu-aarch64/QEMU_EFI.fd)

[QEMu EFI fd 2](https://releases.linaro.org/components/kernel/uefi-linaro/16.02/release/qemu64/QEMU_EFI.fd)

# 使用ISO文件创建系统镜像
```bash
qemu-system-aarch64 -m 2048 -cpu cortex-a57 -smp 2 -M virt -bios /usr/share/qemu-efi-aarch64/QEMU_EFI.fd -nographic -drive if=none,file=CentOS-7-aarch64-Minimal-2009.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=centos-arm.qcow2,id=hd0 -device virtio-blk-device,drive=hd0 -net nic -net user,hostfwd=tcp::2222-:22
```

# 直接启动
```bash
qemu-system-aarch64 -m 2048 -cpu cortex-a57 -smp 2 -M virt -bios /usr/share/qemu-efi-aarch64/QEMU_EFI.fd -nographic -device virtio-scsi-device -drive if=none,file=centos-arm.qcow2,id=hd0 -device virtio-blk-device,drive=hd0
```

Tags:
  qemu