---
layout:     post
title:      'Linux服务器设置'
subtitle:   'set up linux'
date:       2022-09-23
author:     byron han
header-style: text
catalog: true
tags:
    - linux
    - centos
---

> 本文首次发布于 [Byron Han Blog](https://blog.hanjl.com.com/), 作者 [@han(Byron Han)](http://github.com/hanjl7) ,转载请保留原文链接.

# 初始服务器配置

### 新建账号
```shell
useradd develop
passwd develop
```

### 添加sudo权限
```shell
visudo /etc/sudoers

#写入
develop ALL=(ALL)NOPASSWD : ALL
```

### 设置密钥登录
SSH 密钥对是通过加密算法生成的一对密钥，为远程登录实例提供一种更安全便捷的认证方式。腾讯云创建的 SSH 密钥对采用 RSA 2048位的加密方式，生成包括公有密钥（公钥）和私有密钥（私钥）：

公钥：SSH 密钥对成功生成后，服务器仅存储公钥。对于 Linux 实例，公钥内容存储在 ~/.ssh/authorized_keys 文件中。
私钥：您需要妥善保管私钥，拥有您的私钥的任何人都可以解密您的登录信息，因此您需将私钥保存在一个安全的位置。

#### 优势
使用 SSH 密钥对作为登录凭证，相比用户名和密码的认证方式具备以下优势：

安全性：相比普通的密码登录，SSH 密钥对的安全强度更高，可避免暴力破解。SSH 密钥对采用非对称加密算法生成，使用公开密钥对数据进行加密，只有用对应的私有密钥才能解密。私钥可由用户自己保管，无需通过网络发送。
便捷性：使用 SSH 密钥对可以实现一键远程登录 Linux 实例，无需每次登录都输入密码。另外，在同时维护多台 Linux 实例的场景下，使用 SSH 密钥对登录可以实现更加方便、统一的管理。
[腾讯云参考](https://cloud.tencent.com/document/product/1207/44573)

#### 生成密钥
参考[ssh密钥生成](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

#### 复制密钥对
> 推送至服务器端

```shell
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.15.241
```

### 禁用密码登录
1.执行以下命令，打开 sshd_config 配置文件。
```shell
# 编辑 sshd_config 文件 
vi /etc/ssh/sshd_config

# 禁用密码验证 
PasswordAuthentication no
# 启用密钥验证 
RSAAuthentication yes
PubkeyAuthentication yes
```
2.执行以下命令，重启 ssh 服务
```
sudo systemctl restart sshd
```




