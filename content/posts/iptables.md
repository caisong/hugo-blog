---
title: Iptables
date: 2021-09-03T21:41:02+08:00
lastmod: 2021-09-03T21:41:02+08:00
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


# iptables

The `iptables` command will attempt a reverse lookup on ip addresses. This will produce exactly the behavior you describe. You can inhibit the reverse lookup with the -n flag, which is why I always list rules like this:
```shell
iptables -vnL
```

This fact and many other useful tidbits can be found in the `iptables` man page. The relevant section concerning `-n` reads:
```shell
-L, --list [chain]
List all rules in the selected chain. If no chain is selected, all chains
are listed. Like every other iptables command, it applies to the specified
table (filter is the default), so NAT rules get listed by

  iptables -t nat -n -L

Please note that it is often used with the -n option, in order to avoid
long reverse DNS lookups. It is legal to specify the -Z (zero) option as
well, in which case the chain(s) will be atomically listed and zeroed. The
exact output is affected by the other arguments given. The exact rules are
suppressed until you use

  iptables -L -v
```


Tags:
  iptables