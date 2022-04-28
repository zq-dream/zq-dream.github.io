---
title: (转载)图解HDFS存储原理 漫画 中文
date: 2022-04-19 14:39:01
categories:
- 大数据
tags:
- hadoop
- hdfs
- 转载
---
>转载地址[翻译经典 HDFS 原理讲解漫画](https://blog.csdn.net/hudiefenmu/article/details/37655491)
# 1. HDFS写数据原理
![hdfs_write_1](/img/hadoop/hdfs/hdfs_write_1.jpg)  
![hdfs_write_2](/img/hadoop/hdfs/hdfs_write_2.jpg)  
![hdfs_write_3](/img/hadoop/hdfs/hdfs_write_3.jpg)

# 2. HDFS读数据原理
![hdfs_read](/img/hadoop/hdfs/hdfs_read.jpg)

# 3. HDFS故障类型和其检测方法
![hdfs_tolerance_1](/img/hadoop/hdfs/hdfs_tolerance_1.jpg)  
![hdfs_tolerance_2](/img/hadoop/hdfs/hdfs_tolerance_2.jpg)  

## 3.1 读写故障的处理
![hdfs_tolerance_3](/img/hadoop/hdfs/hdfs_tolerance_3.jpg)  

## 3.2 dataNode故障处理
![hdfs_tolerance_4](/img/hadoop/hdfs/hdfs_tolerance_4.jpg)  

## 3.3 副本布局策略
![hdfs_tolerance_5](/img/hadoop/hdfs/hdfs_tolerance_5.jpg)   
