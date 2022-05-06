---
title: Linux环境下安装JDK
date: 2022-05-06 13:54:39
categories:
- 基础
tags:
- java
---
# Linux环境下安装JDK
>系统版本：CentOS Linux release 7.9.2009 (Core)
>JDK版本：	jdk-8u311-linux-x64
## 1.下载
JDK8(又称 JDK1.8) 是 JDK 的一个重要的长期支持版本(LTS)，在生产环境中使用非常广泛。  
oracle官网需要登录才能下载，于是我在[编程宝库](http://www.codebaoku.com/jdk/jdk-oracle-jdk1-8.html)获取了下载链接，这个链接会变化，重新取获取就好了  
下载并解压
```shell
wget -O /opt/software/jdk-8u311-linux-x64.tar.gz 'https://106-42-97-109.d.123pan.cn:30443/123-152/ea3c7df0/1686379-0/ea3c7df0c654d7326c5901efefbc8098?v=1&t=1651816212&s=3600d7dd15e672b8a356c69432594b16&filename=jdk-8u311-linux-x64.tar.gz&d=871df302'

cd /opt/module && tar -zxvf /opt/software/jdk-8u311-linux-x64.tar.gz
```
## 2.添加到环境变量
```shell
vim /etc/profile
```
将以下JAVA_HOME配置添加到下面
```shell
# JAVA_HOME
export JAVA_HOME=/opt/module/jdk1.8.0_311
export PATH=$PATH:$JAVA_HOME/bin
```
刷新对配置的引用
```shell
source /etc/profile
```
测试能否成功使用
```shell
java -version
```
显示版本信息即成功配置
```shell
java version "1.8.0_311"
Java(TM) SE Runtime Environment (build 1.8.0_311-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.311-b11, mixed mode)
```

