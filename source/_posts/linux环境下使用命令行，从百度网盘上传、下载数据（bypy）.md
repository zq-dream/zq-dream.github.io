---
title: linux环境下使用命令行，从百度网盘上传、下载数据（bypy）
date: 2022-05-10 13:40:41
categories:
- 工具
tags:
---
前置依赖
>[python环境](https://zqiang.icu/2022/04/19/install-miniconda-jupyterNotebook/)

## 安装bypy库和requests库
```shell
pip install requests -i https://pypi.doubanio.com/simple
pip install bypy -i https://pypi.doubanio.com/simple
```

## 授权
获取授权码，将授权码输入后按回车
```shell
 bypy info #复制生成的链接在浏览器打开，登录百度云账号，会得到一个授权码
```

## 使用
此时百度网盘的文件夹中 `我的应用数据` - `bypy` 文件夹就是可以使用的文件夹了  
上传下载的文件都在此目录下操作

## 常用命令
查看bypy文件夹下的文件目录
```shell
bypy ls  |  bypy list 

```
下载指定文件
```shell
bypy downfile [filename] -v
```

下载指定目录
```shell
bypy downdir [dir_name] -v
```

下载目录下全部文件
```shell
bypy downdir -v
```

上传文件
```shell
bypy upload [file_name]
```

更多命令使用 `bypy -h` 查看命令手册

## 解除绑定
解除授权
```shell
bypy -c
```
或者在网页进行解除授权[解除授权页面](https://passport.baidu.com/accountbind)
