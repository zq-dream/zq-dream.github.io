---
title: 虚拟机静态IP配置
date: 2022-05-06 16:39:53
categories:
- 工具
tags:
---
编辑网络配置文件
```shell
vim /etc/sysconfig/network-scripts/ifcfg-eth33
```
添加如下网络配置：

- IPADDR 需要和宿主机同一个网段；
- GATEWAY 保持和宿主机一致；
```shell
TYPE=Ethernet
UUID=7165afdf-2758-48aa-83e7-03f36d2eb256
DEVICE=ens0
ONBOOT=yes
BOOTPROTO=static
IPADDR=192.168.141.130
GATEWAY=192.168.141.2
DNS1=8.8.8.8
```
重启网络服务
```shell
systemctl restart network
```
