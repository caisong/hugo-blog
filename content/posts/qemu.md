---
title: Qemu
date: 2024-10-09T21:41:23+08:00
lastmod: 2024-10-09T21:41:23+08:00
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
# qemu

[qemu wiki](https://wiki.alpinelinux.org/wiki/QEMU)

```bash
qemu-img create -f qcow2 alpine.qcow2 8G

qemu-system-x86_64 -m 512 -nic user -boot d -cdrom alpine-standard-3.20.3-x86_64.iso -hda alpine.qcow2 -display gtk -enable-kvm


qemu-system-aarch64 -m 2048 -cpu cortex-a57 -smp 2 -M virt -bios QEMU_EFI.fd -nographic -drive if=none,file=ubuntu-16.04.3-server-arm64.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=ubuntu16.04-arm64.img,id=hd0 -device virtio-blk-device,drive=hd0


qemu-system-aarch64 -m 1024 -cpu cortex-a57 -smp 2 -M virt -bios /usr/share/AAVMF/AAVMF_CODE.fd -nographic -drive if=none,file=/opt/os/CentOS-7-aarch64-Minimal-2009.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=/var/lib/libvirt/images/test.img,id=hd0 -device virtio-blk-device,drive=hd0

qemu-system-arm -m 1024 -cpu cortex-a15 -M virt -bios /usr/share/AAVMF/AAVMF_CODE.fd -nographic -drive if=none,file=/root/CentOS-7-aarch64-Minimal-2009.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=/root/centos-arm.img,id=hd0 -device virtio-blk-device,drive=hd0

qemu-system-arm -m 1024 -cpu cortex-a15 -M virt -bios /usr/share/AAVMF/AAVMF_CODE.fd -nographic -drive if=none,file=/root/CentOS-7-aarch64-Minimal-2009.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=/root/centos-arm.img,id=hd0 -device virtio-blk-device,drive=hd0

qemu-system-aarch64 \
    -m 4096M -cpu cortex-a57 -M virt \
    -bios QEMU_EFI.fd \
    -localtime -serial telnet::4444,server -nographic \
    -drive if=none,file=./qcow2.img,id=hd0 \
    -device virtio-blk-device,drive=hd0 \
    -device virtio-net-device,vlan=0,id=net0,mac=52:54:00:09:a4:37 \
    -net user,vlan=0,name=hostnet0 \
    -redir tcp:40022::22
```

Tags:
  qe, qemu