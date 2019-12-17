---
layout: post
title: "Linux文件权限"
date: 2018-07-03
comments: true
categories: "Linux"
tags:
- 2018
- 开发
- Linux
---

有一次下载一个工具，点击setup时没有反应，使用命令行打开时提示权限不够。
Linux系统对文件的权限做了很详细的区分和敏感处理，因此需要单独去申请权限。
常用的命令如下。

<!-- more -->  

#### 常用命令
* 列举当前目录文件权限: `ls -l`
* 当前目录指定文件权限：`chmod a+x filename`
* 指定目录文件权限:`chmod 777 /home/pinger`
* 指定目录及该目录下的子目录和子文件的权限:`chmod -R 777 /home/pinger`
