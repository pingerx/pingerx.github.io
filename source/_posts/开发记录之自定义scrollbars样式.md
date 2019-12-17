---
layout: post
title: "开发记录之自定义scrollbars样式"
date: 2017-05-20
comments: true
categories: "Android"
tags:
 - 2017
 - 开发
 - Android
---


---
由于项目之前引用了一些很老的系统主题，所以显示的scrollbars样式特别的丑，于是我决定自己去自定义一个好看一点的，实现起来也是蛮简单的。

scrollbars是View自带的一个属性，所以只需要定义一套，之后所有有scrollbars属性的控件都可以使用，当然也可以定制多套，只需要使用shape属性指定颜色就可以。


<!-- more -->  


### 1，使用shape绘制scrollbar的灰色样式
* scrollbar_vertical_thumb.xml文件如下：


      <?xml version="1.0" encoding="utf-8"?>
      <shape xmlns:android="http://schemas.android.com/apk/res/android"
          android:shape="rectangle">
          <solid android:color="#55000000"/>
          <corners android:radius="1dp" />
      </shape>

### 2，在需要使用的控件里调用
* 比如ListView的自定义scrollbar写法


      <ListView
          android:id="@id/list"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:clickable="true"
          android:overScrollMode="never"
          android:scrollbarSize="@dimen/scroll_bar_size"
          android:scrollbarThumbVertical="@drawable/scrollbar_vertical_thumb"/>


---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
