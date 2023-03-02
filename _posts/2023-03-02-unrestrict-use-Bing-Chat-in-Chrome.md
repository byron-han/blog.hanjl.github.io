---
layout:     post
title:      '解除New Bing在Chrome中的搜索限制'
subtitle:   'Lift Microsoft restrictions and use Bing Chat in Chrome'
date:       2023-03-02
author:     byron han
header-style: text
catalog: true
tags:
- Chrome
- browser
---

### 下载浏览器插件 `Header Editor`
> [Chrome Extension Store](https://chrome.google.com/webstore/detail/header-editor/eningockdidmgiojffjmkdblpjocbhgh)<br>
> [Microsoft Edge Extension Store](https://microsoftedge.microsoft.com/addons/detail/header-editor/djbcdihpmcbpkljpjibeiedjenilallo)

### 添加规则
#### 1.直接访问New Bing
>Match type: Regular expression  
Match rules: ^http(s?)://(www\.)?bing\.com/(.*)  
Execute type: normal  
Header name: x-forwarded-for  
Header value: 8.8.8.8  

![image.png](https://s2.loli.net/2023/03/02/IZMDjtoeJGCc95x.png)

#### 2.在Chrome中使用New Bing

>Match type: Regular expression  
Match rules: ^http(s?)://(.*).bing\.com/(.*)  
Execute type: normal  
Header name: user-agent  
Header value: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36 Edg/110.0.1587.41

![image.png](https://s2.loli.net/2023/03/02/cCSuXl4dKg95QAi.png)

#### 3.Bing设置区域为英语区域

#### 4.Use New Bing
![image.png](https://s2.loli.net/2023/03/02/DgpUiOL2XQFoaEx.png)

