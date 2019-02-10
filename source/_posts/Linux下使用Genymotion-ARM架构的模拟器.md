---
layout: post
title: "Linux下使用Genymotion-ARM架构的模拟器"
date: 2018-04-02
comments: true
categories: "develop"
tags:
- 2018
- 开发
- Linux
---

> 在`deeplin`的`Linux`系统上使用`Genymotion`安装程序时，提示`Installation error: INSTALL_FAILED_NO_MATCHING_ABIS`，
意思是没有匹配的架构。Genymotion模拟器使用的是`x86`架构，所以`ARM`架构的程序安装不了。
解决办法就是给模拟器安装一个`ARM`架构的转换包。

* 打开模拟器，可以正常运行，将下载的转换包拖进模拟器，会提示安装，点击安装。
* 安装成功后，打开命令行，输入`adb shell /system/etc/houdini_patcher.sh`。
* 重新打开模拟器，再次运行程序，成功安装。
[参考地址](https://blog.csdn.net/qq_30707799/article/details/68927892)
[转换包下载地址](http://p6jk8aaz8.bkt.clouddn.com/Genymotion-ARM-Translation.zip)

<!-- more -->   

> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
