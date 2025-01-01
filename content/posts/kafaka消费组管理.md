---
title: Kafaka消费组管理
date: 2022-08-31T21:41:03+08:00
lastmod: 2022-08-31T21:41:03+08:00
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
# kafaka 消费组管理

```shell
#zookeeper 
docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper
# kafka0 节点
docker run -d --name kafka0 -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=10.0.2.15:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.0.2.15:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
# kafka1 节点
docker run -d --name kafka1 -p 9093:9093 -e KAFKA_BROKER_ID=1 -e KAFKA_ZOOKEEPER_CONNECT=10.0.2.15:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.0.2.15:9093 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9093 -t wurstmeister/kafka
#kafka2 节点
docker run -d --name kafka2 -p 9094:9094 -e KAFKA_BROKER_ID=2 -e KAFKA_ZOOKEEPER_CONNECT=10.0.2.15:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.0.2.15:9094 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9094 -t wurstmeister/kafka
# kafka manager
docker run -d --name kafka-manager  -p 9000:9000 -e ZK_HOSTS=10.0.2.15:2181 sheepkiller/kafka-manager
# 创建分区
kafka-topics.sh --zookeeper 172.17.0.6:2181 --create --topic fp --partitions 3 --replication-factor 2
# 生产者
kafka-console-producer.sh --broker-list 172.17.0.7:9092 --topic fp
# 消费组
# 消费组文件 consumer.properties
group.id=demo

# 消费者
# 多个消费者启多个客户端，相同组即可
kafka-console-consumer.sh --bootstrap-server 172.17.0.7:9092 --topic fp --consumer.config consumer.properties
```