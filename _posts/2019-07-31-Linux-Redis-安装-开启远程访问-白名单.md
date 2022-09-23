---
layout:     post
title:      Linux Redis 安装 开启远程访问 白名单 
subtitle:   Linux Redis  
date:       2019-07-31
author:     byron han
header-img: img/post-bg-mojave.jpg
catalog: true
tags:
    - Linux
    - Redis
---

## 安装
### 1.获取redis安装资源
`wget http://download.redis.io/releases/redis-4.0.8.tar.gz`
### 2.解压redis
`tar xzvf redis-4.0.8.tar.gz`
### 3.安装Redis
```
mkdir /usr/local/redis
cd ~/redis-4.0.8
make
cd ~/redis-4.0.8/src
make install PREFIX=/usr/local/redis
```
### 4.移动redis.conf配置文件到安装目录
```
mkdir /usr/local/redis/etc
mv redis.conf /usr/local/redis/etc
```
### 5.启动Redis
`/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf`
## 配置redis.conf
> vi /usr/local/redis/etc/redis.conf

| 命令 | 备注 |
| --- | --- |
| daemonize 改为 yes |配置redis为后台启动  |
| bind 注掉或者改为0.0.0.0 | 所有人都可访问  |
| requirepass xx | xx 改为你想设置的访问密码 |

> 修改配置完成后需要重启redis  
>  `pkill redis //停止redis   
>  或者直接 kill -9 杀进程 `

## 远程访问
现在测试是否可访问 
> redis-cli -h your_host -p 6379

如果发现不可访问，可检查服务器的防火墙配置，iptables配置，需要开放6379端口
> iptables -I INPUT -p tcp --dport 6379 -j ACCEPT  
service iptables save

## 白名单
### 1.第一种方式通过iptables 允许指定的外网ip访问
```
//只允许127.0.0.1访问6379
iptables -A INPUT -s 127.0.0.1 -p tcp --dport 6379 -j ACCEPT
//其他ip访问全部拒绝
iptables -A INPUT -p TCP --dport 6379 -j REJECT
```
### 2.第二种方式 bind
> 配置多个bind
> bind xxx.xxx.xxx.xxx
