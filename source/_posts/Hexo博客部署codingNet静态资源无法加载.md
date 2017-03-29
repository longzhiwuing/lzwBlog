---
title: Hexo博客部署codingNet静态资源无法加载
date: 2017-03-29 15:29:14
tags:
categories:
description:
---
用Hexo搭建的个人博客，部署到github的pages的话，好像百度搜索不到。所以在国内的codingNet的pages服务也一起部署一下，这样方便国内国外搜索引擎收录进来。具体部署教程我是参考[这里](http://blog.csdn.net/u011303443/article/details/51509351)但是今天部署到codingNet的pages服务的时候，发现静态资源都加载不到，后来网上搜索了半天，才发现原来你要打算用codingNet的pages服务部署你的博客的话，你创建项目的名字必须和用户名保持一致，不能自己随便自定义。我重新创建了一个和用户名一致的项目，部署到他的pages服务，访问正常

博客地址：http://longzhiwuing.coding.me/longzhiwuing/