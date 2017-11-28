---
category: books-2017
published: true
layout: post
title: Hadoop
description: CentOS虚拟机安装hadoop.
---

## 1、安装vmware 14虚拟机

## 2、安装CentOS 7
	 选择带GUI的服务器安装模式，带网络（NAT），安装vmware tools，确保虚拟机和宿主机网络能通。


## 3、卸载jdk 1.7.0，安装jdk 1.8:
		#查看内置的JDK
		rpm -qa | grep jdk
		#卸载内置的JDK
		yum remove java-1.7.0-openjdk

		#安装jdk 1.8
		rpm -ivh jdk-8u91-linux-x64.rpm

		设置JAVA_HOME：修改配置文件vi /etc/profile，最后一行添加以下代码
		export JAVA_HOME=/usr/java/jdk1.8.0_91   
		export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
		export PATH=$PATH:$JAVA_HOME/bin

		source命令使文件立即生效：
		source /etc/profile

## 4、linux配置ssh免密码登录
		生成密钥 ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
		把公钥加到用于认证的公钥文件中 cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
		验证ssh免密码登录 ssh localhost 若不需要输入密码则配置成功

## 5、安装hadoop
		解压hadoop文件：tar -zxvf hadoop-2.7.2.tar.gz
		在hadoop 2.7.2目录下新建文件夹：
		mkdir tmp
		mkdir tmp/dfs
		mkdir tmp/dfs/data
		mkdir tmp/dfs/name
