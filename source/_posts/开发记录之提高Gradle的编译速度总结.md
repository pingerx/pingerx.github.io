---
layout: post
title: "开发记录之提高Gradle的编译速度总结"
date: 2016-11-08
comments: true
categories: "Android"
tags:
 - 2016
 - 开发
 - Android
---

---

刚进公司，由于公司准备新地方，所以电脑不够用，先用自己的电脑开发。然后配置环境，运行项目，由于项目经过多年多人之手迭代，已经残破不堪，
所以第一次运行大概花了20多分钟，等得蛋都碎了一地。以为接下来会快一些，鬼知道第二次还是10多分钟，我直接疯掉。

受不了这种等待，立刻就去求助度娘，最后看了许多关于Gradle优化的资料，编译终于快了许多。后面经过多方尝试之后，
发现是Google的run instance的问题，只要开着它运行就特慢，关掉后编译速度杠杠的，原因未知。

除了Gradle编译外，还发现了另一种增量编译的工具，就是阿里蚂蚁团队打造的FreeLine，
使用后发现确实很不错，速度很快，但是由于不够成熟，还是有很多问题，比如不能Debug等等，算了还是安心用Gradle吧。

以下是总结的笔记，分享给大家。

<!-- more -->  


### 参考网站
[Android Studio Gradle太慢 解决方案](https://my.oschina.net/u/1034530/blog/490974)

[30秒让你加速Android Studio/Gradle构建](http://mdsa.51cto.com/art/201503/469038.htm)

[加速Android Studio/Gradle构建](http://blog.isming.me/2015/03/18/android-build-speed-up/)




### 参考步骤
#### 第一步：配置.gradle文件夹目录（开启Gradle单独守护线程）
在windows系统的C:\Users\用户名\\.gradle目录下创建gradle.properties文件（有直接用），然后添加以下内容，添加之后会在所以的项目中生效（有内容则并入），添加后全局生效


        org.gradle.daemon=true  // 开启线程守护，第一次编译时开线程，之后就不会再开了
        org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8  // 配置编译时的虚拟机大小
        org.gradle.parallel=true  // 开启并行编译，相当于多条线程再走
        org.gradle.configureondemand=true   启用新的孵化模式

还可以在当前项目中的gradle.properties文件中添加以上内容，则只会在当前项目生效

#### 第二步：修改android studio配置
Ctrl+Alt+S打开设置选项卡，找到Gradle选项，选中offline work，点击apply，如下
![gradle选项配置](http://upload-images.jianshu.io/upload_images/2786991-f3f4af2c423b914b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

找到Compiler选项，设置如下
![compiler选项配置](http://upload-images.jianshu.io/upload_images/2786991-ca9457f2b9bd0711.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

设置网络代理，增加访问网络速度，具体请参考提供的网站

在具体开发module的build.gradle文件中添加


        dexOptions {
            //使用增量模式构建
            incremental true
            //最大堆内存
            javaMaxHeapSize "8g"
            // 上面两项在As2.2后可以去掉了，默认支持
            //是否支持大工程模式
            jumboMode = true
            //预编译
            preDexLibraries = true
            //线程数
            threadCount = 8
        }


----

## 另一种神速编译方式，使用命令行脚本的方式编译
第一步：在目标项目的根节点下创建文件c.bat（名字尽量短） --> 构建脚本，内容如下：


        @Echo Off

        if /i "%1"=="" goto :default
        if /i "%1"=="i" goto :install
        if /i "%1"=="u" goto :uninstall

        ::执行实际的命令
        goto :raw

        ::无参数情况下的默认执行命令
        :default
        gradlew iD
        goto :eof

        ::实际命令
        :raw
        gradlew %1
        goto :eof

        ::安装所有Debug版本的APK
        :install
        gradlew iD
        goto :eof

        ::卸载所有版本的APK
        :uninstall
        gradlew uA
        goto :eof

第二步：在AS控制台的命令行Terminal窗口输入刚才的文件名，然后回车就好了，编译成功，然后打开应用

这种方式好像是会更快一些，而且不会导入整个电脑的卡顿，总的来说这种方法可以值得推荐，但是使用起来也不是特别的方便。



### 总结
多方尝试后发现，只要使用run instance之后，第一次编译就变得特别的慢，至少都要3分钟，还有特别卡顿，卡的电脑动都动不了，但是在去掉即时运行后，编译时间就短了很多，只有30秒，而且一点都不卡，最后毅然改成了普通运行。


---
> 欢迎大家访问我的[简书](http://www.jianshu.com/u/64f479a1cef7)，[博客](http://wanit.me/)和[GitHub](https://github.com/PingerOne)。
