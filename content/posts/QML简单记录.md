---
title: QML简单记录
date: 2024-07-23T21:42:19+08:00
lastmod: 2024-07-23T21:42:19+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - qt
tags:
  - qml
# nolastmod: true
draft: false
---

QML 简单记录  

显示风车旋转


```qml
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    Image{
        id:background
        source: "qrc:/background.png"
    }

    Image {
        id:wheel
        anchors.centerIn: parent //居中
        source: "qrc:/pinwheel.png"

        Behavior on rotation { // behavior on <prooerty>
            NumberAnimation {  // numberanimation 延迟动画
                duration: 250
            }
        }
    }

    MouseArea {
        anchors.fill: parent
        onPressed: { //事件
            wheel.rotation += 90
        }
    }

    visible: true
    width: background.width
    height: background.height
    title: qsTr("Hello World")
}

```

* ubuntu使用quick时，`Unknown module(s) in QT: qml quick`    
  安装开发包`qtdeclarative5-dev`  
  
* 问题 module "QtQuick.Controls" version 2.12 is not installed  
  安装`qml-module-qtquick-controls2` 

