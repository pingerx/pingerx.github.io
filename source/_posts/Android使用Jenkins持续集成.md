---
layout: post
title: "Android使用Jenkins持续集成"
date: 2018-07-23
comments: true
categories: "Android"
tags:
- 2018
- 开发
- Android
---


> 平时迭代开发需要频繁的打包发布到蒲公英上，重复的操作总是令人厌烦。这里简单介绍一下，使用Jenkins自动打包发布到蒲公英上。


### 安装Jenkins
* 下载最新的版本（一个 WAR 文件）。[官网下载地址](https://jenkins.io)
* 运行 `java -jar jenkins.war` 注意：Jenkins 需要运行 Java 5以及以上的版本。

<!-- more -->

### 配置Jenkins
* 第一次启动，复制命令行中的密码，打开浏览器，输入`localhost:8080`，输入密码，进入主页，创建用户。
* 点击 `系统管理->管理插件->可选插件`，可搜索以下插件安装(其他插件按需安装)。
  * git插件(GIT plugin)
  * ssh插件(SSH Credentials Plugin)
  * Gradle插件(Gradle plugin)
* 点击 `系统管理->系统设置->全局属性`，添加以下键值对，要和系统环境一样。
  * ANDROID_HOME
  * GRADLE_HOME
  * JAVA_HOME

![全局属性](http://chuantu.biz/t6/347/1532335531x-1566688556.jpg)

* 点击 `系统管理->全局工具配置`,Git设置为自动安装，Gradle设置为GRADLE_HOME的路径（路径对上就没问题）。


![全局工具配置](http://chuantu.biz/t6/347/1532335501x-1566688556.jpg)

### 创建任务
* 点击新建任务，选择构建一个自由风格的软件项目
* 源码管理，配置Git的仓库
  * Repository URL：仓库地址
  * Credentials：账号密码
  * Branch Specifier：构建分支

* 构建触发器
  * 定时构建：`H/60 * * * *`表示60分钟检查一次代码，有更新就构建


![仓库和触发器](http://chuantu.biz/t6/347/1532335446x-1566688556.jpg)

* 构建(主要配置Use Gradle Wrapper)
  * Make gradlew executable，打钩
  * Tasks：`build`或者是具体的任务`:app:assembleRelease`
  * Root Build script：`${workspace}`
  * Build File：`${workspace}/a8sport/build.gradle`


![构建](http://chuantu.biz/t6/347/1532335583x-1566688556.jpg)

### 构建任务
* 点击立即构建，就可以主动构建任务，第一次会从Git服务器拉取代码，可能会有一些问题会构建失败，前几次失败了再构建就好，如果一直失败可能就是配置有问题，看一下控制台输出。
* 构建输出目录，点击`系统管理->系统设置`可以查看Jenkins的根目录，在根目录下的workspace下有构建的任务，如`app/build/outputs/apk/beta/release`


### 发布到蒲公英
* 安装插件`Upload to pgyer`
* 配置任务，在构建后操作中，选择`upload to pgyer with apiV2`，配置相关参数即可


![上传蒲公英](http://chuantu.biz/t6/347/1532335554x-1566688556.jpg)


### 参考
* [蒲公英文档](https://www.pgyer.com/doc/view/jenkins)
* [Android基于Gradle参数化打不同环境安装包](https://blog.csdn.net/u011541946/article/details/78267097)


---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
