---
title: Apachewebdav配置
date: 2024-12-24T21:40:28+08:00
lastmod: 2024-12-24T21:40:28+08:00
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
# apache webdav配置 

```conf
DavLockDB "/usr/local/apache2/var/DavLock"

Alias /uploads "/usr/local/apache2/uploads"

<Directory "/usr/local/apache2/uploads">
    Dav On

    AuthType Digest
    AuthName DAV-upload
    # You can use the htdigest program to create the password database:
    #   htdigest -c "/usr/local/apache2/user.passwd" DAV-upload admin
    AuthUserFile "/usr/local/apache2/user.passwd"
    AuthDigestProvider file

    # Allow universal read-access, but writes are restricted
    # to the admin user.
    <RequireAny>
        Require method GET POST OPTIONS
        Require user admin
    </RequireAny>
</Directory>

BrowserMatch "Microsoft Data Access Internet Publishing Provider" redirect-carefully
BrowserMatch "MS FrontPage" redirect-carefully
BrowserMatch "^WebDrive" redirect-carefully
BrowserMatch "^WebDAVFS/1.[01234]" redirect-carefully
BrowserMatch "^gnome-vfs/1.0" redirect-carefully
BrowserMatch "^XML Spy" redirect-carefully
BrowserMatch "^Dreamweaver-WebDAV-SCM1" redirect-carefully
BrowserMatch " Konqueror/4" redirect-carefully
```