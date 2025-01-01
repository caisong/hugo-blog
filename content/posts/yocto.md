---
title: Yocto
date: 2025-01-01T17:09:09+08:00
lastmod: 2025-01-01T17:09:09+08:00
author: Author Name
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - 交叉编译
tags:
  - yocto
  - 交叉编译
# nolastmod: true
draft: false
---


<!--more-->

## recipes
 BitBake Recipes, which are denoted by the file extension .bb, are the most basic metadata files. These recipe files provide BitBake with the following:
```plain
    Descriptive information about the package (author, homepage, license, and so on)

    The version of the recipe

    Existing dependencies (both build and runtime dependencies)

    Where the source code resides and how to fetch it

    Whether the source code requires any patches, where to find them, and how to apply them

    How to configure and compile the source code

    Where on the target machine to install the package or packages created

Within the context of BitBake, or any project utilizing BitBake as its build system, files with the .bb extension are referred to as recipes. 
```

## syntax
