---
title: Repo源制作
date: 2021-12-29T21:41:25+08:00
lastmod: 2021-12-29T21:41:25+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 运维
tags:
  - rhel
  - centos
# nolastmod: true
draft: false
---

# repo源制作

制作源最好找一台什么都没装的虚拟机，或者`docker`拉一个原始镜像，不然要制作的软件依赖包可能缺失。

1. 下载软件包及依赖
```bash
yum install yum-plugin-downloadonly
# 下载nano为例
yum install --downloadonly --downloaddir=/root/package/nano nano
```

不加--downloaddir参数，CentOS 7下载的依赖包会放在默认路径*/var/cache/yum/x86_64/7/base/packages*下。

2. 制作源

```shell
yum install createrepo
cd <rpm安装包目录>
createrepo .
```

3. 制作repo
RHEL默认releaserver为版本号+server，如AS6U4的releaseServer为6Server；CentOS直接使用版本号,如6、7。

```shell
cat  > /etc/yum.repos.d/<your_repo_name.repo> <<EOF
[repo-name]
name=<repo name>
baseurl=file:///<rpm direcotry>/\$releaserver/
enabled=1
gpgcheck=0
EOF

```
