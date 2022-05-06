---
title: 安装 Apache Web 服务器
date: 2022-05-06 16:44:01
categories:
- 工具
tags:
---
# 安装 Apache Web 服务器
使用yum安装并启动Apache Web 服务器
```shell
yum install -y httpd  
systemctl start httpd.service  
```
修改apache的配置文件
```shell
vim /etc/httpd/conf/httpd.conf
```

配置监听端口
```shell
Listen 80
```
