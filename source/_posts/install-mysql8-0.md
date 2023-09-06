---
title: 安装mysql8.0，配置密码策略，允许远程登录
date: 2023-09-06 15:27:26
categories:
- MySQL
tags:
- install
- MySQL
---

## MySQL安装

### 安装环境

Centos7.9

### 添加 MySQL Yum 存储库

[MySQL 开发人员专区中的 下载 MySQL Yum 存储库页面](https://dev.mysql.com/downloads/repo/yum/)

### 使用以下命令安装下载的发布包

```shell
yum install mysql80-community-release-el7-10.noarch.rpm
```

可以通过以下命令检查 MySQL Yum 存储库是否已成功添加

```shell
yum repolist enabled | grep "mysql.*-community.*"
```

### 选择发布系列

使用MySQL Yum存储库时，默认选择安装最新的，安装最新版本，无需进行任何配置

使用此命令查看 MySQL Yum 存储库中的所有子存储库，并查看其中哪些子存储库已启用或禁用

```shell
yum repolist all | grep mysql
```

### 安装MySQL

```shell
yum install mysql-community-server
```

这将安装 MySQL 服务器的软件包 ( `mysql-community-server`) 以及运行服务器所需的组件的软件包，包括客户端的软件包 ( `mysql-community-client`)、客户端和服务器的常见错误消息和字符集 ( `mysql-community-common`) 以及共享客户端库 ( `mysql-community-libs`) 。

### 启动 MySQL 服务器

使用以下命令启动 MySQL 服务器

```shell
systemctl start mysqld
```

可以使用以下命令检查MySQL服务器的状态

```shell
systemctl status mysqld
```

### 初始配置

超级用户帐户`'root'@'localhost`已创建。`root`用户的密码存储在日志文件中。要显示它，请使用以下命令

```shell
grep 'temporary password' /var/log/mysqld.log
```

使用生成的临时密码登录

```shell
mysql -uroot -p
```

修改密码，默认密码策略`validate_password`要求密码至少包含1个大写字母、1个小写字母、1个数字和1个特殊字符，并且密码总长度至少为8个字符

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
```



## MySQL参数配置

### 配置密码强度策略

查看MySQL密码策略相关配置

```mysql
SHOW VARIABLES LIKE 'validate_password%';
```

修改MySQL密码策略

```mysql
set global validate_password.policy=0;
set global validate_password.length=1;
```



### 配置允许远程连接

更新域属性，’%’表示允许任意IP地址访问

```mysql
update mysql.user set host='%' where user ='root';
```

授权命令

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'WITH GRANT OPTION;
```

更改加密规则

```mysql
ALTER USER 'root'@'%' IDENTIFIED BY 'dream' PASSWORD EXPIRE NEVER; 
```

更改用户密码

```mysql
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'dream'; #更新用户密码
```

重新加载授权信息

```mysql
FLUSH PRIVILEGES;
```

