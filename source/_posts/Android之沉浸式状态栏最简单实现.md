---
layout: post
title: "Android之沉浸式状态栏最简单实现"
date: 2017-08-17
comments: true
categories: "Android"
tags:
 - 2017
 - 开发
 - Android
---


---

网上有很多对于沉浸式状态栏的讲解，也有很多实现沉浸式状态栏的方法。
具体的原理可以参考几篇分析的比较不错的文章：
[Android沉浸式UI实现及原理](http://www.jianshu.com/p/f3683e27fd94)
[Android 系统状态栏沉浸式/透明化完整解决方案](http://www.jianshu.com/p/34a8b40b9308)

这里将两种实现起来比较简单的方式贴出来，可以直接拿去使用。
<!-- more -->  

### 通过代码进行设置
* 在想要实现透明状态栏的Activity里，或者BaseActivity里的setContentView()方法后调用如下代码

<!-- more -->  


      // 设置状态栏，仅支持到4.4以上版本的Android系统，即API19
      public static void initStatus(Activity activity) {

          if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
              activity.getWindow().setFlags(
                      WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS,
                      WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
          }
      }

* 以上代码会把整个状态栏去掉，所以需要在布局文件里的ToolBar设置paddingTop的属性，statusBarSize=25dp


      android:paddingTop="@dimen/statusBarSize"

* 由于透明状态栏是Google在Android 4.4之后才支持的，所以需要根据不同的版本设置statusBarSize的大小，新建values-v19文件夹，将dimen文件的statusBarSize改成0p就好了


### 通过配置主题进行设置
* 在values文件中设置AppTheme


      <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
         <!-- Customize your theme here. -->
         <item name="colorPrimary">@color/colorPrimary</item>
         <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
         <item name="colorAccent">@color/colorAccent</item>
         <item name="android:windowIsTranslucent">true</item>
      </style>


* 在res下新建一个values-v19文件夹，然后新建values.xml文件，设置AppTheme，这是兼容到4.4版本的写法


      <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
          <item name="colorPrimary">@color/colorPrimary</item>
          <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
          <item name="colorAccent">@color/colorAccent</item>
          <item name="android:windowIsTranslucent">true</item>
          <item name="android:windowTranslucentStatus">true</item>
          <item name="android:windowTranslucentNavigation">true</item>
      </style>

* 在res下新建一个values-v21文件夹，然后新建values.xml文件，设置AppTheme，兼容5.0的写法


    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
         <item name="colorPrimary">@color/colorPrimary</item>
         <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
         <item name="colorAccent">@color/colorAccent</item>
         <item name="android:windowIsTranslucent">true</item>
         <item name="android:windowTranslucentStatus">false</item>
         <item name="android:windowTranslucentNavigation">true</item>
         <!--Android 5.x开始需要把颜色设置透明，否则导航栏会呈现系统默认的浅灰色-->
         <item name="android:statusBarColor">@android:color/transparent</item>
     </style>


* 同理，以上代码也会把整个状态栏去掉，所以还需要在布局文件里的根容器下设置如下代码，然后在values-v19文件夹中将dimen文件的statusBarSize改成0p就好了


       android:paddingTop="@dimen/statusBarSize"




---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
