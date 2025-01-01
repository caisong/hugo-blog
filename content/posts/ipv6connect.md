---
title: Ipv6connect
date: 2021-09-03T21:42:16+08:00
lastmod: 2021-09-03T21:42:16+08:00
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
ipv6 connect 

connect(7, {sa_family=AF_INET6, sin6_port=htons(80), inet_pton(AF_INET6,
>     "fe80::21f:16ff:fe1a:f5b8", &sin6_addr), sin6_flowinfo=0, sin6_scope_id=0},
>     28) = -1 EINVAL (Invalid argument)


      struct sockaddr_in6 sin6;
       . . .
      sin6.sin6_family = AF_INET6;
      sin6.sin6_flowinfo = 0;
      sin6.sin6_port = htons(23);
      sin6.sin6_addr = in6addr_loopback;  /* structure assignment */
       . . .
      if (connect(s, (struct sockaddr *) &sin6, sizeof(sin6)) == -1)


# 获取网卡信息
	struct ifreq ifr;
	char *iface = "eth0";
	unsigned char *mac;
	
	fd = socket(AF_INET, SOCK_DGRAM, 0);

	ifr.ifr_addr.sa_family = AF_INET;
	strncpy(ifr.ifr_name , iface , IFNAMSIZ-1);

	ioctl(fd, SIOCGIFHWADDR, &ifr);

		if (AF_INET6 == remote_addrinfo->ai_family) {
			((struct sockaddr_in6 *)remote_addrinfo->ai_addr)->sin6_scope_id = 2;
		}



```c
if_nametoindex
```

Tags:
  ipv6, linux