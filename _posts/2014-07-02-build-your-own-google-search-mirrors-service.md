---
layout: post
title: "自己搭建的google搜索镜像服务"
category : tools
description: "免费的Google搜索镜像"
tags : [Google,GFW]
---


基于我前几天发布的一个小工具[mproxy]({% post_url 2014-06-25-minimal-http-proxy-c-language-implementation %})，做了一个免费的Google搜索镜像用来满足日常使用Google的需求，为了发挥VPS的更大效能,现分享出来供免费使用。

注：目前此教程只针对Chrome浏览器，其他浏览器的使用者请忽略此文，或自行想办法(原理上都是一样的)免费的镜像不知能够提供多长时间，有兴趣的话可以按照[mproxy]({% post_url 2014-06-25-minimal-http-proxy-c-language-implementation %})的使用教程自行部署服务

应用原理主要是依赖浏览器的PAC(Proxy-Auto-Config)功能,在使用google的时候自动切换至mproxy提供的代理服务，如果想使用其他被墙的网站原理相同，只需要修改.pac文件就好了。设置简洁3步搞定，详情如下。

### step1 下载并编译mproxy

    clone https://github.com/examplecode/mproxy
    cd mproxy
    gcc -o mproxy mproxy.c


### step2 在命令行启动proxy

    ./mproxy -l 8081 -h free.mmbox.me -E -d

### step 3 以命令行的方式启动Chrome 浏览器

为了确保自动切换代理模式可以正常工作，请再测试之前先禁用(chrome->偏好设置->扩展程序)掉所有的代理管理插件，如proxySwitchSharp。 

#### Mac 版本

    cd /Applications/Google\ Chrome.app/Contents/MacOS
    ./Google\ Chrome --proxy-pac-url=http://free.mmbox.me/mproxy.pac

#### linux 版本

    cd /path/of/chrome
    ./chrome --proxy-pac-url=http://free.mmbox.me/mproxy.pac


在完成以上步骤后就可以畅通无阻的使用Google了，enjoy it ! :) 



