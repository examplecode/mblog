---
layout: post
title: "在 mac 10.9 下安装 gollum "
description: ""
category: 
tags: [wiki,gollum,markdown]
---

gollum 是github的使用的一个基于markdown的 wiki系统,最重要的是这个wiki非常符合极简主义精神，不需要数据 markdown + git 就可以搞定非常方便。

## 基本的环境


1. Mac 10.9 
2. homebrew 0.9
3. ruby 2.0

## 安装 libiconv

在安装的时候会出现找不到libiconv所以需要安装
基本环境 homebrew 0.9


    brew install libxml2 libxslt
    brew link libxml2 libxslt --force
    wget http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.13.1.tar.gz
    tar xvfz libiconv-1.13.1.tar.gz
    cd libiconv-1.13.1
    ./configure --prefix=/usr/local/Cellar/libiconv/1.13.1
    make
    sudo make install


## 安装 gollum

    git clone https://github.com/gollum/gollum
    gem install gollum

## 创建自己的wiki系统

    mkdir wiki
    cd wiki
    git init
    gollum


