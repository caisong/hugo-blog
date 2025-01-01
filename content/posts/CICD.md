---
title: CICD
date: 2023-10-22T21:40:35+08:00
lastmod: 2023-10-22T21:40:35+08:00
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
# CI/CD

# 整体流程
* 开发人员：fork本地本地分支，需要完成后，创建`pull request`。提交时提交日志中关联jira issue
* 代码管理员：
    * merge request
    * 仓库ci/cd流程部署
* 测试人员：测试，jira状态变更
* 版本发布管理：构建、发布包

## 开发人员
* 开发
* 单元测试
### commit规范
pull request 必须以状态 + ISSUE开头，后面格式按项目组要求规范。
目前支持的：
* Resolvers Issue-1
* Closes Issue-1
* Fixed Issue-1

#### gitlab hook
gitlab支持local hook和server hook，server hook目前针对所有提交，按WA目录过滤暂时未找到，故当前使用local hook的方式进行。
开发人员在本地设置 commit-msg hook，设置方法提供模板。

## 代码维护人员
### gitlab CI、CD流程构建
1. 添加`.gitlab-ci.yml`到项目中
    CI、CD的流程说明，主要步骤包括build、test、deploy
    
2. 配置项目对应的runner
    runner是CI、CD的运行环境， 支持多种部署方式，目前推荐推荐使用virtualbox、docker或ssh。
    * ssh每次测试还原有依赖，不建议使用；
    * dokcer使用dockerfile实现，了解的可以使用该方式；
    * vitualbox基于创建的基础镜像，每次run都会创建新的镜像，环境不回对其造成影响。
    部署方式待说明

### gitlab sonar集成
在CI流程中添加SONAR检测

### 漏洞检测（可选）
在CI流程中添加漏洞检测

### gitlab jira集成
开发提交commit后，能直接关联jira。反转开发任务和测试提交的问题单。commit信息也会同步至jira中。

### 代码合并
代码审核，代码合并后会触发测试流程。开发必须保证提交的request是完整功能。

## 项目经理

### 项目功能要求
创建JIRA列表，分配任务。相关代码开发完成后，JIRA状态翻转，触发提交测试流程。

## 测试人员
### jira gitlab互联
JIRA与gitlab关联，JIRA中新建ISSUE

### 测试JIRA
创建项目测试JIRA列表，该JIRA列表完全通过后，自动触发发布流程。

### 测试
项目测试、集成测试

## 版本管理
### 版本包规范
目前版本规范中缺少版本包依赖信息

### 发布包安装测试
配置安装环境，安装测试

### 发布包打包
生成补丁包和发布包

