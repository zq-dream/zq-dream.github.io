---
title: 配置SSH免密登录
date: 2022-05-07 12:58:00
categories:
- 工具
tags:
---
# 配置映射
配置 ip 地址和主机名映射
```shell
vim /etc/hosts
```
添加映射信息
```
192.168.0.101  dream101
192.168.0.102  dream102
192.168.0.103  dream103
```

# 生成公私钥
```shell
ssh-keygen -t rsa
```

# 授权
将生成的公钥写入到授权文件
```shell
cat id_rsa.pub >> authorized_keys
chmod 600 authorized_keys
```
