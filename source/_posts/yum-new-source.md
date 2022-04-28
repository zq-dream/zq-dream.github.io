---
title: yum使用aliyun的源,下载更快
date: 2022-04-28 14:57:49
categories: 工具
tags: yum
---
## 备份系统自带的yum源文件
```shell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

## 下载阿里云的yum配置文件
```shell
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

## 运行yum makecache 生成缓存
```shell
yum makecache
```
