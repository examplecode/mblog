---
layout: post
title: "GFW DNS污染原理 - 防止DNS污染的小工具"
description: "一个小工具用于返回被GFW污染的真实域名"
category: tools
tags: [gfw,dns,tools]
---


以前写的小工具，最近整理代码，再这里公布出来。这个小工具用于获取被gfw dns 污染域名的真实ip地址，通常可以用于获取twitter,youtube,facebook等网址的真实ip地址。如果你的某些程序需要绕过GFW DNS污染也许这些代码片断会用的上，分别提供了c语言和java的实现版本。

其工作原理大致如下：

GFW对域名进行DNS污染的原理实际上是在正常的DNS服务器返回请求包之前，返回请求者错误的IP地址。而GFW返回的这些错误地址也是有规律可循，根据这个原理我们就不难写出对抗GFW DNS污染的程序了。所以我提供的小程序核心内容就有两点：

1. 提供GFW返回IP的一个黑名单列表。
2. 如果服务端返回的DNS响应IP地址在黑名单列表中，则进行忽略并尝试等待真实的ip地址返回。


[前往 github 源码地址][1]


## C 语言版本

### 编译

    gcc -o gfw_dns_resolver  gfw_dns_resolver.c 

编译输出调试信息版本
    
    gcc -o gfw_dns_resolver -DDEBUG gfw_dns_resolver.c 


### 运行示例

    ./gfw_dns_resolver www.twitter.com

输出:

    The real ip is: 199.59.149.230


## JAVA 版本

### 编译

    javac GFWDnsResolver.java

### 运行示例
    java GFWDnsResolver www.youtube.com

输出：

    host:www.youtube.com The real ip is:173.194.72.102


[前往 github 源码地址][1]

[1]: https://github.com/examplecode/gfw_dns_resolver