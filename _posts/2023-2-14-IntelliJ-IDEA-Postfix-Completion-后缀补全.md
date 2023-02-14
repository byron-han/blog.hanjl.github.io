---
layout:     post
title:      Postfix Completion 可以让您可以在刚刚键入的表达式周围添加模板代码
subtitle:   IntelliJ IDEA Postfix Completion 
date:       2023-02-14
author:     byron han
header-img: img/2023/postfix-completion.png
catalog: true
tags:
    - IntelliJ IDEA
    - Efficiency
---

> 本文首次发布于 [Byron Han Blog](https://blog.hanjl.com.com/), 作者 [@han(Byron Han)](http://github.com/hanjl7) ,转载请保留原文链接.

### 1、进入设置
File | Settings | Editor | General | Postfix Completion for Windows and Linux

IntelliJ IDEA | Settings | Editor | General | Postfix Completion for macOS

### 2、新增后缀填充
Key: 后缀补充名称  
Minimum language level：支持的JDK版本  
Applicable expression types: 针对的类型  
表达式：  `$EXPR$` 引用的语句 `$END` 光标

![image.png](https://s2.loli.net/2023/02/14/53MFpHanWk8qS92.png)

### 3、推荐短语模版
`$EXPR$.ifs` 判断是否为空
```java
if (StringUtils.isNotBlank($EXPR$)) {
    $END$
}
```
`$EXPR$.list` 快捷list生成
```java
List<$EXPR$> $END$ = new ArrayList<>();
```
`$EXPR$.log` log生成
```java
log.info("$END$:{}",$EXPR$);
```
