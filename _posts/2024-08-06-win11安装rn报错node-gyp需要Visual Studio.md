---
layout:     post
title:      '解决Windows 11运行React Native报错node-gyp需要Visual Studio'
subtitle:   'Resolve the error of node-gyp requiring Visual Studio when running React Native on Windows 11.'
date:       2024-08-06
author:     byron han
header-style: text
catalog: true
tags:
- windows
- node
- react native
- HarmonyOS NEXT
---

### 背景
> 鸿蒙HarmonyOS时支持的React Native版本为0.72.5，所以项目整体做了升级，但在windows 11系统上遇到node-gyp相关报错,**以下都是在无网络下安装**
1. windows 11
2. node v18.20.1

### node-lib和node-headers缺失
#### 下载：
[node-headers](https://nodejs.org/download/release/v18.20.1/node-v18.20.1-headers.tar.gz)
[node-lib](https://nodejs.org/download/release/v18.20.1/win-x64/node.lib)

#### 配置变量
编辑～/.npmrc文件
> nodedir=c:\node\node-v18.20.1-win-x64\node-v18.20.1

### 报错需要Visual Studio
```
npm ERR! gyp ERR! find VS msvs_version was set from command line or npm config
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! find VS **************************************************************
npm ERR! gyp ERR! find VS You need to install the latest version of Visual Studio
npm ERR! gyp ERR! find VS including the "Desktop development with C++" workload.
npm ERR! gyp ERR! find VS For more information consult the documentation at:
npm ERR! gyp ERR! find VS https://github.com/nodejs/node-gyp#on-windows
npm ERR! gyp ERR! find VS **************************************************************
```

#### 离线安装Visual Studio 2022
1.[脱机安装](https://learn.microsoft.com/zh-cn/visualstudio/install/create-an-offline-installation-of-visual-studio?view=vs-2022) Visual Studio
2.仅离线安装C++
```
vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --includeOptional --lang en-US
```
3.打包下载好的zip包到电脑，执行vs_setup.exe 即可
4.配置环境变量
```GYP_MSVS_VERSION=2022```