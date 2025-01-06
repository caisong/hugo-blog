---
title: QT网络操作
date: 2024-07-18T21:42:20+08:00
lastmod: 2024-07-18T21:42:20+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - QT
tags:
  - network
  - qt
# nolastmod: true
draft: false
---

真的好难用

```cpp
      QString ctx = QString("{\"name\":\"%1\", \"message\":\"%2\"}").arg(name).arg(message->text());
      qDebug() << ctx <<"\n";
      QNetworkRequest request;
      request.setHeader(QNetworkRequest::ContentTypeHeader, "application/json");
      request.setUrl(QUrl(url));
      manager->post(request, ctx.toUtf8());
```

```cpp
void Widget::replyFinished(QNetworkReply *reply)
{
    // 处理网络响应的代码
    if (reply->error() == QNetworkReply::NoError) {
        // 处理成功响应的情况
        if(reply->operation()==QNetworkAccessManager::GetOperation){
            QByteArray responseData = reply->readAll();
            txt->appendPlainText(QString::fromUtf8(responseData));
        }
        else if (reply->operation() == QNetworkAccessManager::PostOperation){
            message->clear();
        }
    } else {
        // 处理错误情况
        qDebug() << "Network request error:" << reply->errorString();
    }
    reply->deleteLater(); // 释放资源
}
```

```cpp
 manager = new QNetworkAccessManager(this);
    connect(manager, &QNetworkAccessManager::finished, this, &Widget::replyFinished);

    connect(message, &QLineEdit::returnPressed, this, &Widget::send_message);
    QTimer *timer = new QTimer(this);
    connect(timer, &QTimer::timeout, this, &Widget::display_message);
    timer->start(1000);
```