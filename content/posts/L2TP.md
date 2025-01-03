---
title: L2TP部署
date: 2022-09-28T21:41:05+08:00
lastmod: 2022-09-28T21:41:05+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - l2tp
# nolastmod: true
draft: false
---

## L2TP服务端

1. 内核加载`modprobe af_key`
2. 配置文件
```shell
cat > vpn.env << EOF
VPN_IPSEC_PSK=random
VPN_USER=caisong
VPN_PASSWORD=123456
EOF
```

3. l2tp容器
```shell
# 容器内通信，不需要对外连接
docker run --name l2tp-vpn-server --env-file ./vpn.env -p 500:500/udp -p 4500:4500/udp -v /lib/modules:/lib/modules:ro -d --privileged hwdsl2/ipsec-vpn-server
```

## L2TP客户端
1. centos基础镜像
```shell
# 必须挂载module，容器里没有
docker run -itd -v /lib/modules:/lib/modules:ro --privileged centos:8 /sbin/init
```
2. 客户端配置
```shell
# 容器镜像不带这些module，安装软件会有依赖。直接先把依赖的module安装完成后，再这个镜像基础上再安装l2tp客户端
dnf install xl2tpd

VPN_SERVER_IP=random 
VPN_IPSEC_PSK=172.17.0.2 
VPN_USERNAME=caisong
VPN_PASSWORD=123456
```
* `/etc/xl2tpd/xl2tpd.conf`
```shell
cat > /etc/xl2tpd/xl2tpd.conf <<EOF
[lac myvpn]
lns = $VPN_SERVER_IP
ppp debug = yes
pppoptfile = /etc/ppp/options.l2tpd.client
length bit = yes
EOF
```
* `/etc/ppp/options.l2tpd.client`
```shell
cat > /etc/ppp/options.l2tpd.client <<EOF
ipcp-accept-local
ipcp-accept-remote
refuse-eap
require-chap
noccp
noauth
mtu 1280
mru 1280
noipdefault
defaultroute
usepeerdns
connect-delay 5000
name $VPN_USER
password $VPN_PASSWORD
EOF
```

* Create xl2tpd control file:
```shell
mkdir -p /var/run/xl2tpd
touch /var/run/xl2tpd/l2tp-control
systemctl start xl2tpd  
```