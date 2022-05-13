---
title: 使用Hexo+Github pages搭建博客
date: 2022-04-28 14:39:01
categories:
- 工具
tags:
- github
- hexo
---
## 前置环境准备
我是用的是Centos7.9.2009(宝塔Linux面板)

### 1.Nodejs
#### 下载
```
wget https://nodejs.org/dist/latest-v17.x/node-v17.9.0-linux-x64.tar.xz
```

#### 解压
```
xz -d node-v17.9.0-linux-x64.tar.xz
tar -xvf node-v17.9.0-linux-x64.tar
```

#### 安装到/opt/module下，配置环境变量
```
mv node-v17.9.0-linux-x64 /opt/module/node-v17.9.0
vim /etc/profile
#在底部添加 PATH 变量
export PATH=$PATH:/opt/module/node-v17.9.0/bin
```

#### 刷新对/etc/profile的引用
```
source /etc/profile
```

#### 验证nodejs能否能正常使用
```
node -v
npm -v
```


### git
#### 安装git
```
yum -y install git
```

#### 验证git是否能正常使用
```
git --version
```

#### 修改本地配置，git才能知道是谁提交的
```
git config --global user.name "zq-dream"
git config --global user.email "zqiang918@gmail.com"
```

#### 本地生成公钥，在[github](https://github.com/settings/keys)中添加公钥，意思是github允许谁提交
```
ssh-keygen -t rsa -b 4096 -C "zqiang918@gmail.com"
cat ~/.ssh/id_rsa.pub
```

#### 验证SSH配置是否成功
```
ssh -T git@github.com
```


## 2.安装Hexo
```
npm install -g hexo-cli
```

### 初始化一个博客的文件夹
#### 创建并进入一个博客目录
```
mkdir ~/myblog
cd ~/myblog
```

#### 初始化Hexo
```
hexo init
npm install
```

#### 验证hexo是否成功安装
```
hexo -v
```

### 试试能否正常启动
#### 启动本地服务器，只有localhost能访问
```
hexo server
```

#### 另起一个终端，使用文本浏览器尝试访问
```
yum -y install elinks
elinks http://localhost:4000/   
```

### 关联hexo和github
#### 在hexo的config中配置github的信息
```
vim _config.yml
#翻到最后修改
deploy: 
    type: git
    repo: git@github.com:zq-dream/zq-dream.github.io.git
    branch: main
    message: '站点更新:{{now("YYYY-MM-DD HH:mm:ss")}}'
```
          
#### 安装github部署的插件
```
npm install hexo-deployer-git --save
```

#### 部署到github上（会先清空github上关联repositories的内容）
```
hexo clean # 清除缓存，若是网页正常情况下可以忽略这条命令
hexo g     #  == hexo generate  生成
hexo d     # == hexo deploy 部署
```
也可以浓缩到一行命令
```
hexo clean && hexo g && hexo d
```
平时使用简洁一点的命令发布
```
hexo g -d
```

## 增加快捷启动命令
编辑配置文件
```shell
vim ~/.bashrc
```

增加快捷命令
```python
alias hd='git add . && git commit -m "hexo back" && git push -u origin master && hexo clean && hexo g && hexo d'
```
