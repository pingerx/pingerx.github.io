---
layout: post
title: "开发记录之Activity的转场动画实现"
date: 2017-06-22
comments: true
categories: "develop"
tags:
- 2017
- 开发
- Android
---


---
关于Google提供的动画框架，请上传送门，[Android Transition Framework详解---超炫的动画框架](http://mp.weixin.qq.com/s?__biz=MzA3MjgwNDIzNQ==&mid=2651940687&idx=1&sn=843fcc9cf508751ec2aab7fe059e9436&chksm=84fd75abb38afcbd3b814127a3401d260e8700240289a44ac6156c1daf0a93f1b4e7e0a20e49&scene=0#rd)


其中对于Activity的跳转有了很不错的讲解，所以具体请查看动画框架，这里只是简单的讲一下三种跳转方式的实现和应用，
实际开发中用的比较多的还是通过主题配置的方式，可以进行全局使用，个别独特的跳转就需要使用动画框架，不过实现了就特别炫。


<!-- more -->   



## 一、通过Theme进行配置（开发中最常用的方式）

### 1、写好跳转动画，采用帧动画的形式
* 在anim文件夹下创建xml文件，使用set动画集来配置动画
* slide_left_in.xml(Activity从左侧进入的动画)


      <?xml version="1.0" encoding="utf-8"?>
      <set xmlns:android="http://schemas.android.com/apk/res/android">
      <translate
          android:duration="300"
          android:fromXDelta="-100.0%p"
          android:toXDelta="0.0"/>
      </set>

* slide_state.xml(Activity保持不变)


      <?xml version="1.0" encoding="utf-8"?>
      <set xmlns:android="http://schemas.android.com/apk/res/android">
      <translate
        android:duration="300"
        android:fromXDelta="0"
        android:toXDelta="0"/>
      </set>


### 2、配置跳转Activity的主题
* 首先在清单文件中，找到指定的Activity，并配置其主题


      <activity
           android:name=".ui.activity.TestActivity"
           android:theme="@style/ActivityTheme"/>


* 其次在style.xml文件中进行设置


      <!--配置单个Activity的跳转动画，可以在AppTheme里配置所有Activity的跳转-->
      <style name="ActivityTheme" parent="AppTheme">
          <item name="android:windowAnimationStyle">@style/activityAnim</item>
      </style>

      <!--配置各种方式的跳转动画-->
      <style name="activityAnim">
          <item name="android:activityOpenEnterAnimation">@anim/slide_right_in</item>
          <item name="android:activityOpenExitAnimation">@anim/slide_state</item>
          <item name="android:activityCloseEnterAnimation">@anim/slide_state</item>
          <item name="android:activityCloseExitAnimation">@anim/slide_right_out</item>
      </style>

      <!--activityOpenEnterAnimation ：activity打开时进入的动画-->
      <!--activityOpenExitAnimation  ：activity打开时退出的动画-->
      <!--activityCloseEnterAnimation ：activity关闭时进入的动画-->
      <!--activityCloseExitAnimation  ：activity关闭时退出的动画-->



## 二、overridePendingTransition()方法进行设置
* 在startActivity()和finish()之后可以调用overridePendingTransition()处理跳转动画，这个方法接收两个参数，一个是新启动的activity进入时的动画，另一个是当前activity消失时的动画。

* 启动


      startActivity(new Intent(this, TestActivity.class));
      overridePendingTransition(R.anim.slide_right_in, R.anim.slide_state);


* 退出


      finish();
      overridePendingTransition(R.anim.slide_right_out, R.anim.slide_state);

## 三、谷歌提供的Activity动画类ActivityOptionsCompat
* ActivityOptionsCompat是supportv4中新加的一个类，可以为activity添加各种动画效果，里面的api至少要求4.0，部分要求5.0以上，谷歌为我们封装好了的一些拉伸扩散动画，共享元素动画等等。

* 启动


        ActivityOptionsCompat compat = ActivityOptionsCompat.makeCustomAnimation(_mActivity,R.anim.slide_right_in,R.anim.slide_state);
        ActivityCompat.startActivity(_mActivity,new Intent(_mActivity,TestActivity.class),compat.toBundle());


* 退出


        ActivityCompat.finishAfterTransition(this);


### 总结
使用时一般是通过配置Theme的方式，在AppTheme里配置所有Activity的跳转动画，进行统一管理，如果需要对某个Activity进行特殊处理，可以使用overridePendingTransition或者ActivityOptionsCompat进行单独设置。

动画执行优先级：系统动画 < AppTheme < (overridePendingTransition\ActivityOptionsCompat)。




---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
