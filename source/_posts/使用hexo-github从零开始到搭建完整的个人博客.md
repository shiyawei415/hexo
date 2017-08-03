---
layout: w
title: 使用hexo+github从零开始到搭建完整的个人博客
date: 2017-07-19 16:16:57
tags: 

- Hexo 
- github

categories: 

- web前端 
---



# 1. 安装Git Bash

### . [下载地址](https://git-for-windows.github.io/)
### . 安装步骤：双击下载好的exe文件，一路next就好啦

### . 安装好后，打开gitbash，查看版本：

### 命令: git version  **文字**
![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/24323927.jpg)

### 然后你就可以在这里发挥你的聪明才智了


# 2. 安装NodeJs

Hexo是基于nodeJS环境的静态博客，里面的npm工具很有用啊，所以还是老老实实把这玩意儿装了吧

### . [下载地址](https://nodejs.org/en/)

### . 安装步骤：反正下载好msi文件后，双击打开安装，也是一路next，不过在Custom Setup这一步记得选 Add to PATH ,这样你就不用自己去配置电脑上环境变量了，装完在按 win + r 快捷键调出运行，然后输入cmd确定，在cmd中输入path可以看到你的node是否配置在里面（环境变量），没有的话你就自由发挥吧。
    
### . 查看版本：

### &emsp;&emsp;  **.** 命令：node -v
![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/8387677.jpg)

### 又到自由发挥的时候了

# 3. 安装hexo

看到这么多安装，千万不要紧张，一定要稳住，别怕，因为后面的东西都是在gitbash中用npm工具安装就好了。


### . 先创建一个文件夹（用来存放所有blog的东西），然后++cd++到该文件夹下。

### . 安装hexo命令：npm i -g hexo

### . 安装完成后，查看版本：

![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/37799597.jpg)

### . 初始化命令：hexo init ，初始化完成之后打开所在的文件夹可以看到以下文件：
![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/47441658.jpg)

### . 解释一下：

### &emsp;&emsp;  **.** node_modules：是依赖包

### &emsp;&emsp;  **.** public：存放的是生成的页面

### &emsp;&emsp;  **.** scaffolds：命令生成文章等的模板

### &emsp;&emsp;  **.** source：用命令创建的各种文章

### &emsp;&emsp;  **.** themes：主题

### &emsp;&emsp;  **.** _config.yml：整个博客的配置

### &emsp;&emsp;  **.** db.json：source解析所得到的

### &emsp;&emsp;  **.** package.json：项目所需模块项目的配置信息


### . 做好这些前置工作之后接下来的就是各种配配配置了。



# 4. 搭桥到github

### . 没账号的创建账号，有账号的看下面。

1. 创建一个repo，名称为++yourname.github.io++其中yourname是你的github名称，按照这个规则创建才有用哦，如下：

![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/60398318.jpg)
![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/15906142.jpg)


# 5. 一步之遥


### . 用编辑器打开你的blog项目，修改_config.yml文件的一些配置(冒号之后都是有一个半角空格的)：


```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```


### . 回到gitbash中，进入你的blog目录，分别执行以下命令：


```
hexo clean
hexo generate
hexo server
```

### 注：hexo 3.0把服务器独立成个别模块，需要单独安装：npm i hexo-server。


### . 打开浏览器输入：http://localhost:4000

### . 接着你就可以遇见天使的微笑了~


# 6. 上传到github

### . 先安装一波：npm install hexo-deployer-git --save（这样才能将你写好的文章部署到github服务器上并让别人浏览到）

### . 执行命令(建议每次都按照如下步骤部署)：


```
hexo clean
hexo generate
hexo deploy
```


### 注意deploy的过程中要输入你的username及passward。

### . 在浏览器中输入http://yourgithubname.github.io就可以看到你的个人博客啦，是不是很兴奋！


### . 感觉gitbash中东西太多的时候输入clear命令清空。



# 7. 绑定个人域名

### . 不想绑定的自行忽略

### . 第一步购买域名：随便在哪个网站买一个就好了，我是在阿里云购买的[shiyawei.com](http://shiyawei.com/)，欢迎访问。

### . 第二步添加CNAME：在项目的source文件夹下新建一个名为CNAME的文件，在里面添加你购买的域名，比如我添加的是[shiyawei.com](http://shiyawei.com/)只能添加一个哦。

### . 到DNS中添加一条记录：

![](http://otbt7qcgu.bkt.clouddn.com//17-7-19/47618043.jpg)

### . 接着再次部署一下，用你购买的域名打开，就可以看到你的博客啦~


# 8 .写文章部分

### . 新建文章：hexo new '文章名'，然后你就可以在source/_posts路径下看到你创建的文章啦，编辑完成之后按照前面说的方式部署，在浏览器刷新就能看到你的文章了。

### . [关于具体的文章编辑你可以看下[官网的介绍](https://hexo.io/zh-cn/docs/writing.html)

### . 至于markdown，可以自行发挥啦~

