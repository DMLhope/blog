---
title: 关闭ipv6的方法
description: 关闭ipv6的方法
date: 2023-11-22 00:00:00+0000
categories: 
  - note
tags: 
  - ipv6
image: 20231122.png
---

## linux配置文件关闭ipv6
编辑/etc/sysctl.conf文件
``` 
sudo vim /etc/sysctl.conf
```
添加如下代码:
``` 
net.ipv6.conf.all.disable_ipv6=1

net.ipv6.conf.default.disable_ipv6=1

net.ipv6.conf.lo.disable_ipv6=1
```
重新加载配置
``` 
sudo sysctl -p
```

## linux临时关闭ipv6
查询自己的网卡名称可以使用`ipconfig`或者`ip a`,用来确认想要关闭ipv6的网卡名
临时关闭可以使用如下命令:
```
 sudo sh -c 'echo 1 > /proc/sys/net/ipv6/conf/<interface-name>/disable_ipv6'
```
这里的`<interface-name>`指的就是之前确认的网卡名

