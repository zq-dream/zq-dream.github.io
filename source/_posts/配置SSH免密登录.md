---
title: 配置SSH免密登录
date: 2022-05-23 13:03:00
categories:
- 工具
tags:
- ssh
---
# 配置映射
配置 ip 地址和主机名映射
```shell
vim /etc/hosts
```
添加映射信息
```
192.168.0.11  dream11
192.168.0.12  dream12
192.168.0.13  dream13
```

# 生成github和免密登录的公私钥
ssh-keygen命令用于为 `ssh` 生成、管理和转换认证密钥，它支持RSA和DSA两种认证密钥
- `-t` 指定认证类型
- `-b` 指定密钥长度
- `-C` 添加注释
```shell
ssh-keygen -t rsa -b 4096 -C "zqiang918@gmail.com"
```

# 授权
ssh-copy-id命令可以把本地主机的公钥复制到远程主机的authorized_keys文件上  
ssh-copy-id命令也会给远程主机的用户主目录（home）下的 `~/.ssh` 和 `~/.ssh/authorized_keys` 设置合适的权限
- `-i` 指定认证文件(公钥)
- `-p` port 指定连接的端口

```shell
ssh-copy-id dream@dream11
```

# 测试
```shell
ssh dream11
```
