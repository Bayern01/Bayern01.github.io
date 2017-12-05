---
category: work-2017
published: true
layout: post
title: Spark
description: Spark环境搭建指南.
---

## 1、软件下载
			在清华镜像网下载spark-2.2.0-bin-without-hadoop.tgz：https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.2.0/
			在官网上下载scala 2.10.4: http://www.scala-lang.org/download/2.10.4.html
			解压并拷贝spark到/opt目录，解压并拷贝scala到/usr/lib目录下

## 2、设置环境变量：
	 vi /etc/profile

	增加：
		export SCALA_HOME=/usr/lib/scala-2.10.4
		export SPARK_HOME=/opt/spark-2.2.0
		export PATH=.:$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HIVE_HOME/bin:$SCALA_HOME/bin:$SPARK_HOME/bin

		使配置立即生效 
		source /etc/profile

## 3、设置hadoop classpath：
	 如果是之前已经安装了hadoop的版本（即使用的spark-2.2.0-bin-without-hadoop.tgz文件），要运行单机版spark，先进入conf目录修改编辑配置文件：spark-env.sh
	增加一行：
		export SPARK_DIST_CLASSPATH=$(hadoop classpath)

	否则会出现java.lang.NoClassDefFoundError: org/apache/hadoop/fs/FSDataInputStream错误。

## 4、启动spark（注意要先启动hdfs）：
	./bin/spark-shell




