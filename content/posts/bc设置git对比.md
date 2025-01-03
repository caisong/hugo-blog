---
title: beyond compare设置git diff
date: 2024-11-06T21:40:29+08:00
lastmod: 2024-11-06T21:40:29+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 工具
tags:
  - bc
  - git
# nolastmod: true
draft: false
---

bc设置git 对比

<!--more-->

[原始链接](https://www.scootersoftware.com/kb/vcs#tortoisegit "bc")

## git windows
### diff
```bat
  git config --global diff.tool bc
  git config --global difftool.bc.path "c:/Program Files/Beyond Compare 5/bcomp.exe"
```
### merge
  ```bat
  git config --global merge.tool bc
  git config --global mergetool.bc.path "c:/Program Files/Beyond Compare 5/bcomp.exe"
  ```

### 使用
```bat
# diff file
   git difftool filename.ext
   # diff dir 
      git difftool --dir-diff
      # merge
         git mergetool filename.txt
```

#### 其他
```bat
git config --global difftool.prompt false
git config --global mergetool.keepBackup false
```

## git linux
**git 1.8版本及以上**
### diff
```bash
git config --global diff.tool bc
git config --global difftool.bc.trustExitCode true 
````

### merge
```bash
git config --global merge.tool bc
git config --global mergetool.bc.trustExitCode true
```

  ### 使用
  ```bash
git difftool file.ext   
git mergetool file.ext
  ```

** git 1.7的暂时不记录了**



* TortoiseGit
* diff
"C:\Program Files\Beyond Compare 5\BComp.exe" %base %mine /title1=%bname /title2=%yname /leftreadonly 
* merge
"C:\Program Files\Beyond Compare 5\BComp.exe" %mine %theirs %base %merged /title1=%yname /title2=%tname /title3=%bname /title4=%mname 
