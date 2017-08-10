---
layout: w
title: javaScript-浏览器版本、操作系统、内核、设备判断
date: 2017-03-15 11:16:57
tags: [javascript,浏览器]


categories: 

- web前端 
---


# javaScript-获取浏览器版本、操作系统、内核、设备信息

1. 先引入[Broeser.js](https://github.com/shiyawei415/myWork/tree/master/demo/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%A3%80%E6%B5%8B)。



2. 调用：

> ### 查看有哪些属性？

```
	var info = new Browser();
	
	
	//页面输出浏览器各个信息：
	document.writeln("浏览器："+info.browser+"<br/>");
	document.writeln("版本："+info.version+"<br/>");
	document.writeln("内核："+info.engine+"<br/>");
	document.writeln("操作系统："+info.os+"<br/>");
	document.writeln("设备："+info.device+"<br/>");
	document.writeln("语言："+info.language+"<br/>");
    
    
    //控制台查看所有浏览器信息
	console.log(info)

```

> ### 移动端和pc端判断

```
	var info = new Browser();
	
	//pc端和移动端判断
	if(info.device == 'PC'){
		alert('pc端')
	}else{
		alert('移动端')
	}

```

> ### 安卓系统和ios判断 或其他系统判断查看（[Broeser.js](https://github.com/shiyawei415/myWork/tree/master/demo/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%A3%80%E6%B5%8B)）代码

```
	var info = new Browser();

	//安卓系统和ios判断
	if(info.os === 'iOS'){
		alert('ios')
	}
	if(info.os === 'Android'){
		alert('Android')
	}
```
