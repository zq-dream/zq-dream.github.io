---
title: 在github上备份hexo
date: 2022-04-28 16:20:11
categories:
- 工具
tags:
- github
- hexo
---
## 前言
重做系统忘记备份hexo了，还好本地有备份markdown，本地的备份我也不是长期留存的，还是在github上做好备份吧。

## 个人备份习惯
个人而言习惯于先备份文件再生成博客。即先执行`git add .`，`git commit -m "hexo back"`，`git push -u origin master`将博客备份完成，然后执行`hexo g -d`发布博客。

### 备份博客的快捷命令
通过`alias`，编辑一些命令的集合，这样就能通过使用`hd`将博客备份后再发布了
```
alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push -f'
```


## 初次做备份
### 创建新分支
新开一个仓库专门放各类备份应该也不错，这个就先和博客放在同一个仓库下，新建一个分支来存放博客的备份。
这个分支的目标是存放hexo的内容备份，就叫`hexo`吧。
在本地新建并切换到名为`hexo`的分支
```
git checkout -b hexo
```
### 屏蔽不需要的文件
平时使用的服务器按传出流量计费的，hexo生成的文件比较大，屏蔽掉比较好
建立`.gitignore`文件将不需要备份的文件屏蔽。个人的`.gitignore`文件如下：
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
_multiconfig.yml
```

### 提交备份到`github master`分支上
指定远程仓库
```shell
git remote add origin git@github.com:zq-dream/zq-dream.github.io.git
```
将文件添加到暂存区
```shell
git add .
```
将暂存区文件提交到本地分支
```shell
git commit -m 'hexo back'
```
将本地分支提交到远程分支
```shell
git push -u origin master
```



## 新环境恢复博客
目前假设本地Hexo博客基础环境已经搭好
### 基础环境
`git`
`nodejs`
`hexo`（使用`npm install -g hexo-cli`安装即可）

### 恢复博客
输入下列命令克隆博客，我在github上设置hexo为默认分支了
```
git clone git@github.com:zq-dream/zq-dream.github.io.git
```
在克隆的那个文件夹下输入如下命令恢复博客：
```
npm install hexo-cli
npm install
npm install hexo-deployer-git
npm i hexo-wordcount --save
```
