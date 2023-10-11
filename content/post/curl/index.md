---
title: curl 命令使用
date: 2021-07-07
categories: 
  - note
tags: 
  - curl
image: 20210707.png
---

## 基础用法

```plain
curl + url （默认为get请求）
```
设定为post请求：
```plain
curl -X -POST url   
curl -XPOST url 
curl -XPOST url -d 数据
 + 例如 curl -X -POST url -d "{"title":"..."}" 
curl -SPUT url -d  数据
curl -XDELETE url
```
将Http Header添加到请求里
```plain
curl URL -H 首部 -H 第二个首部 ...
  + 例如： curl -X -POST url -H 'Cotent-Type:application/json' -d "{"title":"..."}"
```
获取所有首部
```plain
curl -I URL
```
下载
```plain
curl -O URL
curl -o 文件名 URL
curl --limit-rate 100k(限速大小) -o 文件名 URL
curl -C - -o 上一次的文件名 URL (实现断点续传)
```
跟随重定向
```plain
curl -L URL
curl -v -L URL (显示详细信息)
```
使用代理
```plain
curl --proxy 协议://用户名:密码@ip地址:端口 URL
```

