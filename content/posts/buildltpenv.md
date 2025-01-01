---
title: Buildltpenv
date: 2021-09-03T21:40:30+08:00
lastmod: 2021-09-03T21:40:30+08:00
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
# build ltp env

## build server env
1. comile LTP on server
```shell
make autotools
# --prefix={ltp target path}
./configure
make
make install
```

2. build server test env
   1. necessary software
   ```shell
   sudo apt-get install telnetd cfingerd rdist rsync udhcpd lightttpd xinetd nfs-kernel-server rpcbind
   ```
   2. build xinetd env
   ```shell
   bash xinet_config
   ```

   3. build rsh env
   ```shell
   echo rsh >>/etc/securetty
   echo rlogin >>/etc/securetty
   echo rexec >>/etc/securetty
   echo telnet >>/etc/securetty

   for i in $(seq 10); do
   echo tty$i >> /etc/securetty
   done

   echo "dragonboard-410c root" >> ~/.rhosts
   # replace with real ip of db410c
   echo "192.168.10.35 dragonboard-410c" >> /etc/hosts
   ```

   4. build ssh env [optional]
   ```shell
   # client
   ssh-keygen -t rsa -N ""  -f /home/root/.ssh/id_rsa

   # server
   scp root@dragonboard-410c:/home/root/.ssh/id_ras.pub db410c.pub
   cat  db410c.pub >> ~/.ssh/authorized_keys
   ```

   5. start services
   ```shell
   sudo systemctl restart rpcbind
   sudo systemctl restart nfs-kernel-server
   sudo systemctl restart xinetd
   ```

   6. copy additional software to db410c
   ```shell
   # caisong@10.167.218.57:~/db410c_env/mini
   rsync -avz `ls` --chown root:root root@192.168.10.35:/
   # caisong@10.167.218.57:~/db410c_env/full
   rsync -avz `ls` --chown root:root root@192.168.10.35:/app2
   ```

## build db410c env
1. syslog
   ```shell
   touch /var/log/messages
   echo 'OPTIONS="-O /var/log/messages"' >> /etc/default/busybox-syslog
   systemctl restart syslog
   ```

2. mount disk
    ```shell
    # db410c must unplug sd card and plug sd card agagin when booting
    mkdir /app /app2 /root
    # please replace to your disk
    mount /dev/mmcblk1p1 /app
    mount /dev/mmcblk1p2 /tmp
    mount /dev/mmcblk1p3 /app2
    mkswap /dev/mmcblk1p5 && swapon /dev/mmcblk1p5
    ```

3. build boot env
    ```shell
    # current boot env is on 10.167.218.57
    rsync -avz caisong@10.167.218.57:~/db410c_env/mini/* --chown root:root /
    rsync -avz caisong@10.167.218.57:~/db410c_env/full/* --chown root:root /app2/
    ```

4. env parameter
    ```shell
    # profile
    echo "export PATH=\$PATH:/app2/usr/bin:/app2/usr/local/bin:/app2/etc/:/app2/sbin:/app2/usr/sbin" >> /etc/profile
    PATH=$PATH:/app2/usr/bin:/app2/usr/local/bin:/app2/etc/'

    # rlogin required
    ln -sf /app2/usr/lib/tcl8.6 /usr/lib
    ```

5. ip setting on boot
    ```shell
    # replace 192.168.10.35 to your ip
    cat > /opt/setipaddr.sh << "EOF" &&
    #! /bin/sh
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/bin:/opt/:$PATH
    ifconfig eth0 192.168.10.35 up
    EOF

    cat > /etc/systemd/system/setipaddr.service << "EOF" &&
    [Unit]
    Description=set ip on boot
    After=network.target

    [Service]
    Type=oneshot
    ExecStart=/opt/setipaddr.sh

    [Install]
    WantedBy=multi-user.target
    EOF

    (cd /etc/systemd/system/ && systemctl enable setipaddr && systemctl start setipaddr)
    ```

6. hostname
    ```shell
    # add server hostname
    echo "192.168.10.31 debian" >> /etc/hosts
    ```

7. add ftp user
    ```shell
    useradd -d /var/ftp -m -s /usr/sbin/nologin ftp
    chmod a-w /var/ftp
    ```

8. ssh env
    ```shell
    [-f /home/root/.ssh/id_rsa ] || ssh-keygen -t rsa -N ""  -f /home/root/.ssh/id_rsa
    ```

9. xinetd

    ```shell
    bash xinet_config
    systemctl start xinetd
    ```

10. some services
    ```shell
    systemctl daemon-reload
    systemctl restart rpcbind
    systemctl restart crond
    ```

11. compile LTP
    ```shell
    # please set same prefix as server if you did
    ./configure
    make
    make install
    ```


Tags:
  ltp