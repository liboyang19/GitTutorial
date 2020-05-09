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
``` bash
$ git init               // Initialized local Git repository
```

将文件添加到缓存区
``` bash
$ git add <file>         // Add file(s) to index
```

提交缓存区的文件
``` bash
$ git commit             // Commit changes in index
```

检查当前的工作树状态
``` bash
$ git status             // Check status of working tree
```

查询历史提交信息
``` bash
$ git log                // Check commit log
```

将本地仓库推送到远程仓库
``` bash
$ git push               // Push to remote repository
```

获得远程仓库最新的版本
``` bash
$ git pull               // Pull latest from remote repository
```

将一个仓库复制到新的目录下
``` bash
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

## 远程仓库

### 1. 创建repo

### 2. 关联本地仓库
新建一个本地仓库
``` bash
echo "# ll" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/liboyang19/ll.git
git push -u origin master
```

或者关联已存在的仓库
``` bash
git remote add origin https://github.com/liboyang19/ll.git
git push -u origin master
```

### 3. 更新

## GitHub workflow

在项目的开始到结束，我们会有两种仓库。一种是源仓库（origin），一种是开发者仓库。

### 源仓库

在项目的开始，项目的发起者构建起一个项目的最原始的仓库，我们把它称为`origin`。有两个作用：
1. 汇总参与该项目的各个开发者的代码
2. 存放趋于稳定和可发布的代码

源仓库应该是受保护的，开发者不应该直接对其进行开发工作。只有项目管理者（通常是项目发起人）能对其进行较高权限的操作。

### 开发者仓库

每个开发者需要把源仓库的“复制”一份，作为自己日常开发的仓库。这个复制，也就是`fork`。

### 分支

永久性分支
* master branch: 主分支
* dev branch: 开发分支

![](https://i.imgur.com/sHxgjmg.jpg)

临时性分支
* feature branch: 功能分支
* release branch: 预发布分支
* hotfix branch: bug 修复分支

![](https://i.imgur.com/vCQ3mYG.jpg)

### 工作流

为了方便演示，这里使用两个GitHub账号，管理员为**Manager660**，开发者为**liboyang19**。

#### Step 1: 创建源仓库

这一步通常由项目发起人操作，建立源仓库，并且初始化两个永久分支`master`和`dev`。

#### Step 2: 开发者fork源仓库

源仓库建立以后，每个开发就可以去复制一份源仓库到自己的github账号中，然后作为自己开发所用的仓库。

#### Step 3: 将自己的开发者仓库下载到本地

``` bash
$ git clone
```

#### Step 4: 构建本地功能分支进行开发

#### Step 5: 向管理员提交 Pull Request

#### Step 6: 管理员测试、合并

实践中摸索，这是一个非常强大的工具，值得学习。