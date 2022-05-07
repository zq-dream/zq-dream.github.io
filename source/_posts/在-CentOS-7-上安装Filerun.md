---
title: 在 CentOS 7 上安装Filerun
date: 2022-05-06 16:41:00
categories:
- 工具
tags:
---
# 前置环境
>[Apache](https://zqiang.icu/2022/05/06/%E5%AE%89%E8%A3%85-Apache-Web-%E6%9C%8D%E5%8A%A1%E5%99%A8/)  
>[MariaDB 10](https://zqiang.icu/2022/05/06/%E5%AE%89%E8%A3%85-MariaDB-10/)  
>[PHP 7.4](https://zqiang.icu/2022/05/07/install-PHP-FPM-7-4/)  

## 配置数据库
使用 root 帐户登录 MariaDB
```shell
mysql -u root -p
```

创建数据库
```mysql
CREATE DATABASE filerun;  
```
创建一个用户并给权限
```mysql
GRANT ALL ON filerun.* to 'filerun'@'localhost' IDENTIFIED BY 'filerun';  

```
执行刷新权限操作
```mysql
FLUSH PRIVILEGES; 
```

退出MariaDB
```shell
exit  
```

## 配置PHP
安装 FileRun 所需的 PHP 模块
```shell
yum install -y php-imagick php-mbstring php-opcache php-pdo php-mysqlnd php-gd php-xml php-zip  
```
还有一个模块手动下载安装
```shell
cd /usr/lib64/php/modules  
wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz  
tar xvfz ioncube_loaders_lin_x86-64.tar.gz  
```
将filerun需要的PHP相关配置写入文件，该文件将由 PHP 自动附加到其配置中
```shell
vim /etc/php.d/01_filerun.ini  
```
将以下配置加入配置文件中
```shell
xpose_php              = Off  
error_reporting         = E_ALL & ~E_NOTICE  
display_errors          = Off  
display_startup_errors  = Off  
log_errors              = On  
ignore_repeated_errors  = Off  
allow_url_fopen         = On  
allow_url_include       = Off  
variables_order         = "GPCS"  
allow_webdav_methods    = On  
memory_limit            = 128M  
max_execution_time      = 300  
output_buffering        = Off  
output_handler          = ""  
zlib.output_compression = Off  
zlib.output_handler     = ""  
safe_mode               = Off  
register_globals        = Off  
magic_quotes_gpc        = Off  
upload_max_filesize     = 20M  
post_max_size           = 20M  
enable_dl               = Off  
disable_functions       = ""  
disable_classes         = ""  
session.save_handler     = files  
session.use_cookies      = 1  
session.use_only_cookies = 1  
session.auto_start       = 0  
session.cookie_lifetime  = 0  
session.cookie_httponly  = 1  
date.timezone            = "UTC"

zend_extension = /usr/lib64/php/modules/ioncube/ioncube_loader_lin_7.4.so
```

最后重启php-fpm服务，使配置生效
```shell
systemctl restart php-fpm.service  
```

## 下载filerun的安装包
在web服务器的根目录下下载并解压后给权限
```shell
cd /var/www/html/  
wget -O FileRun.zip https://filerun.com/download-latest-centos-7  
unzip FileRun.zip
rm FileRun.zip  
chown -R apache:apache system/data/
```

打开apache web服务的地址，按照安装向导配置filerun，保存下初始管理员的密码
```
Your username is superuser
Your password is cbfd28c4a6de
```
登录后修改管理员密码

在对应配置文件夹下下载中文翻译包
```shell
cd /var/www/html/system/data/translations/
wget https://raw.githubusercontent.com/zq-dream/back/main/chinese.zip
unzip chinese.zip
rm chinese.zip
```
在设置`Interface`中启用中文翻译包

配置一个文件夹，将文件都存储在那个文件夹中
```shell
mkdir /files  
chown apache:apache /files  
```
在用户-权限中修改文件存储路径

要启用图片、pdf的缩略图需要安装ImageMagick支持
```shell
wget https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm  
rpm -Uvh rpmfusion-free-release*rpm  
yum install -y libheif  
yum install -y ImageMagick*  
```
并在设置`Files` `Thumbs and previews`中启用`Enable ImageMagick support`
