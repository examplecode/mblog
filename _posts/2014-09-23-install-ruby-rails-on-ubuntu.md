---
layout: post
title: "ubuntu下安装ruby rails环境"
description: ""
category: devopt
tags: [ruby,rails]
---


## step1 安装rvm

     curl -L https://get.rvm.io | bash -s stable
     source ~/.rvm/scripts/rvm


## step2 安装 ruby

选择当前最新的稳定版本

    rvm install 2.1.2


## step3 替换默认镜像

使用国内较近的镜像：替换为taobao镜像

    gem source -r https://rubygems.org/
    gem source -a https://ruby.taobao.org

## step4 安装rails

    gem install rails
