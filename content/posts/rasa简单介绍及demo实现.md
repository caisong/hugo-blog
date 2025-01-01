---
title: Rasa简单介绍及demo实现
date: 2022-11-03T21:41:24+08:00
lastmod: 2022-11-03T21:41:24+08:00
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
# rasa 简单介绍及demo实现

ps. 本文基于rasa 3.1版本(python 3.8)

## Rasa简介
Rasa是开源的机器学习框架，用于构建AI小助手和聊天机器人。支持自然语言处理、聊天会话和外部应用对接等。

Rasa有两个主要模块：
* Rasa NLU 用于对用户消息内容的语义理解（用于聊天机器人中的意图提取和实体提取）
* Rasa Core 用于对话管理（用于构建AI助手的对话引擎）

RasaX 帮助用户提升和部署由Rasa框架构建的AI小助手和聊天机器人（用于发布机器人的）

## Rasa core消息处理流程（这部分未验证，根据demo执行看，基本一致）
https://upload-images.jianshu.io/upload_images/3285850-ece175b3a873ff90?imageMogr2/auto-orient/strip|imageView2/2/w/719/format/webp

1. 将用户输入的Message传递到Interpreter(Rasa NLU模块)，该模块负责识别Message中的"意图(intent)“和提取所有"实体”(entity)数据；
2. Rasa Core会将Interpreter提取到的意图和识别传给Tracker对象，该对象的主要作用是跟踪会话状态(conversation state)；
3. 利用policy记录Tracker对象的当前状态
4. 选择执行相应的action
5. action执行，action 记录在Track对象中的？（暂时没明白）
6. 将执行action返回的结果输出

## Rasa 安装
按照官方教程安装
ps. 必须得使用python3.8(3.8以上，机器学习的库有版本冲突)

## Rasa概念(自己理解，可能与官方文档有出入，供参考)
* story: 一种训练数据的形式，是用户和BOT之间的对话表示。用户输入表示为intent，BOT响应表示为action
* intent: 根据用户输入，经过NLU识别后认为用户的意图（目的）
* action: 针对itent可执行的行为
* entity: 就是识别出来的关键字
* slot: 中间变量，结合关键字实现entity存储和逻辑控制
* synonym: 同义词，entity同一关键字的不同说法
* response: bot回复的模板


## Rasa项目结构
执行`rasa init`后可得到基础结构
|路径|文件说明|备注|
|:--|:--|--|
|actions|自定义action代码路径|custom action才需要，默认空|
|models|初始训练的模型数据|执行 `rasa train` 产生模型文件|
|tests|||
|config.yml|NLU、Core配置文件|pipeline nlu相关，policy core相关|
|domain.yml|Rasa domain文件|Core配置文件your assistant’s domain|
|endpoints.yml|对接外部消息服务的endpoint||
|data|数据||
|data/nlu.yml|Rasa NLU的训练数据|描述intent如何识别和entity如何提取的训练文件|
|data/stories.yml|Rasa Stories数据|描述针对不同的intent该采取的action|
|data/rule.yml|Rasa Rule文件||
|credentials.yml|details for connecting to other services||

3.1 都是用yaml格式，且格式与内容跟之前版本都有所差别。官方提供了migrate工具（我没用起来，根据理解重新写的yml文件）

### domain
bot配置文件
intent、slot、entity、action、response都这儿声明
intent 与nlu.yml和storeis.yml文件中的intent对应
slot 与原来格式相差较大，3.1指定了与entity的映射关系。与action结合使用，一般只有action 条件控制时才需要指定，其他NLU根据映射直接赋值了。
action 就是bot动作
  * utter开头的一般直接回复了用于简单动作
  * action 开头的可定制

response 就是回复模板

### config
这部分内容涉及NLU处理流程，不太了解。仅转述根据相关资料
pipeline 配置NLU模块使用的算法？，按顺序执行

```yaml
- name: "MitieNLP" # 预训练词向量
  model: "data/total_word_feature_extractor.dat"
- name: "JiebaTokenizer" # Jieba分词器，中文推荐
- name: "MitieEntityExtractor" # entity提取器
- name: "EntitySynonymMapper" # 同义词映射器 
- name: "MitieFeaturizer" # 特征化
- name: "SklearnIntentClassifier" # 意图分类器
```

policy 好像是响应选择

https://img-blog.csdnimg.cn/20200227102611889.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FuZHJFeHBlcnQ=,size_16,color_FFFFFF,t_70

## rasa server
可以使用rasa SDK实现server端，或者根据其API要求，实现相关接口。
具体可参考 [rasa action server](https://rasa.com/docs/action-server/)

## 参考文档
* [Rasa 入坑指南一：初识 Rasa](https://www.52nlp.cn/rasa%e5%85%a5%e5%9d%91%e6%8c%87%e5%8d%97-%e5%88%9d%e8%af%86rasa) 
* [Rasa 入坑指南二：基于 Rasa 构建天气查询机器人](https://www.52nlp.cn/rasa%e5%85%a5%e5%9d%91%e6%8c%87%e5%8d%97%e4%ba%8c-%e5%9f%ba%e4%ba%8e-rasa-%e6%9e%84%e5%bb%ba%e5%a4%a9%e6%b0%94%e6%9f%a5%e8%af%a2%e6%9c%ba%e5%99%a8%e4%ba%ba)
* [Rasa Doc](https://rasa.com/docs/rasa/)
* [Rasa 聊天机器人框架使用](https://www.jianshu.com/p/ad11f5815447)
* [Rasa中文聊天机器人开发指南(2)：NLU篇](https://jiangdg.blog.csdn.net/article/details/104530994)
* [Rasa中文聊天机器人开发指南(3)：Core篇](https://jiangdg.blog.csdn.net/article/details/105434136)