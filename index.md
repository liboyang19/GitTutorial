今天只是做一个大致的介绍，讲述一些最基本的流程。

## 想象如下场景

有一份很重要的文件，每次更改都要小心翼翼地创建一个副本。
![](https://i.imgur.com/AQOzWlO.jpg)

小组合作完成一个大项目，管理混乱。
![](https://i.imgur.com/CrfWpiy.jpg)

担心硬盘损坏，创建多个副本备份，上传到百度云，或者拷贝到别的移动硬盘等等。

这些都说明，我们需要一个能够管理文件、控制版本且能够方便多人协作的系统。

## 什么是Git&GitHub？

### Git

[Git](https://git-scm.com/)是一种**Version Control System(VCS)**，可以追踪文件的历史更改。

* 分布式版本控制
* 追踪代码历史的足迹
* 对文件snapshots
* 通过`commit`可以决定在什么时候进行snapshot
* 可以访问任何时候的snapshot

### GitHub

Git用来管理本地文件，而GitHub用来管理远程文件，两者结合在一起，就可以实现多人协作开发以及分布式版本管理。

后续会详细介绍GitHub的workflow。

# Git入门

## Git安装

我们首先需要下载安装，选择对应的系统，安装成功后进行验证：
```
git --version
```

如果是Mac或者Linux系统，可以使用默认的Bash终端；如果是Windows系统，可以使用PowerShell，或者同步安装完成的Git Bash。

## 基础概念

### Repositories,仓库

Repository是一个非常重要的概念，我们所有的Git操作都要在一个Repo中进行，比如我们的一个大项目就是一个repo，它可以被Git追踪。

有两种主要的repo：
* **本地仓库** 本地计算机上的项目仓库，供个人使用，对项目版本进行控制。
* **远程仓库** 将仓库上传到远端服务器，尤其是团队合作时非常有用。比如一个GitHub的项目就是一个repo

### 三种主要状态

repo中的文件可以有三种主要的状态：`modified`, `staged`, `committed`.

* **modified**表示你已经对文件进行了修改，但是还没有提交到数据库中
* **staged**表示你已经对修改过的文件做了一个标记，它即将被提交到数据库（即将做一个次snapshot）
* **committed**表示文件已经提交，安全地保存在数据库中

因此就有了Git项目的三个主要部分：the working tree, the staging area, and the Git directory.

![gitstatus](https://git-scm.com/book/en/v2/images/areas.png)

* **The working tree**是项目文件的某个版本检查点。可以把它理解为当前的工作区，就位于磁盘中，可供用户使用和修改。
* **The staging area**称为缓存区，它存储了你要准备提交的信息，在Git的说法中，它也可以叫"index"，但是"staging area"也没有问题，都是同一个事物。
* **The Git directory**存储了项目的所有版本的信息，这部分对用户来说是隐藏的，不用关注。

如果文件的某个版本是在Git directory中的，那么它是**committed**；如果它被修改了并且已经放入缓存区，那么它是**staged**；如果它被修改了，但还没有放入缓存区，那么它是**modified**。

## 基础的Git命令

初始化本地仓库，将某个文件夹变为可以被Git的仓库。
```
$ git init               // Initialized local Git repository
```

将文件添加到缓存区
```
$ git add <file>         // Add file(s) to index
```

提交缓存区的文件
```
$ git commit             // Commit changes in index
```

检查当前的工作树状态
```
$ git status             // Check status of working tree
```

查询历史提交信息
```
$ git log                // Check commit log
```

将本地仓库推送到远程仓库
```
$ git push               // Push to remote repository
```

获得远程仓库最新的版本
```
$ git pull               // Pull latest from remote repository
```

将一个仓库复制到新的目录下
```
$ git clone              // Clone repository into a new folder
```

## 回退版本

面对的场景不同，目的不同，会有不同的命令和处理办法，所以这里先略过，可以查看[这里](https://git-scm.com/book/en/v2)。

## Branch，分支

为了不影响项目的正常使用，在添加新功能，或者修复bug时，都要添加一个新的分支。之后所有的操作都是在分支上进行。这样就可以有效地将稳定版本（master）与不稳定版本（dev）分开，在逻辑上和操作上都是很方便的。

![](https://i.imgur.com/4YAxwz3.jpg)

优点：
* 并行开发
* 保证master的稳定性

等到bug修复，或者新功能添加完成，并且已经确定通过测试，就可以正式上线，即合并到master上。

### 合并冲突

* 针对不同类型的冲突，有不同的解决方法
* 增强代码的逻辑性，实现代码解耦，可以有效减少类似问题的出现。