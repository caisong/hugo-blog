---
title: Smack
date: 2021-09-03T21:41:33+08:00
lastmod: 2021-09-03T21:41:33+08:00
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
# smack

```shell
onlycap
	This contains the label processes must have for CAP_MAC_ADMIN
	and CAP_MAC_OVERRIDE to be effective. If this file is empty
	these capabilities are effective at for processes with any
	label. The value is set by writing the desired label to the
	file or cleared by writing "-" to the file.

You can add access rules in /etc/smack/accesses. They take the form:

    subjectlabel objectlabel access
```


```shell
CAP_MAC_ADMIN
    Override Mandatory Access Control (implemented for the SMACK LSM)
CAP_MAC_OVERRIDE
    Allow MAC configuration or state changes (implemented for the SMACK LSM)
```

Tags:
  ltp, smack