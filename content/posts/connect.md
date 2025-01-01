---
title: Connect
date: 2021-09-03T21:41:57+08:00
lastmod: 2021-09-03T21:41:57+08:00
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
## connect
```c
 int cfd = SAFE_SOCKET(remote_addrinfo->ai_family,                         
                         remote_addrinfo->ai_socktype, 0);                                                         
                                                                                                   
        tst_res(TINFO, "server_addr:%s %s", server_addr, iface);                                                   
                                                                                                                   
        iface = strchr(server_addr, '%');                        
                                                                                                                   
        tst_res(TINFO, "server_addr:%s %s", server_addr, iface);
                                                                   
        if(iface) {                                               
                        iface++;                                            
        }                                                                   
        else                                                    
        {                                                                  
                        iface = getenv("LHOST_IFACES");                        
        }                                                                  
        tst_res(TINFO, "IFACES NAME %s", iface);                               
                                                                               
        if(iface)                                                          
        {                                                                      
                        if(AF_INET6 == remote_addrinfo->ai_family)
                        {                                         
                                        ifr.ifr_addr.sa_family = AF_INET;
                                        strncpy(ifr.ifr_name , iface , IFNAMSIZ-1);
                                                                                   
                                        if(0 == ioctl(cfd, SIOCGIFINDEX, &ifr))    
                                        {                                          
                                                        ifindex = ifr.ifr_ifindex; 
                                                        tst_res(TINFO, "IFACES INDEX %d", ifindex);
                                        }                                                          
                                        ((struct sockaddr_in6 *)remote_addrinfo->ai_addr)->sin6_scope_id = ifindex;
                        }                                                                                          
        }          
```                                                     

Tags:
  c, snippet