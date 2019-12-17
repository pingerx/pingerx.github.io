---
layout: post
title: "Linux制作快捷启动方式"
date: 2018-04-10
comments: true
categories: "Linux"
tags:
- 2018
- 开发
- Linux
---

Linux使用的安装程序是.deb后缀的软件，安装这种软件会自动生成启动图标，但是我们自己解压出来的.sh文件
就不能够生成快捷启动方式，所以需要制作启动方法。


#### Linux默认启动图标位置
* Linux默认的启动图标都在`/usr/share/applications`这个目录里，使用txt编辑器打开这些文件，发现
其实是键值对的文本内容，并且文件的后缀都是`.desktop`。


      [Desktop Entry]
      Name=studio
      Comment=this is Android Studio
      Exec=/home/pinger/Develop/Android/android-studio/bin/studio.sh
      Icon=/home/pinger/Develop/Android/android-studio/bin/studio.png
      Terminal=false
      Type=Application
      Categories=Application;

<!-- more -->  

* 其中
  * Name表示启动应用的名字
  * Exec表示启动程序的入口，要填写完整
  * Icon表示启动应用的图标


#### 制作启动图标
* 打开文件管理器，进入desktop目录，新建文本文件，将上面内容复制进入，替换Name，Exec和Icon的值，保存关闭。
* 修改该文件名为Name的值，后缀为.desktop。确认即可启动该应用。  


---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
