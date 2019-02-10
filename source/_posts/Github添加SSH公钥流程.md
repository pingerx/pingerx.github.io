---
layout: post
title: "Github添加SSH公钥流程"
date: 2018-03-25
comments: true
categories: "develop"
tags:
- 2018
- 开发
- Git
---

使用Git操作Github远程仓库时需要登录账号和密码，但是每次操作都需要登录非常麻烦。
所幸Github服务器使用了SSH公钥认证，所以只需要在本地生成一份公钥并添加到Github服务器就可以免去重复登录。

<!-- more -->  


### 1. 检查本地已有公钥
* 公钥默认是生成在`C:\Users\Administrator\.ssh`目录下，检查该目录是否有文件，如果不正确的话可以删除重新生成。
* 或者打开`Git`命令窗口，输入`ls -al ~/.ssh`会列出.ssh目录的文件。

### 2. 生成新的SSH公钥
* `git`命令行输入`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`，替换成自己在`github`的邮箱地址，一直确认就会在`C:\Users\Administrator\.ssh`生成公钥。

### 3. 添加公钥到代理
* `git`命令行输入`eval $(ssh-agent -s)`
* `git`命令行输入`ssh-add ~/.ssh/id_rsa`


### 3. 复制生成的公钥添加到Github账号
* `git`命令行执行`cat ~/.ssh/id_rsa.pub`可以列出公钥内容，复制。
* 或者进入`C:\Users\Administrator\.ssh`目录，复制`id_rsa.pub`文件的内容。
* 登录Github，在设置里添加公钥即可。

### 4. 测试是否连接成功
* `git`命令行执行`ssh -T git@github.com`，如果出现`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`就表示成功。


### 更多关于Github添加SSH公钥信息
* [Github添加SSH公钥官方教程](https://help.github.com/articles/connecting-to-github-with-ssh/)
* [Github添加SSH公钥常见问题](https://help.github.com/categories/authenticating-to-github/)



---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
