---
title: RowCallbackHandler处理数据问题
date: 2017-11-16 20:12:35
tags: spring-boot,jdbcTemplate
categories:
description:
---

今天通过jdbcTemplate.query方法传入sql语句，进行结果处理时，选择了RowCallbackHandler的回调方式。刚开始自以为是的写出
```
while(rs.next()){
	//处理逻辑
}
```
结果发现，结果总是少一条记录，当时觉得很奇怪，网上找了半天，才发现RowCallbackHandler的processRow回调方法本意就是方便的让你写出处理每一条数据的处理逻辑。也就是说自己不必再循环获取每一条数据了。只要直接在方法里写出处理每一条数据的业务逻辑即可。

