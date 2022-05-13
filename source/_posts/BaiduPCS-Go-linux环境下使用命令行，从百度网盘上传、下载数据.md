---
title: BaiduPCS-Go(linux环境下使用命令行，从百度网盘上传、下载数据)
date: 2022-05-13 12:24:25
categories:
- 工具
tags:
---
# 简介
更多配置或命令参考[百度网盘客户端加强版](https://github.com/qjfoidnh/BaiduPCS-Go)

## 安装
下载并将脚本加入bin目录下
```shell
wget https://github.com/qjfoidnh/BaiduPCS-Go/releases/download/v3.8.7/BaiduPCS-Go-v3.8.7-linux-amd64.zip
unzip BaiduPCS-Go-v3.8.7-linux-amd64.zip
mkdir ~/bin
mv BaiduPCS-Go-v3.8.7-linux-amd64/BaiduPCS-Go ~/bin/baiduPCS-Go
rm -rf BaiduPCS-Go-v3.8.7-linux-amd64
```

## 使用
使用百度 BDUSS 来登录百度帐号  

### 获取百度 BDUSS
前往[百度网盘官网](pan.baidu.com)  
登录后按 `F12`   
切换到 `Application`   
在菜单中找到 `Cookie `   
在下拉菜单总找到 `pan.baidu.com`  
在右侧的Cookie列表中找到 `BDUSS` 复制对应的value值  

### 登录
```shell
baiduPCS-Go login -bduss=[BDUSS]
```

### 切换工作目录
```shell
baiduPCS-Go cd files
```

### 列出当前目录文件
```shell
baiduPCS-Go ls
```
### 修改下载文件的储存目录
```shell
baiduPCS-Go config set -savedir=/files
```

### 下载文件
```shell
baiduPCS-Go d [filename|dirname]
```

### 显示和修改程序配置项
```shell
# 显示配置
baiduPCS-Go config

# 设置配置
baiduPCS-Go config set -选项=值
```
