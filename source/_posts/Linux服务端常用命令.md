---
layout: post
title: "Linux服务端常用命令"
date: 2020-01-05
comments: true
categories: "Linux"
img: https://ae06.alicdn.com/kf/Ue94d76a72dfa4846928b4ba8b8636269I.png
tags:
- 2020
- 开发
- Linux
---

### cd命令

* 进入目录：cd /dir
* 退出目录：cd ..

### ls命令

* 查看当前目录文件和目录名：ls
* 查看当前目录文件，包含文件的属性与权限数据：ll


### rz命令
* 使用rz命令，在具体的目录下命令行输入`sudo rz`命令，选择文件即可上传到该目录

### 文件操作
* 列举当前目录文件权限: `ls -l`
* 当前目录指定文件权限：`chmod a+x filename`
* 指定目录文件权限:`chmod 777 /home/pinger`
* 指定目录及该目录下的子目录和子文件的权限:`chmod -R 777 /home/pinger`