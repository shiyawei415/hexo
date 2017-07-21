---
layout: w
title: git基本使用
date: 2017-06-19 16:16:57
tags: 

- git
- github

categories: 

- web前端 
---

![](http://otbt7qcgu.bkt.clouddn.com//17-7-20/61395012.jpg)

## git 基本使用




> ##  安装msysgit

下载地址：[msysgit](https://git-for-windows.github.io/)，安装完成后配置系统环境变量，打开git bash，尽量少用图形化工具git gui，推荐使用命令行。

![系统变量配置](http://otbt7qcgu.bkt.clouddn.com//17-7-20/82805025.jpg)

![git bash](http://otbt7qcgu.bkt.clouddn.com//17-7-20/74685843.jpg)

你可以在本地操作git，也可以在远程服务器仓库操作git，例如**github**，这样你就需要配置下**ssh key**，详情请查看官方文档说明[generating-ssh-keys](https://help.github.com/articles/generating-ssh-keys/ "generating-ssh-keys")

> ## git操作

### 1、检出仓库（克隆仓库）

本地克隆：

```
$ git clone git仓库地址

```

远程克隆：

```
$ git clone server仓库地址

```

ssh方式**(推荐)**，例如：

```
$ git clone git@github.com:hcy2367/hcy2367.github.io.git

```

https方式，例如：

```
$ git clone https://github.com/hcy2367/hcy2367.github.io.git

```

### 2、创建新仓库

```
$ git init

```

### 3、添加工作区（working dir）新的或改动的文件到暂存区（Index或stage）

```
$ git add <filename> | --all | -A | .

```

git工作区，暂存区，HEAD区（可以理解为本地仓库master分支的最新版本）关系图：

![gittrees](http://otbt7qcgu.bkt.clouddn.com//17-7-20/19981864.jpg)

### 4、从暂存区删除添加或改动的的文件

```
$ git rm --cached <filename> | *



```

### 5、查看当前仓库状态

执行add、commit操作之前和之后最好都要查看下当前提交的一些状态信息，防止漏添加，错提交

```
$ git status

```

### 6、查看和对比修改的内容

```
$ git diff <filename>

```

### 7、查看提交的历史记录版本（添加参数：–pretty=oneline，用于输出少量信息）

```
$ git log

```

### 8、提交到当前分支master HEAD区

```
$ git commit -m '代码提交信息'

```

### 9、版本回退

HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本HEAD~100，如回退到上一个版本，则命令如下：

```
$ git reset --hard HEAD^

```

其中–hard参数表示撤销工作区与暂存区的修改，回退到指定历史版本，可使用如下命令：

```
$ git reset --hard 20038

```

其中20038为提交版本的前五位ID号（原始：20038c521d4e81aca8ec8bca9f05d50ebb4fb835），查看时可使用如下命令：

```
$ git reflog

```

### 10、撤销修改

丢弃工作区的修改，已添加到暂存区的文件不受影响，**注意：不能少了–参数**，命令如下：

```
$ git checkout -- <filename> | *

撤销所有修改

$ git checkout .

```

把暂存区的修改撤销掉，重新放回工作区，命令如下：

```
$ git reset HEAD <filename> | *

```

### 11、删除文件

删除后再commit到HEAD区，如果误删文件了，可以恢复到该文件的最新版本。

```
$ git rm <filename>

```

### 12、推送到远端仓库

```
$ git push -u origin master | <branch>

```

**-u参数**表示初次推送时把本地的master分支和远程的master分支关联起来；

**如果你还没有克隆现有仓库，并欲将你的本地仓库连接到某个远程服务器**，你可以使用如下命令添加：

```
$ git remote add origin <server>

```

例如这样你就能够将你的改动推送到所添加的服务器上去了：

```
$ git remote add origin git@github.com:hcy2367/hcy2367.github.io.git

```

### 13、分支

![git branch](http://otbt7qcgu.bkt.clouddn.com//17-7-20/38247958.jpg)

创建分支并切换到新建分支：

```
$ git checkout -b <branch>

```

切换回主分支：

```
$ git checkout master

```

列出所有分支：

```
$ git branch

```

列出所有远程分支：

```
$ git branch -a

```

合并指定分支到当前分支（默认使用fast forward方式）：

```
$ git merge <branch>

```

普通模式合并（禁用fast forward，因为该方式合并后看不到历史提交信息）：

```
$ git merge --no-ff -m "merge with no-ff" <branch>

```

删除分支：

```
$ git branch -d <branch>

```

丢弃一个没有被合并过的分支，可以通过如下命令强行删除：

```
$ git branch -D <branch>

```

推送到远端仓库：

```
$ git push origin <branch>

```

### 14、更新与合并

查看远程信息：

```
$ git remote -v

```

从远程获取最新版本到本地仓库，并自动merge到本地分支：

```
$ git pull origin master

```

从远程获取最新版本到本地仓库，不自动merge到本地分支：

```
$ git fetch

```

**合并分支前先到另外一个分支更新代码，然后本地合并后提交到远程仓库；** 当有冲突时，可使用`$ git diff`或`$ git status`命令查看分支的差异，手工解决后，再执行`$ git add <filename>`命令以将它们标记为合并成功。查看提交记录图形信息：

```
$ git log --graph --pretty=oneline --abbrev-commit

```

### 15、标签（可以理解为版本库的快照）

创建标签：

```
$ git tag <tagname>

```

可使用命令如下命令找到历史提交的ID号：

```
$ git log --pretty=oneline --abbrev-commit

```

再打标签：

```
$ git tag v1.0 6224937

```

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：

```
$ git tag -a v1.1 -m "version 1.1 released" 3628164

```

查看标签：

```
$ git tag

```

查看标签信息：

```
$ git show v1.0

```

删除本地标签：

```
$ git tag -d v1.1

```

推送标签到远程：

```
$ git push origin <tagname>

```

一次性推送全部未推送的标签：

```
$ git push origin --tags

```

删除远程标签（先删除本地，再删除对应的远程tag）：

```
$ git tag -d v1.1
$ git push origin :refs/tags/v1.1

```

### 16、丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：

```
$ git fetch origin
$ git reset --hard origin/master

```

### 17、移除所有未跟踪文件（一般会加上参数-df，-d表示包含目录，-f表示强制清除）

```
$ git clean [options]

```

### 18、多人协作的工作模式

*   首先，可以试图用`$ git push origin <branch>`推送自己的修改；
*   如果推送失败，则因为远程分支比你的本地更新，需要先用`$ git pull`试图合并；
*   如果合并有冲突，则解决冲突，并在本地提交；
*   没有冲突或者解决掉冲突后，再用`$ git push origin <branch>`推送就能成功；
*   如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`$ git branch --set-upstream <branch> origin/<branch>`解决即可。

### 19、git工作流程图

说了这么多，来张工作图，可能更加通俗易懂：

![git工作图](http://otbt7qcgu.bkt.clouddn.com//17-7-20/77460517.jpg)

> ## 总结

掌握上面的命令后基本上可以轻松使用git来管理项目和参与团队开发了，当你欣赏到git的过人和可爱之处后，你可能再也不想使用svn来管理代码了，熟悉操作后你就可以遨翔于**github**、**gitcafe**、**gitlab**的天空，为开源生态圈贡献自己的一份力量。不管是**fork**，**star**，**clone**，还是**pull request**，总要尝试下未知的世界。

> 人一定要靠自己

