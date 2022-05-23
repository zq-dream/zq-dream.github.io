---
title: Centos7 普通用户配置sudo免密
date: 2022-05-23 18:35:50
categories:
- 基础
tags:
---
# 起因
自己学习的环境需要执行一条root权限的命令时，每次都要用sudo命令然后再确认密码，非常不方便  
修改配置sudo免密后方便很多

# 修改配置
用root用户修改 `/etc/sudoers`  
可以给用户权限，也可以给某个用户组权限
```shell
user_name  ALL=(ALL) ALL         # 允许user_name执行sudo命令(需要输入密码).
%user_group ALL=(ALL) ALL        # 允许user_group执行sudo命令(需要输入密码).
user_name  ALL=(ALL) NOPASSWD: ALL  # 允许user_name执行sudo命令(不需要输入密码).
%user_group ALL=(ALL) NOPASSWD: ALL # 允许user_group执行sudo命令(不需要输入密码).
```

# 例如
给用户免密sudo权限
```
## Allow root to run any commands anywhere 
root    ALL=(ALL)       ALL
dream   ALL=(ALL)       NOPASSWD: ALL
```
