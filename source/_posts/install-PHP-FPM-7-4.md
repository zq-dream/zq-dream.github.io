---
title: 安装 PHP-FPM 7.4
date: 2022-05-07 10:28:12
categories:
- 工具
tags:
-- PHP
---
# 安装 PHP-FPM 7.4
鉴于 CentOS 7 默认提供较旧的 PHP 版本 5.4，我们首先需要更新 yum 存储库
```shell
yum install -y epel-release yum-utils  
yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm 
```

yum会提示导入存储库 GPG 密钥，键入`y` 点击`Enter`  

启用 PHP 7.4 Remi 存储库并安装 PHP 7.4
```shell
yum-config-manager --enable remi-php74 
yum install -y php-fpm php  
```

添加自启动并启动php
```shell
systemctl enable php-fpm.service  
systemctl start php-fpm.service  
```
## 配置PHP-FPM，使Apache与PHP-FPM一起工作
编辑Apache配置文件
```shell
vim /etc/httpd/conf/httpd.conf  
```
在文件末尾且在`IncludeOptional conf.d/*.conf`这行内容前添加以下配置
```
<IfModule proxy_module>
  ProxyPassMatch ^/(.*\.php(/.*)?)$ fcgi://127.0.0.1:9000/var/www/html/$1
</IfModule>
```
在`IfModule dir_module`标签中添加主页名称
```
DirectoryIndex index.html index.php  
```
重启apache web服务，使配置生效
```shell
systemctl restart httpd.service  
```
