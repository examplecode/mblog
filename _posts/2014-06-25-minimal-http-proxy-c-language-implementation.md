---
layout: post
title: "最小的http proxy c语言实现 - 支持翻墙"
description: "c语言实现的http porxy 支持翻墙"
category: 
tags: [proxy,gfw,http,goagent]
---


前几天发布了一个[防止GFWDNS污染的小工具]({% post_url  2014-06-20-the-tools-prevent-dns-cache-pollution %}) 出乎意料的有热心网友很快跟进基于类似原理开发出了更好用的工具，详情点击[这里](http://www.v2ex.com/t/118913#reply123)。于是我又心血来潮写了这么一个小东西，希望能够起到抛砖引玉的作用。

源码地址：[https://github.com/examplecode/mproxy](https://github.com/examplecode/mproxy)

## 关于mproxy

### mproxy 是什么？

这是一个c语言实现的 极小的 http proxy 不依赖任何第三方库核心代码不足500行。


### mproxy有什么作用？

个人认为作用有两点：

1. mproxy 代码量极少，实现简单,可以用来了解http proxy的基本工作原理。
2. 如果你有翻墙的需求，它可以帮忙解决这个问题，至少可以访问google,youtube,facebook,twitter这些网站。

翻墙的原理，一句话搞明白。

     Browser --> mproxy(local proxy)  --> mproxy (remte proxy) -> 墙外的世界

### mproxy 需要单独的服务器资源么？

是的，你出来需要一台本地代理外还需要在国外部署一台独立的服务器作为中转来达到翻墙的目的。mproxy不像一些翻墙软件使用GAE作为服务（GAE服务不允许建立socket）,下面是你所需要的资源。

1. 一台国外的服务器或VPS (现在国外的vps都比较便宜，我的测试环境就是用的[digitalocean](https://www.digitalocean.com/?refcode=0340b5e32fde) 的vps 一个月只需要5美元，网站操作体验感觉比lindoe好，性能稳定性貌似差点，但毕竟价钱不一样) 。
2. 一台unix like 本地服务器作为你的http代理。

### mproxy 如何安装部署？

mproxy 的安装部署请参考以下网址：

[https://github.com/examplecode/mproxy](https://github.com/examplecode/mproxy)

### mproxy和 其他的翻墙软件有什么不同？

其实原理基本原理上没有特别大的区别，只是mproxy实现更加简单，没有使用一些第三方的库比如openssl，异步socket，http lib等。只是使用最少的代码展示翻墙的基本原理而已。

### mproxy 的使用效果如何？

mproxy刚刚开发完毕，实现简陋也没有经过大量测试。和成熟稳定的翻墙软件比还有一定差距，其主要目的也是用来学习和研究翻墙原理,目前这个东东完全没有达到一个产品级的水平，如果你喜欢折腾就继续尝试一下当成玩具，否则就此打住吧，免得你抱怨我发布一个垃圾的东西。目前经测试访问google,twitter,facebook,youtube等网站没有问题。

### mproxy 作为后台程序运行的时候如何查看程序输出？

直接使用重定向命令即可

    ./mproxy -l 8081 -D -d > out_8081.log 2>&1


## 关于测试服务器 

下面是我用来测试的服务器(不保证哪天会关闭)，如果你手头有一个unix like的系统可以先安装一个本地的mproxy,然后连接到我提供的测试服务器看看翻墙效果。服务器来自 [digitalocean](https://www.digitalocean.com/?refcode=0340b5e32fde) 的vps虚拟实例性能不高只有512M的内存，所以测试用户多了可能会响应较慢。

- ip 地址：162.243.247.187
- 端口号: 8080,8081 (目前我的服务器上运行了两个mproxy实例，连接哪个都可以)

再你的本地服务器启动mproxy使用如下命令:
    
    ./mproxy -h 162.243.247.187:8080 -E -d


## 关于vps 

如果你想购买[digitalocean](https://www.digitalocean.com/?refcode=0340b5e32fde)的vps麻烦点击下面的链接，你懂的：）。

[https://www.digitalocean.com/?refcode=0340b5e32fde](https://www.digitalocean.com/?refcode=0340b5e32fde)

