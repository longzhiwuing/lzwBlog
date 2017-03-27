---
title: CentOS 6.5 root用户启动docker Cannot connect to the Docker daemon.
date: 2017-02-12 19:17:04
tags: docker
categories:
---

在网上搜索Cannot connect to the Docker daemon.这个问题，基本上都是说权限不够导致的。但是我用root用户，肯定不是这个问题。我用service docker start 显示的是OK。但是执行docker images的时候，就会出现Cannot connect to the Docker daemon这个问题。

后来查看日志 less /var/log/docker 发现问题。/usr/bin/docker: relocation error: /usr/bin/docker: symbol dm_task_get_info_with_deferred_remove, version Base not defined in file libdevmapper.so.1.02 with link time reference

在[stackoverflow](http://stackoverflow.com/questions/27216473/docker-1-3-fails-to-start-on-rhel6-5)找到解决方案。大概意思应该是lib包有问题，更新一下就可以了

解决方案：
sudo yum-config-manager --enable public_ol6_latest

sudo yum install device-mapper-event-libs

安装成功后，运行docker images可以正常执行