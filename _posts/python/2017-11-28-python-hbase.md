---
category: python-2017
published: true
layout: post
title: Hbase
description: Hbase设计指南.
---

## 1、RowKey的设计
		RowKey = userid-time
		个人信息：userid（ip、mac、openid）
		位置信息：x、y、z、mapid
		消费信息：进店信息


## 2、hbase多表联合分析
	 如果是hbase中的多个表，需要进行多个表的联合分析。如电信大数据分析，需要结合用户话单、位置进行联合分析。





