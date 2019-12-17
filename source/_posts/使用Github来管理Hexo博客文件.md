---
layout: post
title: "使用Github来管理Hexo博客文件"
date: 2018-07-03
comments: true
categories: "Hexo"
tags:
- 2018
- 开发
- Git
---

Hexo在本地完成初始化和博客编辑，最终是部署在Github上的。
如果你换台电脑更新博客就非常麻烦，必须要拷贝博客的代码，重新部署才能生效。
有一个办法可以解决这个问题，就是在Github上开一个分之来管理代码文件。

<!-- more -->  


Hexo部署在Github上默认是master分支，这个分支是
存放Hexo部署后的文件的，并不是本地博客的源文件。

使用命令`git branch hexo`新建hexo分支，该将作为存放本地源文件的分支。
在master分支上编辑文件，部署发布博客，等博客发布完成后，执行`git add .`
和`git commit -m '更新内容'`把改动的文件添加到本地git仓库。

执行`git checkout hexo`，切换到hexo分支，该分支不需要改动任何内容。
在hexo分支上执行`git merge master`合并master分支的文件，
执行`git push hexo`发布到服务器就好了。

当换台电脑编写博客时，如果是第一次使用，先拉取Github上的代码到本地，配置好Hexo的环境。
执行`git branch`确定当前在哪个分支，如果不在hexo分支，
则执行`git checkout hexo`切换到hexo分支，执行`git pull`拉取服务器的最新文件。

切换回master分支，执行`git merge hexo`，合并hexo分支来拉取最新的源文件，
这样就保证了换电脑了，本地的master分支接上了上一次更新的master分支内容。


#### 注意：
* master分支用来编辑内容，该分支的文件不需要使用git提交到服务器，而是使用hexo命令部署。
* hexo分支不需要编辑内容，该分支是master分支文件的中转，需要使用git进行提交和拉取。
