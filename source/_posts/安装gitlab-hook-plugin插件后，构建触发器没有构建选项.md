---
title: 安装gitlab-hook-plugin插件后，构建触发器没有构建选项
date: 2017-12-27 19:45:28
tags: gitlab jenkins
categories: jenkins gitlab
description:
---

打算当有新的commit push到gitlab时，jenkins可以自动触发构建过程。网上的教程基本都是使用gitlab-hook-plugin插件进行操作，但是我安装完后，当配置构建触发器时，没有教程里的配置项：Build when a change ... 



后来在网上搜的时候发现，需要安装gitlab-plugin插件，而且需要版本1.4.5及以上才会在构建触发器中有该配置项，亲测好使，可以实现触发构建了