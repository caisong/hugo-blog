---
title: Windows移植linux
date: 2017-10-29T20:13:54+08:00
lastmod: 2017-10-29T20:13:54+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - linux
tags:
  - linux
  - windows
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

## 数据层

### 数据库驱动
详细内容见《PostgreSQL调查》
数据库连接方式可以使用UnixODBC（ODBC驱动）或libpq（原生驱动）两种方式
| 类型   | unixODBC | libpq |
| :--- | :------: | :---: |
| 优点   |  代码改动小   | 查询效率高 |
| 缺点   |   效率较低   | 代码改动大 |

### 连接池
* 官方推荐的pgpoll-Ⅱ、pgbouncer第三方连接池。易于扩展、方便部署。
* 使用长连接建立简单的连接池。  

## 网络层

网络Epoll模型
客户端代码  
```c
/*
 * =====================================================================================
 *
 *       Filename:  client.c
 *
 *    Description:  client example
 *
 *        Version:  1.0
 *        Created:  11/10/2016 11:03:37 PM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */

#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <fcntl.h>
#include <unistd.h>

/*
 * ===  FUNCTION  ======================================================================
 *         Name:  main
 *  Description:
 * =====================================================================================
 */
#define MAXLINE 4096
int main(int argc, char *argv[])
{
	struct sockaddr_in servaddr;
	const char *servIP = "192.168.220.128";
	int sockfd;
	char sendLine[MAXLINE] = {0};
	char recvLine[MAXLINE] = {0};
	int rec_len = 0;

	if ((sockfd = socket(AF_INET, SOCK_STREAM, 0)) < 0)
	{
		printf("create socket error:%s (errno: %d )\n", strerror(errno), errno);
		exit(0);
	}

	memset(&servaddr, 0, sizeof(servaddr));
	servaddr.sin_family = AF_INET;
	servaddr.sin_port = htons(43388);
	if (inet_pton(AF_INET, servIP, &servaddr.sin_addr) <= 0)
	{
		printf("inet_pton error for %s\n", servIP);
	}

	if (connect(sockfd, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0)
	{
		printf("connect error :%s (errno: %d)", strerror(errno), errno);
	}

	printf("send message to server\n");
	while (1)
	{
		fgets(sendLine, 4096, stdin);
		if (send(sockfd, sendLine, strlen(sendLine), 0) < 0)
		{
			printf("send msg error:%s, (errno :%d)\n", strerror(errno), errno);
			exit(0);
		}
		if ((rec_len = recv(sockfd, recvLine, MAXLINE, 0)) == -1)
		{
			perror("recv error");
			exit(0);
		}
		recvLine[rec_len] = '\0';
		printf("server :%s \n", recvLine);
	}
	close(sockfd);
	printf("client offline\n");
	exit(0);
} /* ----------  end of function main  ---------- */
```

服务器端代码

```c
/*
 * =====================================================================================
 *
 *       Filename:  epollEx.c
 *
 *    Description:  epoll example
 *
 *        Version:  1.0
 *        Created:  11/10/2016 10:15:10 PM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/epoll.h>
#include <errno.h>

#define MAXEVENTS 64
struct data_send
{
	int fd;
	char *buff;
	int len;
	int flag;
};

static int make_socket_non_blocking(int sfd)
{
	int flags, s;

	flags = fcntl(sfd, F_GETFL, 0);
	if (flags == -1)
	{
		perror("fcntl");
		return -1;
	}

	flags |= O_NONBLOCK;
	s = fcntl(sfd, F_SETFL, flags);
	if (s == -1)
	{
		perror("fcntl");
		return -1;
	}

	return 0;
}

static int create_and_bind(char *port)
{
	struct addrinfo hints;
	struct addrinfo *result, *rp;
	int s, sfd;

	memset(&hints, 0, sizeof(struct addrinfo));
	hints.ai_family = AF_UNSPEC;     /* Return IPv4 and IPv6 choices */
	hints.ai_socktype = SOCK_STREAM; /* We want a TCP socket */
	hints.ai_flags = AI_PASSIVE;     /* All interfaces */

	s = getaddrinfo(NULL, port, &hints, &result);
	if (s != 0)
	{
		fprintf(stderr, "getaddrinfo: %s\n", gai_strerror(s));
		return -1;
	}

	for (rp = result; rp != NULL; rp = rp->ai_next)
	{
		sfd = socket(rp->ai_family, rp->ai_socktype, rp->ai_protocol);
		if (sfd == -1) continue;

		s = bind(sfd, rp->ai_addr, rp->ai_addrlen);
		if (s == 0)
		{
			/* We managed to bind successfully! */
			break;
		}

		close(sfd);
	}

	if (rp == NULL)
	{
		fprintf(stderr, "Could not bind\n");
		return -1;
	}

	freeaddrinfo(result);

	return sfd;
}

int main(int argc, char *argv[])
{
	int sfd, s;
	int efd;
	struct data_send *data;
	struct epoll_event event;
	struct epoll_event *events;

	//if (argc != 2)
	//{
	//    fprintf(stderr, "Usage: %s [port]\n", argv[0]);
	//    exit(EXIT_FAILURE);
	//}

	sfd = create_and_bind("43388");
	if (sfd == -1) abort();

	s = make_socket_non_blocking(sfd);
	if (s == -1) abort();

	s = listen(sfd, SOMAXCONN);
	if (s == -1)
	{
		perror("listen");
		abort();
	}

	efd = epoll_create1(0);
	if (efd == -1)
	{
		perror("epoll_create");
		abort();
	}

	event.data.fd = sfd;
	event.events = EPOLLIN | EPOLLET;
	s = epoll_ctl(efd, EPOLL_CTL_ADD, sfd, &event);
	if (s == -1)
	{
		perror("epoll_ctl");
		abort();
	}

	/* Buffer where events are returned */
	events = calloc(MAXEVENTS, sizeof event);

	/* The event loop */
	while (1)
	{
		int n, i;

		n = epoll_wait(efd, events, MAXEVENTS, -1);
		for (i = 0; i < n; i++)
		{
			if ((events[i].events & EPOLLERR) || (events[i].events & EPOLLHUP) ||
				(!(events[i].events & EPOLLIN || events[i].events & EPOLLOUT)))
			{
				/* An error has occured on this fd, or the socket is not
				   ready for reading (why were we notified then?) */
				fprintf(stderr, "epoll error\n");
				close(events[i].data.fd);
				continue;
			}

			else if (sfd == events[i].data.fd)
			{
				/* We have a notification on the listening socket, which
				   means one or more incoming connections. */
				while (1)
				{
					struct sockaddr in_addr;
					socklen_t in_len;
					int infd;
					char hbuf[NI_MAXHOST], sbuf[NI_MAXSERV];

					in_len = sizeof in_addr;
					infd = accept(sfd, &in_addr, &in_len);
					if (infd == -1)
					{
						if ((errno == EAGAIN) || (errno == EWOULDBLOCK))
						{
							/* We have processed all incoming
							   connections. */
							break;
						}
						else
						{
							perror("accept");
							break;
						}
					}

					s = getnameinfo(&in_addr, in_len, hbuf, sizeof hbuf, sbuf, sizeof sbuf,
									NI_NUMERICHOST | NI_NUMERICSERV);
					if (s == 0)
					{
						printf(
							"Accepted connection on descriptor %d "
							"(host=%s, port=%s)\n",
							infd, hbuf, sbuf);
					}

					/* Make the incoming socket non-blocking and add it to the
					   list of fds to monitor. */
					s = make_socket_non_blocking(infd);
					if (s == -1) abort();

					event.data.fd = infd;
					event.events = EPOLLIN | EPOLLET;
					s = epoll_ctl(efd, EPOLL_CTL_ADD, infd, &event);
					if (s == -1)
					{
						perror("epoll_ctl");
						abort();
					}
				}
				continue;
			}
			else if (events[i].events & EPOLLIN)
			{
				/* We have data on the fd waiting to be read. Read and
				   display it. We must read whatever data is available
				   completely, as we are running in edge-triggered mode
				   and won't get a notification again for the samen
				   data. */
				int fd = 0;
				while (1)
				{
					ssize_t count;
					char buf[512] = {0};
					fd = events[i].data.fd;
					count = read(fd, buf, sizeof buf);
					if (count == -1)
					{
						/* If errno == EAGAIN, that means we have read all
						   data. So go back to the main loop. */
						if (errno != EAGAIN)
						{
							perror("read");
						}
						break;
					}
					else if (count == 0)
					{
						/* End of file. The remote has closed the
						   connection. */
						break;
					}

					/* Write the buffer to standard output */
					// strcpy(recv, "client: ");
					// strcat(recv, buf);
					// s = write(1, recv, strlen(recv));
					// if (s == -1)
					//{
					//    perror("write");
					//    abort();
					//}
					// strcpy(buf, "hello, client");
					// write(events[i].data.fd, buf, strlen(buf));

					write(STDOUT_FILENO, buf, strlen(buf));
				}
				data = (struct data_send *)malloc(sizeof(struct data_send));
				memset(data, 0, sizeof(struct data_send));
				data->fd = fd;
				event.data.ptr = data;
				event.events = EPOLLOUT | EPOLLET;
				s = epoll_ctl(efd, EPOLL_CTL_MOD, fd, &event);
				if (s == -1)
				{
					perror("epoll_ctl");
					abort();
				}
				data->buff = malloc(64);
				strcpy(data->buff, "hello");
				data->len = strlen(data->buff);
			}
			else if (events[i].events & EPOLLOUT)
			{
				struct data_send *to_send = (struct data_send *)events[i].data.ptr;
				write(to_send->fd, to_send->buff, to_send->len);
				if (to_send->flag != 0)
				{
					close(to_send->fd);
				}
				else
				{
					event.data.fd = to_send->fd;
					event.events = EPOLLIN | EPOLLET;
					s = epoll_ctl(efd, EPOLL_CTL_MOD, to_send->fd, &event);
					if (s == -1)
					{
						perror("epoll_ctl");
						abort();
					}
				}
			}
		}
	}

	free(events);

	close(sfd);

	return EXIT_SUCCESS;
}
```



## 应用逻辑层

### Windows平台相关的变量声明

HANDLE 包括线程和数据库相关的变量，需要一一对应。其余的可以直接替换或`typedef`重定义。
`typedef unsinged long DWORD`

### Windows服务 --> Linux服务

编写相关Shell文件
```bash
#!/bin/bash
#description: example 
export ORACLE_SID=orcl
export ORACLE_PID=`ps -ef|grep ora|grep -E 'smon|pmon|ckpt'|wc -l`
export ORACLE_BASE=/u01/app
export ORACLE_HOME=/u01/app/oracle
export PATH=$PATH:$ORACLE_HOME/bin
ORA_OWNR="oracle"
if [ ! -f $ORACLE_HOME/bin/dbstart -o ! -d $ORACLE_HOME ]
   then
   echo "Oracle startup:can't start"
   exit 1
fi
case "$1" in
  start)
  echo -n "Starting Oracle:"
  su - $ORA_OWNR -c "$ORACLE_HOME/bin/dbstart"
  echo "OK"
  ;;
  stop)
  echo -n "Shutdown Oracle:"
  su - $ORA_OWNR -c "$ORACLE_HOME/bin/dbshut"
  echo "OK"
  ;;
  status)
  if [ $ORACLE_PID = "3" ];then
     echo "Oracle Instance is running..."
  else echo "Oracle Instance is not running..."
  fi
  ;;
  restart)
  $0 stop
  $0 start
  ;;
  *)
  echo "Usage:`basename $0` start|stop|status|restart"
esac
exit $?
```

### Windows网络库相关 --> Linux Socket

客户端代码
```c
​```cpp
/*
 * =====================================================================================
 *
 *       Filename:  client.c
 *
 *    Description:  client example
 *
 *        Version:  1.0
 *        Created:  11/10/2016 11:03:37 PM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */

#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <fcntl.h>
#include <unistd.h>

/*
 * ===  FUNCTION  ======================================================================
 *         Name:  main
 *  Description:
 * =====================================================================================
 */
#define MAXLINE 4096
int main(int argc, char *argv[])
{
	struct sockaddr_in servaddr;
	const char *servIP = "192.168.220.128";
	int sockfd;
	char sendLine[MAXLINE] = {0};
	char recvLine[MAXLINE] = {0};
	int rec_len = 0;

	if ((sockfd = socket(AF_INET, SOCK_STREAM, 0)) < 0)
	{
		printf("create socket error:%s (errno: %d )\n", strerror(errno), errno);
		exit(0);
	}

	memset(&servaddr, 0, sizeof(servaddr));
	servaddr.sin_family = AF_INET;
	servaddr.sin_port = htons(43388);
	if (inet_pton(AF_INET, servIP, &servaddr.sin_addr) <= 0)
	{
		printf("inet_pton error for %s\n", servIP);
	}

	if (connect(sockfd, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0)
	{
		printf("connect error :%s (errno: %d)", strerror(errno), errno);
	}

	printf("send message to server\n");
	while (1)
	{
		fgets(sendLine, 4096, stdin);
		if (send(sockfd, sendLine, strlen(sendLine), 0) < 0)
		{
			printf("send msg error:%s, (errno :%d)\n", strerror(errno), errno);
			exit(0);
		}
		if ((rec_len = recv(sockfd, recvLine, MAXLINE, 0)) == -1)
		{
			perror("recv error");
			exit(0);
		}
		recvLine[rec_len] = '\0';
		printf("server :%s \n", recvLine);
	}
	close(sockfd);
	printf("client offline\n");
	exit(0);
} /* ----------  end of function main  ---------- */
```

服务器端代码

```cpp
/*
 * =====================================================================================
 *
 *       Filename:  epollEx.c
 *
 *    Description:  epoll example
 *
 *        Version:  1.0
 *        Created:  11/10/2016 10:15:10 PM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/epoll.h>
#include <errno.h>

#define MAXEVENTS 64
struct data_send
{
	int fd;
	char *buff;
	int len;
	int flag;
};

static int make_socket_non_blocking(int sfd)
{
	int flags, s;

	flags = fcntl(sfd, F_GETFL, 0);
	if (flags == -1)
	{
		perror("fcntl");
		return -1;
	}

	flags |= O_NONBLOCK;
	s = fcntl(sfd, F_SETFL, flags);
	if (s == -1)
	{
		perror("fcntl");
		return -1;
	}

	return 0;
}

static int create_and_bind(char *port)
{
	struct addrinfo hints;
	struct addrinfo *result, *rp;
	int s, sfd;

	memset(&hints, 0, sizeof(struct addrinfo));
	hints.ai_family = AF_UNSPEC;     /* Return IPv4 and IPv6 choices */
	hints.ai_socktype = SOCK_STREAM; /* We want a TCP socket */
	hints.ai_flags = AI_PASSIVE;     /* All interfaces */

	s = getaddrinfo(NULL, port, &hints, &result);
	if (s != 0)
	{
		fprintf(stderr, "getaddrinfo: %s\n", gai_strerror(s));
		return -1;
	}

	for (rp = result; rp != NULL; rp = rp->ai_next)
	{
		sfd = socket(rp->ai_family, rp->ai_socktype, rp->ai_protocol);
		if (sfd == -1) continue;

		s = bind(sfd, rp->ai_addr, rp->ai_addrlen);
		if (s == 0)
		{
			/* We managed to bind successfully! */
			break;
		}

		close(sfd);
	}

	if (rp == NULL)
	{
		fprintf(stderr, "Could not bind\n");
		return -1;
	}

	freeaddrinfo(result);

	return sfd;
}

int main(int argc, char *argv[])
{
	int sfd, s;
	int efd;
	struct data_send *data;
	struct epoll_event event;
	struct epoll_event *events;

	//if (argc != 2)
	//{
	//    fprintf(stderr, "Usage: %s [port]\n", argv[0]);
	//    exit(EXIT_FAILURE);
	//}

	sfd = create_and_bind("43388");
	if (sfd == -1) abort();

	s = make_socket_non_blocking(sfd);
	if (s == -1) abort();

	s = listen(sfd, SOMAXCONN);
	if (s == -1)
	{
		perror("listen");
		abort();
	}

	efd = epoll_create1(0);
	if (efd == -1)
	{
		perror("epoll_create");
		abort();
	}

	event.data.fd = sfd;
	event.events = EPOLLIN | EPOLLET;
	s = epoll_ctl(efd, EPOLL_CTL_ADD, sfd, &event);
	if (s == -1)
	{
		perror("epoll_ctl");
		abort();
	}

	/* Buffer where events are returned */
	events = calloc(MAXEVENTS, sizeof event);

	/* The event loop */
	while (1)
	{
		int n, i;

		n = epoll_wait(efd, events, MAXEVENTS, -1);
		for (i = 0; i < n; i++)
		{
			if ((events[i].events & EPOLLERR) || (events[i].events & EPOLLHUP) ||
				(!(events[i].events & EPOLLIN || events[i].events & EPOLLOUT)))
			{
				/* An error has occured on this fd, or the socket is not
				   ready for reading (why were we notified then?) */
				fprintf(stderr, "epoll error\n");
				close(events[i].data.fd);
				continue;
			}

			else if (sfd == events[i].data.fd)
			{
				/* We have a notification on the listening socket, which
				   means one or more incoming connections. */
				while (1)
				{
					struct sockaddr in_addr;
					socklen_t in_len;
					int infd;
					char hbuf[NI_MAXHOST], sbuf[NI_MAXSERV];

					in_len = sizeof in_addr;
					infd = accept(sfd, &in_addr, &in_len);
					if (infd == -1)
					{
						if ((errno == EAGAIN) || (errno == EWOULDBLOCK))
						{
							/* We have processed all incoming
							   connections. */
							break;
						}
						else
						{
							perror("accept");
							break;
						}
					}

					s = getnameinfo(&in_addr, in_len, hbuf, sizeof hbuf, sbuf, sizeof sbuf,
									NI_NUMERICHOST | NI_NUMERICSERV);
					if (s == 0)
					{
						printf(
							"Accepted connection on descriptor %d "
							"(host=%s, port=%s)\n",
							infd, hbuf, sbuf);
					}

					/* Make the incoming socket non-blocking and add it to the
					   list of fds to monitor. */
					s = make_socket_non_blocking(infd);
					if (s == -1) abort();

					event.data.fd = infd;
					event.events = EPOLLIN | EPOLLET;
					s = epoll_ctl(efd, EPOLL_CTL_ADD, infd, &event);
					if (s == -1)
					{
						perror("epoll_ctl");
						abort();
					}
				}
				continue;
			}
			else if (events[i].events & EPOLLIN)
			{
				/* We have data on the fd waiting to be read. Read and
				   display it. We must read whatever data is available
				   completely, as we are running in edge-triggered mode
				   and won't get a notification again for the same
				   data. */
				int fd = 0;
				while (1)
				{
					ssize_t count;
					char buf[512] = {0};
					fd = events[i].data.fd;
					count = read(fd, buf, sizeof buf);
					if (count == -1)
					{
						/* If errno == EAGAIN, that means we have read all
						   data. So go back to the main loop. */
						if (errno != EAGAIN)
						{
							perror("read");
						}
						break;
					}
					else if (count == 0)
					{
						/* End of file. The remote has closed the
						   connection. */
						break;
					}

					/* Write the buffer to standard output */
					// strcpy(recv, "client: ");
					// strcat(recv, buf);
					// s = write(1, recv, strlen(recv));
					// if (s == -1)
					//{
					//    perror("write");
					//    abort();
					//}
					// strcpy(buf, "hello, client");
					// write(events[i].data.fd, buf, strlen(buf));

					write(STDOUT_FILENO, buf, strlen(buf));
				}
				data = (struct data_send *)malloc(sizeof(struct data_send));
				memset(data, 0, sizeof(struct data_send));
				data->fd = fd;
				event.data.ptr = data;
				event.events = EPOLLOUT | EPOLLET;
				s = epoll_ctl(efd, EPOLL_CTL_MOD, fd, &event);
				if (s == -1)
				{
					perror("epoll_ctl");
					abort();
				}
				data->buff = malloc(64);
				strcpy(data->buff, "hello");
				data->len = strlen(data->buff);
			}
			else if (events[i].events & EPOLLOUT)
			{
				struct data_send *to_send = (struct data_send *)events[i].data.ptr;
				write(to_send->fd, to_send->buff, to_send->len);
				if (to_send->flag != 0)
				{
					close(to_send->fd);
				}
				else
				{
					event.data.fd = to_send->fd;
					event.events = EPOLLIN | EPOLLET;
					s = epoll_ctl(efd, EPOLL_CTL_MOD, to_send->fd, &event);
					if (s == -1)
					{
						perror("epoll_ctl");
						abort();
					}
				}
			}
		}
	}

	free(events);

	close(sfd);

	return EXIT_SUCCESS;
}
```

### 配置文件及xml文件解析

目前使用windows系统函数解析ini文件，之前发布的Linux版中间件中ini解析对gcc版本要求太高，目前Centos 7 不支持。
可选方案：
目前使用多次读取ini文件的方式，按需获取配置文件中相关信息。Linux平台下ini文件解析器可以使用开源库`iniparser`或自己实现。使用xml方式定义配置文件，文件结构清晰，仅加载一次配置文件实现整体解析，开源库众多，如`libxml2`,`tinyxml`等，且**分析业务中获取地址需要解析xml格式内容**
| 类型   |  ini   |   xml    |
| :--- | :----: | :------: |
| 优点   | 代码改动量小 | 结构清晰，效率高 |
| 缺点   |  效率低   |  代码改动大   |
部分xml配置文件示例
```xml
<root>
    <server kind="1" port="43388"/>
    <wifi enable="false"/>
    <companycode/>
    <filePath>
        <path type="carsettingmanagement" value="carsettingmanagement"/>
        <path type="parameter" value="parameterset"/>
        <path type="outdata" value="DataFile"/>
        <path type="difffile" value="DiffFile"/>
        <path type="userfile" value="UserFile"/>
        <path type="carlog" value="CarLogFile"/>
    </filePath>
    <DBInfo>
        <info type="connDBInfo" addr="10.167.218.27"userName="sa" password="Sa123456" dbName="INFOMANAGEMENT_DB"/>
        <info type="V1DB" addr="10.167.218.27"userName="sa" password="Sa123456" dbName="INFOMANAGEMENT_DB"/>
    </DBInfo>
    <CarFirmCheck>
        <version>31030101</version>
        <version>21030413</version>
        <version>32030108</version>
    </CarFirmCheck>
</root>
```

### 文件相关

| windows                           | Linux                               |
| :-------------------------------- | :---------------------------------- |
| CreateFile                        | open                                |
| DeleteFile                        | remove                              |
| ReadFile                          | read                                |
| WriteFile                         | write                               |
| CreateDirectory<br/>FindFirstFile | kdir<br/>opendir<br/>closedir<dir/> |
| GetFileSize<br/>GetFileTime       | fstat                               |
| GetModuleFileName                 | getcwd<br/>                         |
| GetFirstFile                      | file_exists                         |
| CloseHandle                       | close                               |
| SetFilePointer                    | lseek                               |

### Eslc压缩库

目前使用的是dll库，需要日方提供Linux版本
动态库调用
| Windows        | Linux   |
| :------------- | :------ |
| LoadLibrary    | dlopen  |
| GetProcAddress | dlsym   |
| FreeLibrary    | dlclose |
|                | dlerror |

### 日志

日志配置文件
支持日志分级、文件输出、格式定义等常见功能。

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE log4c SYSTEM "">

<log4c version="1.2.4">

	<config>
		<bufsize>0</bufsize>
		<debug level="0"/>
		<nocleanup>1</nocleanup>
		<reread>1</reread>
	</config>

	<category name="root" priority="notice"/>
	<category name="myapp" priority="debug" appender="myfile" />
	<appender name="myfile" type="rollingfile" logdir="." prefix="commdl" layout="dated" rollingpolicy="myrollingpolicy" />
	<rollingpolicy name="myrollingpolicy" type="sizewin" maxsize="1024000" maxnum="10" />
	<layout name="dated" type="dated"/>
</log4c>
```
使用示例

```c
/*
 * =====================================================================================
 *
 *       Filename:  logTest.c
 *
 *    Description:  log4c example
 *
 *        Version:  1.0
 *        Created:  11/10/2016 12:16:45 AM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */
#ifdef HAVE_CONFIG_H
#include "config.h"
#endif

#include <stdio.h>

#include "log4c.h"

int main(int argc, char** argv)
{
	int rc = 0;
	log4c_category_t* mycat = NULL;

	if (log4c_init())
	{
		printf("log4c_init() failed");
		rc = 1;
	}
	else
	{
		mycat = log4c_category_get("myapp");
		log4c_category_log(mycat, LOG4C_PRIORITY_ERROR, "Hello World!");

		/* Explicitly call the log4c cleanup routine */
		if (log4c_fini())
		{
			printf("log4c_fini() failed");
		}
	}
	return rc;
}
```


### windows共享内存

| Windows            | Linux      | Classification |
| :----------------- | :--------- | :------------- |
| CreateFileMaping() | shm_open() | Context        |
| MapViewOfFile()    | mmap()     | Context        |
| UnampViewOfFile()  | munmap()   | Context        |


### 线程 事件 互斥量 临界区 信号量

进程映射
| Windows                                  | Linux                                    | Classification |
| :--------------------------------------- | :--------------------------------------- | :------------- |
| CreateProcess()<br/>CreateProcessAsUser() | fork()<br/>setuid()<br/>exec()<br/>      | Mappable       |
| TerminateProcess()                       | kill()                                   | Mappable       |
| SetThreadpriority()<br/>GetThreadPriority()<br/> | setPriority()<br/>getPriority()          | Mappable       |
| GetCurrentProcessID()                    | getpid()                                 | Mappable       |
| Exitprocess()                            | exit()                                   | Mappable       |
| Waitforsingleobject()<br/>Waitformultipleobject()<br/>GetExitCodeProcess() | waitpid()<br/>Using sys V semaphores, waitforsingleobject/multiobject<br/>不能实现 | Context        |
| GetEnvironmentVariable<br/>SetEnvironmentVariable | getenv()<br/>setenv()                    | Mappable       |
线程映射  
| Windows                                | Linux                                    | Classification |
| :------------------------------------- | :--------------------------------------- | :------------- |
| CreateThread                           | pthread_create<br/>pthread_attr_init<br/>pthread_attr_setstacksize<br/>pthread_attr_destory | Mappable       |
| ThreadExit                             | pthread_exit                             | Mappable       |
| WaitForSingleObject                    | pthread_join<br/>pthread_attr_setdetachstate<br/>pthread_detach | Mappable       |
| SetpriorityClass<br/>SetThreadPriority | setpriority<br/>sched_setscheduler</br>sched_setparam<br><br>pthread_setschedparam<br>pthread_setschedpolicy<br>pthread_attr_setschedparam<br>pthread_attr_setschedpolicy | Context        |
事件
| Windows                   | Linux(thread)                            | Linux(process)    | Classification   |
| :------------------------ | :--------------------------------------- | :---------------- | :--------------- |
| CreateEvent<br/>OpenEvent | pthread_cond_init<br/>sem_init<br/>      | semget<br/>semctl | Context specific |
| SetEvent                  | pthread_cond_signal<br/>sem_post         | semop             | Context specific |
| ResetEvent                | N/A                                      | N/A               | Context specific |
| WaifForSingleobject       | pthread_cond_wait<br/>pthread_cond_timedwait<br/>sem_wait<br/>sem_trywait | semop             | Context specific |
| CloseHandle               | pthread_cond_destory<br/>sem_destroy     | semctl            | Context specific |
互斥量
| Windows                | Linux(thread)                            | Linux(process)    | Classification   |
| :--------------------- | :--------------------------------------- | :---------------- | :--------------- |
| CreateMutex            | pthreads_mutex_init                      | semget<br/>semctl | Context specific |
| OpenMutex              | N/A                                      | semget            | Context specific |
| WaifForSingleObject    | pthread_mutex_lock<br/>pthread_mutex_unlock | semop             | Context specific |
| ReleaseMutex           | pthread_mutex_unlock                     | semop             | Context specific |
| CloseHandle            | pthread_mutex_destroy                    | semctl            | Context specific |
| SignalObjectAndWait    | semop                                    | semop             | Context specific |
| WaitForMultipleObjects | sem_wait<br>sem_trywait                  | semop             | Context specific |
临界区
| Windows                                  | Linux                                    | Classification |
| :--------------------------------------- | :--------------------------------------- | :------------- |
| InitializeCriticalSection<br>InitializeCriticalSectionAndSpinCount | pthreads_mutex_init                      | Mappable       |
| EnterCriticalSection<br/>TryEnterCriticalSection | pthread_mutex_lock<br> pthread_mutex_trylock | Mappable       |
| LeaveCriticalSection                     | pthread_mutex_unlock                     | Mappable       |
| DeleteCriticalSection                    | pthread_mutex_destroy                    | Mappable       |
信号量
| Windows             | Linux(thread)           | Linux(process)   | Classification   |
| :------------------ | :---------------------- | :--------------- | :--------------- |
| CreateSemaphore     | sem_init                | semget<br>semctl | Context specific |
| OpenSemaphore       | N/A                     | semget           | Context specific |
| WaitForSingleObject | sem_wait<br>sem_trywait | semop            | Context specific |
| ReleaseSemaphore    | sem_post                | semop            | Context specific |
| CloseHandle         | sem_destroy             | semctl           | Context specific |
线程相关Example
```c
	/*
	 * =====================================================================================
	 *
	 *       Filename:  shmExample.c
	 *
	 *    Description:  shared memeory example
	 *
	 *        Version:  1.0
	 *        Created:  11/10/2016 01:33:33 AM
	 *       Revision:  none
	 *       Compiler:  gcc
	 *
	 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
	 *        Company:
	 *
	 * =====================================================================================
	 */

	#include <sys/mman.h>
	#include <sys/stat.h>
	#include <fcntl.h>

	#include <stdlib.h>
	#include <stdio.h>

	/*
	 * ===  FUNCTION  ======================================================================
	 *         Name:  main
	 *  Description:
	 * =====================================================================================
	 */
	#define FILE_MODE (S_IRUSR | S_IWUSR | S_IRGRP | S_IROTH)
	#define SHM_NAME "myshm"
	pthread_mutex_t mutex;
	pthread_cond_t cond;

	void shm_write()
	{
		int i, fd;
		struct stat stat;
		unsigned char *ptr;
		printf("write thread acquire lock\r\n");
		pthread_mutex_lock(&mutex);
		printf("write thread get lock\r\n");
		fd = shm_open(SHM_NAME, O_RDWR, FILE_MODE);
		fstat(fd, &stat);
		ptr = mmap(NULL, stat.st_size, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
		close(fd);
		for (i = 0; i < stat.st_size; ++i)
		{
			*ptr++ = i % 256;
		}
		printf("write thread release lock\r\n");
		pthread_mutex_unlock(&mutex);
		printf("write thread signal cond\r\n");
		pthread_cond_signal(&cond);
	}

	void shm_read()
	{
		int i, fd;
		struct stat stat;
		unsigned char c, *ptr;
		printf("read thread acquire lock\r\n");
		pthread_mutex_lock(&mutex);
		printf("read release lock\r\n");
		pthread_cond_wait(&cond, &mutex);
		printf("read cond satisfy\r\n");
		fd = shm_open(SHM_NAME, O_RDONLY, FILE_MODE);
		fstat(fd, &stat);
		ptr = mmap(NULL, stat.st_size, PROT_READ, MAP_SHARED, fd, 0);
		close(fd);
		for (i = 0; i < stat.st_size; ++i)
		{
			if ((c = *ptr++) != i % 256)
			{
				// fprintf(stderr, "ptr[%d] = %d\r\n", i, c);
				pthread_mutex_unlock(&mutex);
				return;
			}
			/*  else
			{
				fprintf(stdout, "ptr[%d] = %d\r\n", i, c);
				}*/
		}
		fprintf(stdout, "ptr[100] = %d\r\n", *(ptr+100));
		pthread_mutex_unlock(&mutex);
		printf("exit\r\n");
	}

	int main(int argc, char *argv[])
	{
		int fd;
		int flags;
		off_t length;
		char *ptr;
		pthread_t pt1, pt2;
		flags = O_RDWR | O_CREAT;
		length = 1024;
		fd = shm_open(SHM_NAME, flags, FILE_MODE);
		ftruncate(fd, length);
		ptr = mmap(NULL, length, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
		pthread_mutex_init(&mutex, NULL);
		pthread_cond_init(&cond, NULL);
		pthread_create(&pt1, NULL, shm_read, NULL);
		pthread_create(&pt2, NULL, shm_write, NULL);
		pthread_join(pt1, NULL);
		pthread_join(pt2, NULL);
		// shm_write();
		// shm_read();
		pthread_cond_destroy(&cond);
		pthread_mutex_destroy(&mutex);
		munmap(ptr, length);
		shm_unlink(SHM_NAME);
		return 0;
	} /* ----------  end of function main  ---------- */
```

### 进程内存控制

| Function                                 | Platform | Description                              |
| :--------------------------------------- | :------- | :--------------------------------------- |
| SetProcessWorkingSetSize<br>GetProcessWorkingSetSize | Windows  | Sets/get the minimum and maximum working set sizes for the specified process |
| brk<br/>sbrk                             | Linux    | change data segment size                 |
| setrlimit<br>getrlimit                   | Linux    | get/set resource limits                  |

### 其他系统函数对应

| Category  | Windows                                  | Linux                                    |
| :-------- | :--------------------------------------- | :--------------------------------------- |
| Time      | GetLocalTime<br/>FileTimeToLocalFileTime<br/>FileTimeToSystemTime<br/>GetTickCount | localtime<br/>gettimeofday<br/>gmtime<br/>clock_gettime |
| Memory    | FillMemory<br/>ZeroMemory<br/>CopyMemory<br/>MoveMemory<br/> | memset<br/>memset<br/>memcpy<br/>memmove<br/> |
| sys log   | RegisterEventSource<br/>ReportEvent<br/>DeregisterEventSource | openlog<br/>syslog<br/>closelog          |
| mem alloc | GlobalAlloc<br/>GlobalFree               | malloc<br/>free                          |
| sys error | GetLastError                             | strerror<br/>errno                       |
| string    | StrToInt<br/>MultiByteToWideChar<br/>StringCchPrintf | atoi<br>iconv<br/>sprintf                |

### WSAWaitForMultiObjects

```c
/*
 * =====================================================================================
 *
 *       Filename:  waiForMulti.c
 *
 *    Description:  wait for multi objects
 *
 *        Version:  1.0
 *        Created:  11/12/2016 12:21:09 AM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/sem.h>
#include <sys/ipc.h>
#include <errno.h>

#define SEM_R 0400  //用户（属主）读
#define SEM_A 0200  //用户（属主）写
#define SVSEM_MODE (SEM_R | SEM_A | SEM_R >> 3 | SEM_R >> 6)
static int num = 0;

union semun
{
	int val;
	struct semid_ds *buf;
	unsigned short *array;
};

void thread()
{
	int semid;
	if (++num < 3)
	{
		printf("%d\n", num);
		return;
	}
	semid = semget(ftok("test", 0), 0, 0);
	if (0 != semctl(semid, 0, SETVAL, 0))
	{
		printf("error\n");
	}
	else
	{
		printf("change over\n");
	}
}

int main(int argc, char *argv[])
{
	int i, ret, oflag, semid, nsems;
	pthread_t pt1, pt2, pt3;
	struct sembuf *ops;
	struct semid_ds seminfo;
	unsigned short *ptr;
	union semun arg;
	oflag = SVSEM_MODE | IPC_CREAT | IPC_EXCL;  //设置创建模式
	//创建信号量，通过ftok函数创建一个key，返回信号量 标识符
	nsems = 3;
	if (semid = semget(ftok("test", 0), nsems, oflag) < 0)
	{
		if (errno == EEXIST)
		{
			semid = semget(ftok("test", 0), 0, 0);
			arg.buf = &seminfo;
			semctl(semid, 0, IPC_STAT, arg);
		}
	}
	ptr = calloc(nsems, sizeof(unsigned short));
	ptr[0] = 1;
	arg.array = ptr;
	semctl(semid, 0, SETALL, arg);
	semctl(semid, 0, GETALL, arg);
	for (i = 0; i < nsems; ++i) printf("%d: %d\n", i, arg.array[i]);
	pthread_create(&pt1, NULL, thread, NULL);
	pthread_create(&pt2, NULL, thread, NULL);
	pthread_create(&pt3, NULL, thread, NULL);
	ops = calloc(nsems, sizeof(struct sembuf));
	ops[0].sem_num = 0;
	ops[0].sem_op = 0;
	ops[0].sem_flg = 0;
	semop(semid, ops, nsems);
	memset(&seminfo, 0, sizeof(seminfo));
	semctl(semid, 0, GETALL, arg);
	for (i = 0; i < nsems; ++i) printf("%d: %d\n", i, arg.array[i]);
	exit(0);
}
```
```c
/*
 * =====================================================================================
 *
 *       Filename:  waiForMulti.c
 *
 *    Description:  wait for multi objects
 *
 *        Version:  1.0
 *        Created:  11/12/2016 12:21:09 AM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  CaiSong (), cais.fnst@cn.fujitsu.com
 *        Company:
 *
 * =====================================================================================
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/sem.h>
#include <sys/ipc.h>

#define SEM_R 0400  //用户（属主）读
#define SEM_A 0200  //用户（属主）写
#define SVSEM_MODE (SEM_R | SEM_A | SEM_R >> 3 | SEM_R >> 6)
static int num = 0;

union semun
{
	int val;
	struct semid_ds *buf;
	unsigned short *array;
};

void thread()
{
	int semid;
	if (++num < 3) {printf("%d\n", num);return;}
	semid = semget(ftok("test", 0), 0, 0);
	if (0 != semctl(semid, 0, IPC_RMID))
	{
		printf("error\n");
	}
	else
	{
		printf("change over\n");
	}
}

int main(int argc, char *argv[])
{
	int i, ret, oflag, semid, nsems;
	pthread_t pt1, pt2, pt3;
	struct sembuf *ops;
	struct semid_ds seminfo;
	unsigned short *ptr;
	union semun arg;
	oflag = SVSEM_MODE | IPC_CREAT | IPC_EXCL;  //设置创建模式
	//创建信号量，通过ftok函数创建一个key，返回信号量 标识符
	nsems = 3;
	semid = semget(ftok("test", 0), 0, 0);
	arg.buf = &seminfo;
	semctl(semid, 0, IPC_STAT, arg);
	ptr = calloc(nsems, sizeof(unsigned short));
	ptr[0] = 1;
	arg.array = ptr;
	semctl(semid, 0, SETALL, arg);
	semctl(semid, 0, GETALL, arg);
	for (i = 0; i < nsems; ++i) printf("%d: %d\n", i, arg.array[i]);
	pthread_create(&pt1, NULL, thread, NULL);
	pthread_create(&pt2, NULL, thread, NULL);
	pthread_create(&pt3, NULL, thread, NULL);
	ops = calloc(nsems, sizeof(struct sembuf));
	ops[0].sem_num = 0;
	ops[0].sem_op = 0;
	ops[0].sem_flg = 0;
	semop(semid, ops, nsems);
	memset(&seminfo, 0, sizeof(seminfo));
	semctl(semid, 0, GETALL, arg);
	for (i = 0; i < nsems; ++i) 
	{
		printf("%d: %d\n", i, arg.array[i]);
	}
	exit(0);
}
```

等待多事件，所有的`WSAWaitForMultiObjects`函数都没有等待多个事件，除了程序继续运行的必要事件外，其他监视的是数据库写入、连接等异常事件。若数据库连接异常，可以在写DB出错被发现，非必须监视。其他写与网络相关的事件在`epoll`中被监视，其他线程可以不监听。  

## 数据缓存

对于不经常修改的数据建议使用缓存，人为手动修改数据库，导致的异常不应该在考虑范围。对于通过ITP修改的数据，ITP在DB中添加相应修改记录，中间件通过扫描该表更新缓存。
	a. 运用服务器监视线程：
	* fn_App_CmdListenThd
	cmd监视
	* fn_App_CompanyInfoListenThd
	会社情报监视，遍历所有数据，逐条比较内容校验是否变更；
	* fn_App_EvtListenThd
	监视序列号检测事件、命令响应事件;
	* fn_App_SnpReqListenThd
	画像取得超时事件
	* fn_App_ConnInfoListenThd
	地图数据状态、服务器状态、连接数更新
	
	b. 版本服务器监视线程 ：
	* fn_Ver_CompanyInfoUpdThd
	会社情报监视
	* fn_Ver_ConnInfoUpdThd
	数据库连接数更新
	
	c. Hyr服务器
	* fn_Hyr_ServerInfoListenThd
	mst_Server_Management监视

## 不成熟方案

1. 使用多线程、进程考虑

```plain
	多线程的优点：
	方便高效的内存共享 - 多进程下内存共享比较不便，且会抵消掉多进程编程的好处
	较轻的上下文切换开销 - 不用切换地址空间，不用更改CR3寄存器，不用清空TLB。
	多进程的优点：
	更强的容错性 - 一个进程crash不会导致整个系统崩溃
	更好的多核可伸缩性 - 进程的使用将许多内核资源（如地址空间，页表，打开的文件）隔离，在多核系统上的可伸缩性强于多线程程序<br/>
	综上，当你的不同任务间需要大量共享数据或频繁通信时，使用多线程，其他情况下尽量使用多进程。
	提高多线程程序效率的一般方法：
	不要频繁创建，销毁线程，使用线程池
	减少线程间同步和通信（最为关键）
	避免需要频繁共享写的数据
	合理安排共享数据结构，避免伪共享（false sharing）
	使用非阻塞数据结构/算法
	避免可能产生可伸缩性问题的系统调用（比如mmap）
	避免产生大量缺页异常，尽量使用Huge Page
	可以的话使用用户态轻量级线程代替内核线程<br/>
	作者：刘然
	链接：https://www.zhihu.com/question/24485648/answer/27980547
	来源：知乎
	著作权归作者所有，转载请联系作者获得授权。
```

