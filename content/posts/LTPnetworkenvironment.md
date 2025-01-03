---
title: LTP network environment
date: 2021-09-03T21:41:08+08:00
lastmod: 2021-09-03T21:41:08+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - LTP 
tags:
  - LTP
# nolastmod: true
draft: false
---
LTP 网络相关测试集环境配置

## client(debian) 

```shell
sudo apt-get install rsh-server nfs-kernel-server fingerd
echo $client_hostname >> /root/.rhosts

/sbin/restorecon -v /root/.rhosts  [optional] (sudo apt-get install policycoreutils)

for i in rlogin rsh rexec; do echo $i >> /etc/securetty; done

export RHOST=$SERVER_HOSTNAME
export PASSWD=$ROOT_PASSWD
```



## server(ubuntu)

```shell
sudo apt-get install rsh-server telnetd cfingerd rdist rsync udhcpd lighttpd nfs-kernel-server
echo $client_hostname >> /root/.rhosts

/sbin/restorecon -v /root/.rhosts  [optional] (sudo apt-get install policycoreutils)

for i in rlogin rsh rexec; do echo $i >> /etc/securetty; done

vim /etc/ftpusers

# comment line containing "root" string
export RHOST=$CLIENT_HOSTNAME
export PASSWD=$ROOT_PASSWD
```



# network test

```shell
export PATH=/opt/ltp/testcases/bin:/usr/bin:$PATH

export LHOST_HWADDRS='00:0c:29:f8:7d:01'
export RHOST_HWADDRS='00:0c:29:ce:b3:2f'

export LHOST_IFACES='eth0'
export RHOST_IFACES='ens33'

export IPV4_NETWORK="192.168.30"
export LHOST_IPV4_HOST=130
export RHOST_IPV4_HOST=134

export LTP_RSH=${LTP_RSH:-"rsh -n"}
LTP_RSH=${LTP_RSH:-"rsh -n"}
export LTP_RSH="$LTP_RSH"

export LHOST_IPV6_HOST="fef8:7d01"
export RHOST_IPV6_HOST="fece:b32f"

export IPV6_NETWORK="fe80::20c:29ff"

export NS_DURATION=60

```