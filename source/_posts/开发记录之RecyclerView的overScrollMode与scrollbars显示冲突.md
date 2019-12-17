---
layout: post
title: "开发记录之RecyclerView的overScrollMode与scrollbars显示冲突"
date: 2017-04-28
comments: true
categories: "Android"
tags:
 - 2017
 - 开发
 - Android
---

---
在使用RecyclerView时，使用overScrollMode="never"去掉阴影，之后发现scrollbars不显示了，google后找到了解决方式。


### 1、有问题的RecyclerView布局
* RecyclerView布局如下


      <android.support.v7.widget.RecyclerView
          android:id="@id/list"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:overScrollMode="never"
          android:scrollbars="vertical"/>


<!-- more -->  
### 2、解决方式
* 解决方法很简单，将RecyclerView背景设置成透明就好了


        android:background="@android:color/transparent"




---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
