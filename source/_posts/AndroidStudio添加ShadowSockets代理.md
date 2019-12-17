---
layout: post
title: "AndroidStudio添加ShadowSockets代理"
date: 2018-05-12
comments: true
categories: "Android"
tags:
- 2018
- 开发
- Android
---

* 平时使用Android Studio访问的基本都是国外的服务器，网速十分的缓慢。所以一般都会对Studio设置代理，
可以直接翻墙访问，速度也是蹭蹭蹭往上涨。
* 进入Studio设置界面，搜索proxy，选择http proxy选项。
* 选择Automatic proxy configuration url，填入`http://127.0.0.1:1080/pac`，apply就可以了。


<!-- more -->  

> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
