---
layout: post
title: "开发记录之Git常用命令（使用收集中）"
date: 2017-02-01
comments: true
categories: "develop"
tags:
 - 2017
 - 开发
 - Git
---


> 刚接触Git不久，现在天天都在使用，把用到的命令和踏过的坑列出来，希望一起进步。


### 常用的Clone、Pull、Push命令
* clone主分支[origin]


		// 默认主机是origin
		git clone  https://github.com/PingerOne/ImageGo.git

		// 使用 -o 来指定主机
		git clone -o master https://github.com/PingerOne/ImageGo.git

* clone具体的某一个分支[develop_vote分支]


		git clone -b develop_vote https://github.com/PingerOne/ImageGo.git

<!-- more -->   

* fetch，将服务器代码拉下来，不会与本地代码合并（常用来查看别人的进程）


		git fetch origin develop_vote

* Pull下来，会先fetch，然后merge


		git pull origin develop_vote

* Push上去，推送到远程develop_vote分支


		git push origin develop_vote

### 使用Git在GitHub上新建分支
* 在本地新建一个分支


		git branch develop_refresh   

* 切换到新分支


		git checkout develop_refresh

* 将新分支发布在github上


		git push origin develop_refresh

### 使用Git在GitHub上删除分支
* 在本地删除一个分支


		git branch -d develop_refresh

* 在github远程端删除一个分支


		git push origin :develop_refresh   (分支名前的冒号代表删除)

### 使用Git删除远程服务器文件和文件夹
* 指定文件名字或者文件夹名字


		git rm --cached fileName/-r directoryName

* 提交


		git commit "删除xx文件/xx文件夹"
		git push



---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
