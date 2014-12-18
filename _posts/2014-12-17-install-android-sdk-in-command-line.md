---
layout: post
title: "在ubuntu的行命令环境安装android sdk"
description: "android"
category: android 
published: false
tags: [android]
---

最近要搭建一个基于android的后台构建系统，这一切都需要通过终端在远程服务器进行部署。下面是我在64位
unbuntu下通过命令行安装android sdk的过程。

## step 1 安装 JDK 环境

配合android的JDK最好选用JDK官方版本而不是Open JDK,下面是在unbuntu下安装JDK 1.7的方法。

    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java7-installer
    


##  step 2 安装32位运行环境

android sdk 工具包的一些命令行工具是基于32位系统的，在64为平台运行32程序必须安装 i386 的一些依赖库, 方法如下：

    sudo dpkg --add-architecture i386
    sudo apt-get update
    sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386
    sudo ./adb


## step 3 安装android SDK

    wget http://dl.google.com/android/android-sdk_r24.0.1-linux.tgz
    tar xvzf android-sdk_r24.0.1-linux.tgz

编辑 .profile 或者 .bash_profile 把下面的目录增加到 path的搜索路径中

    export PATH="$PATH:$HOME/android/android-sdk-linux/tools:$HOME/android/android-sdk-linux/platform-tools"

使环境变量生效

    source ~/.profile

列出sdk相关的列表

    android list sdk --all

输出如下所示：

       1- Android SDK Tools, revision 24.0.1
       2- Android SDK Platform-tools, revision 21
       3- Android SDK Build-tools, revision 21.1.2
       4- Android SDK Build-tools, revision 21.1.1
       5- Android SDK Build-tools, revision 21.1
       6- Android SDK Build-tools, revision 21.0.2
       7- Android SDK Build-tools, revision 21.0.1
       8- Android SDK Build-tools, revision 21
       9- Android SDK Build-tools, revision 20
      10- Android SDK Build-tools, revision 19.1
      11- Android SDK Build-tools, revision 19.0.3
      12- Android SDK Build-tools, revision 19.0.2
      13- Android SDK Build-tools, revision 19.0.1
      14- Android SDK Build-tools, revision 19
      15- Android SDK Build-tools, revision 18.1.1
      16- Android SDK Build-tools, revision 18.1
      17- Android SDK Build-tools, revision 18.0.1
      18- Android SDK Build-tools, revision 17
      19- Documentation for Android SDK, API 21, revision 1
      20- SDK Platform Android 5.0.1, API 21, revision 2
      21- SDK Platform Android 4.4W.2, API 20, revision 2
      22- SDK Platform Android 4.4.2, API 19, revision 4
      23- SDK Platform Android 4.3.1, API 18, revision 3
      24- SDK Platform Android 4.2.2, API 17, revision 3
      ....

选择你想要安装项目的序号，开始安装，这里我想安装 build tools 21 及 android 4.2.2以上的SDK所以选择序号 “1,2,3,20,21,22,23”

    android update sdk -u -a -t  1,2,3,20,21,22,23

## step 4 测试android SDK环境是否OK



