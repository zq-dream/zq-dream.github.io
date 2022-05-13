---
title: 安装 MariaDB 10
date: 2022-05-06 16:41:47
categories:
- 工具
tags:
- mysql
---
# 安装 MariaDB 10
>MariaDB数据库管理系统是MySQL的一个分支（这里一定要注意，分支分支），主要由开源社区在维护，采用GPL授权许可 MariaDB的目的是完全兼容MySQL，包括API和命令行，使之能轻松成为MySQL的代替品。在存储引擎方面，使用XtraDB来代替MySQL的InnoDB。 MariaDB由MySQL的创始人Michael Widenius主导开发

鉴于 CentOS 7 默认提供了较旧的 MariaDB，我们首先需要更新 yum 存储库
```shell
vim /etc/yum.repos.d/MariaDB10.repo  
```

添加以下配置
```shell
[mariadb]
name = MariaDB
baseurl = http://mirrors.ustc.edu.cn/mariadb/yum/10.3/centos7-amd64/
gpgkey=http://mirrors.ustc.edu.cn/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

安装并运行
```shell
yum install -y mariadb-server mariadb  
systemctl start mariadb  
```

开启自启动
```shell
systemctl enable mariadb.service  
```

运行MariaDB的脚本，设置root密码、根据提示配置一些规则
```shell
mysql_secure_installation
```
