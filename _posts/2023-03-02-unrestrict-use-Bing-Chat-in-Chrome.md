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

```json
{
	"request": [
		{
			"enable": false,
			"name": "必应中文  >> 英文",
			"ruleType": "redirect",
			"matchType": "regexp",
			"pattern": "^https?://cn\\.bing\\.com/(.*)",
			"exclude": "",
			"isFunction": false,
			"action": "redirect",
			"to": "https://www.bing.com/$1&setmkt=en-US",
			"group": "bing"
		}
	],
	"sendHeader": [
		{
			"enable": true,
			"name": "必应 Chat 代理：Edge 浏览器",
			"ruleType": "modifySendHeader",
			"matchType": "regexp",
			"pattern": "^http(s?)://(.*)\\.bing\\.com/(.*)",
			"exclude": "",
			"isFunction": false,
			"action": {
				"name": "sec-ch-ua",
				"value": "\"Chromium\";v=\"116\", \"Not)A;Brand\";v=\"24\", \"Microsoft Edge\";v=\"116\""
			},
			"group": "bing"
		},
		{
			"enable": true,
			"name": "必应 Chat 代理：Edge 浏览器_user-agent",
			"ruleType": "modifySendHeader",
			"matchType": "regexp",
			"pattern": "^http(s?)://(.*)\\.bing\\.com/(.*)",
			"exclude": "",
			"isFunction": false,
			"action": {
				"name": "user-agent",
				"value": " Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36 Edg/116.0.1938.54"
			},
			"group": "bing"
		}
	],
	"receiveHeader": [],
	"receiveBody": []
}
```

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

