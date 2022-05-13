---
title: 安装miniconda和jupyter Notebook
date: 2022-04-19 14:39:01
categories:
- 工具
tags:
- miniconda
- jupyter notebook
- python
---
# 安装`Miniconda`
```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
```

# 安装使用`jupyter notebook`

## 通过Anaconda安装`jupyter notebook`
```python
conda install jupyter notebook
```

## 设置密码生成密钥
```python
python
from notebook.auth import passwd 
passwd() 
```
接下来便会让你输入两次密码，该密码在登陆jupyter时需要使用。密码确认后就会生成一段密钥。

## 获取配置文件路径
使用默认配置替换现有配置（此处用来获取配置文件路径）
```python
jupyter notebook --generate-config --allow-root
```
`--generate-config`:使用默认配置替换现有配置  
`--allow-root`:不建议以 root 身份运行，跳过root检测

## 修改配置文件
```shell
vim ~/.jupyter/jupyter_notebook_config.py
```
增加以下属性
```python
c.NotebookApp.ip='*'                                     # 就是设置所有ip皆可访问  
# 设置密码后生成的密钥  
c.NotebookApp.password = u'argon2:$argon2id$v=19$m=10240,t=10,p=8$fCXQDWpf2jRqi5rXorz7Rg$iAz+u1S/3J7pP49MnBnZi2uSQdcbti3/M1B/LV/4Da0'
c.NotebookApp.open_browser = False                       # 禁止自动打开浏览器  
c.NotebookApp.port =8889                                 #这里是你选择使用的端口 
c.NotebookApp.notebook_dir = '/opt/module/notebook_dir'  #指定`jupyter notebook`存放文件的目录，缺省是用户家目录
```

## 关联`Jupyter Notebook`和`conda`的环境和包——`nb_conda`
安装
```python
conda install nb_conda
```
上述命令将`conda`创建的环境与`Jupyter Notebook`相关联，便于在Jupyter Notebook的使用中，在不同的环境下创建笔记本进行工作。

卸载
```python
canda remove nb_conda
```

## Markdown生成目录
Jupyter Notebook无法为Markdown文档通过特定语法添加目录，因此需要通过安装扩展来实现目录的添加
```python
conda install -c conda-forge jupyter_contrib_nbextensions
```
执行上述命令后启动`Jupyter Notebook`导航栏多了`Nbextensions`的类目，点击`Nbextensions`，勾选`Table of Contents`
之后再在`Jupyter Notebook`中使用Markdown，点击工具栏中的对应图标即可使用。

## 运行jupyter notebook
```shell
nohup jupyter notebook --allow-root >> ~/notebook.log 2>&1 &
```

## 增加快捷启动命令
编辑配置文件
```shell
vim ~/.bashrc
```

增加快捷命令
```python
alias notebook='nohup jupyter notebook --allow-root >> ~/notebook.log 2>&1 &'
```
