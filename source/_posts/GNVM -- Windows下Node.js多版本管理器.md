---
layout: w
title: Windows下Node.js多版本管理器
date: 2017-07-31 11:16:57
tags: 

- nodejs
- npm


categories: 

- web前端 
---
# GNVM 使用 Go 语言编写的 Node.js 多版本管理器

GNVM 是一个简单的 Node.js 多版本管理器，类似 nvm nvmw nodist 


```
c:\> gnvm install latest 1.0.0-x86 1.0.0-x64 5.0.0
Start download Node.js versions [5.10.1, 1.0.0, 1.0.0-x86, 5.0.0].
5.10.1: 18% [=========>__________________________________________] 4s
 1.0.0: 80% [==========================================>_________] 40s
1.0...: 50% [==========================>_________________________] 30s
 5.0.1: 100% [==================================================>] 20s
End download.

c:\> gnvm ls
5.1.1 -- latest
1.0.0
1.0.0 -- x86
5.0.0 -- global

c:\> gnvm use latest
Set success, current Node.js version is 5.10.0.

c:\> gnvm update latest
Update success, current Node.js latest version is 5.10.0.
```



> ## 特色


- 单文件，不依赖于任何环境。

- 下载即用，无需配置。

- 彩色日志输出。

- 支持多线程下载。

- 内置 TAOBAO，方便切换，也支持自定义 。

- 支持 NPM 下载/安装/配置。





> ## 下载

- git 用户，请使用
- 
  git clone git@github.com:Kenshin/gnvm-bin.git
  
- go 用户，请使用
- 
  go get github.com/Kenshin/gnvm
  


- curl 用户，请使用
- 
  curl -L https://github.com/Kenshin/gnvm-bin/blob/master/32-bit/gnvm.exe?raw=true -o gnvm.exe

    curl -L https://github.com/Kenshin/gnvm-bin/blob/master/64-bit/gnvm.exe?raw=true -o gnvm.exe
    
    
> ## 安装

- 存在 Node.js 环境
 
    > ##### 下载并解压缩 gnvm.exe 保存到 Node.js 所在的文件夹。


- 不存在 Node.js 环境

    > ##### 下载并解压缩 保存到任意文件夹，并将此文件夹加入到环境变量 Path。  
    
> ## 验证

- 在 cmd 下，输入 gnvm version，如有 版本说明 则配置成功。

    
> ## 功能介绍


```

config       Setter and getter .gnvmrc file
use          Use any the local already exists of Node.js version
ls           Show all [local] [remote] Node.js version
install      Install any Node.js version
uninstall    Uninstall local Node.js version and npm
update       Update Node.js latest version
npm          NPM version management
session      Set any local Node.js version to session Node.js version
search       Search and Print Node.js version detail usage wildcard mode or regexp mode
node-version Show [global] [latest] Node.js version
reg          Add config property [noderoot] to Environment variable [NODE_HOME]
version      Print GNVM version number

```


> ## 入门指南

- gnvm.exe 是一个单文件 exe，无需任何配置，直接使用。


### 更换更快的库 registry

- gnvm.exe 内建了 DEFAULT and TAOBAO 两个库。


```
gnvm config registry TAOBAO

```


### 安装 多个 Node.js

```
gnvm install latest 1.0.0-x86 1.0.0-x64 5.0.0
```

### 卸载本地任意 Node.js 版本

```
gnvm uninstall latest 1.0.0-x86 1.0.0-x64 5.0.0
```


### 切换本地存在的任意版本 Node.js

```
gnvm use 5.10.1
```


### 列出本地已存在的全部 Node.js 版本

```
c:\> gnvm ls
5.1.1 -- latest
1.0.0
1.0.0 -- x86
5.0.0 -- global
```


### 更新本地的 Node.js latest 版本

```
gnvm update latest
```


### 安装 NPM

gnvm 支持安装 npm, 例如：下载最新版的 npm version ，使用 gnvm npm latest。

```
gnvm npm latest
```

### 查询 Node.js 版本
可以使用关键字 * 或者 正则表达式 /regxp/，例如： gnvm search 5.*.* 或者 gnvm search /.10./ 。

```
c:\> gnvm search 5.*.*
Search Node.js version rules [5.x.x] from http://npm.taobao.org/mirrors/node/index.json, please wait.
+--------------------------------------------------+
| No.   date         node ver    exec      npm ver |
+--------------------------------------------------+
1     2016-04-05   5.10.1      x86 x64   3.8.3
2     2016-04-01   5.10.0      x86 x64   3.8.3
3     2016-03-22   5.9.1       x86 x64   3.7.3
4     2016-03-16   5.9.0       x86 x64   3.7.3
5     2016-03-09   5.8.0       x86 x64   3.7.3
6     2016-03-02   5.7.1       x86 x64   3.6.0
7     2016-02-23   5.7.0       x86 x64   3.6.0
+--------------------------------------------------+
```

## 例子

1. 升级本地 Node.js latest 版本。

```
c:\> gnvm config registry TAOBAO
Set success, registry new value is http://npm.taobao.org/mirrors/node/
c:\> gnvm update latest
Notice: local  Node.js latest version is 5.9.1.
Notice: remote Node.js latest version is 5.10.1 from http://npm.taobao.org/mirrors/node/.
Waring: remote latest version 5.10.1 > local latest version 5.9.1.
Waring: 5.10.1 folder exist.
Update success, Node.js latest version is 5.10.1.
```
2. 查看本地 Node.js global and latest 版本。

```
c:\> gnvm node-version
Node.js latest version is 5.10.1.
Node.js global version is 5.10.1
```
3. 验证 .gnvmrc registry 正确性。

```
c:\> gnvm config registry test
Notice: gnvm config registry http://npm.taobao.org/mirrors/node/ valid ................... ok.
Notice: gnvm config registry http://npm.taobao.org/mirrors/node/index.json valid ......... ok.
```
4. 本地不存在 NPM 时，安装当前 Node.js 版本对应的 NPM 版本。

```
c:\ gnvm npm global
Waring: current path C:\xxx\xxx\nodejs\ not exist npm.
Notice: local    npm version is unknown
Notice: remote   npm version is 3.8.3
Notice: download 3.8.3 version [Y/n]? y
Start download new npm version v3.8.3.zip
v3.8.3.zip: 100% [==================================================>] 4s
Start unzip and install v3.8.3.zip zip file, please wait.
Set success, current npm version is 3.8.3.
c:\> npm -v
3.8.7
```
5. 安装 NPM latest 版本。

```
c:\ gnvm npm laltest
Notice: local    npm version is 3.7.3
Notice: remote   npm version is 3.8.7
Notice: download 3.8.7 version [Y/n]? y
Start download new npm version v3.8.7.zip
v3.8.7.zip: 100% [==================================================>] 3s
Start unzip and install v3.8.7.zip zip file, please wait.
Set success, current npm version is 3.8.7.
c:\> npm -v
3.8.7
```









    
