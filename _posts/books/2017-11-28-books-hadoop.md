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

## 6、配置hadoop-env.sh和yarn-env.sh中的JAVA_HOME
		vim etc/hadoop/hadoop-env.sh
		增加：export JAVA_HOME=/usr/java/jdk1.8.0_91

## 7、配置MapReduce
		编辑core-site.xml:
		[root@bogon hadoop-2.7.2]# vim etc/hadoop/core-site.xml
		<configuration>
		    <property>
		        <name>fs.defaultFS</name>
		        <value>hdfs://localhost:9000</value>
		    </property>
		</configuration>

		编辑hdfs-xml：
		[root@bogon hadoop-2.7.2]# vim etc/hadoop/hdfs-site.xml
		<configuration>
		    <property>
		        <name>dfs.replication</name>
		        <value>1</value>
		    </property>
		</configuration>

## 8、格式化：
		bin/hdfs namenode –format

## 9、启动Mapreduce：
		sbin/start-dfs.sh

## 10、使用netstat –a查看所有端口，检查50070是否listen
		访问http://127.0.0.1:50070/

## 11、安装hbase：
		解压：tar –zxvf hbase-1.2.6
		创建tmp目录：mkdir tmp
		修改配置文件hbase-site.xml，单机只需如下配置：
		vim /opt/hbase-1.2.6/conf/hbase-site.xml
		使用本地文件系统：
		<configuration>
		  <property>
		    <name>hbase.rootdir</name>
		    <value>file:///opt/hbase-1.2.6/tmp/hbase</value>
		  </property>
		</configuration>

		启动hbase：执行bin目录下的start-hbase.sh
		http://127.0.0.1:16010

## 12、安装hive：
		下载hive 2.1.1
		https://mirrors.tuna.tsinghua.edu.cn/apache/hive/hive-2.1.1/

		解压：tar –zxvf hive-2.1.1
		设置环境变量：
		vi /etc/profile

		增加：
		export JAVA_HOME=/usr/local/java/jdk1.8.0_91
		export HADOOP_HOME=/opt /hadoop-2.7.2
		export HIVE_HOME=/opt/hive-2.1.1
		export PATH=.:$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HIVE_HOME/bin

		使配置立即生效 
		source /etc/profile

		在目录$HIVE_HOME/conf/下，执行命令 
		cp hive-log4j2.properties.template hive-log4j2.properties拷贝一份重命名 
		修改property.hive.log.dir = /opt/hive-2.1.1/logs/

		安装配置参考：https://www.cnblogs.com/hmy-blog/p/6506417.html

## 13、安装mahout：
		下载apache-mahout-distribution-0.13.0.tar.gz文件，解压。
		在hdfs中创建testdata目录：
		bin/hadoop fs -mkdir -p testdata
		拷贝测试数据到hdfs的testdata目录中
		hadoop fs -copyFromLocal /opt/synthetic_control.data testdata
		
		启动mahout进行聚类算法：
		mahout org.apache.mahout.clustering.syntheticcontrol.kmeans.Job

