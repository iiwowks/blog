---
layout:     post
title:      "geektime git学习"
date:       2020-08-08
category:   Git
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

![image](/media/post/git-cheatSheet.jpg)

### 配置user信息

```bash
$ git config --global user.name 'your_name'
$ git config --global user.email 'your_email'
$ git config --global --list
```

### config的三个作用域

```bassh
$ git config --local //local 只对某个仓库有效
$ git config --global //global 对当前用户所有仓库有效
$ git config --system  //system 对系统所有登录的用户有效
```

### 建git仓库

1.  把已有的项目代码纳入git管理

```bash
$ cd folder
$ git init
```

2. 新建的项目直接用git管理

```bash
$ cd 某个文件夹
$ git init your_project
$ cd your_project
```

### 暂存区

![](/media/post/git-zancun.png)

```bash
$ git status // 查看当前状态
$ git add xxx.html images  // 添加文件或文件夹到暂存区
$ git commit -m 'Add xxx + img'
$ git commit -am 'xxx'
$ git log  // 查看git历史
$ git add -u // 已被git管理的文件全部提交到暂存区

$ git mv readme readme.md // 重命名
$ git reset --hard  // 清理暂存区和工作区
$ git log --oneline  // git log显示为一列
$ git log --oneline --all -n4 --graph
$ git log -n4 //查看最近4次历史

```

### .git文件夹

```
$ ls -al
total 26
drwxr-xr-x 1 IIWOWKS 197609    0  8月  3 17:21 ./
drwxr-xr-x 1 IIWOWKS 197609    0  7月 29 10:30 ../
-rw-r--r-- 1 IIWOWKS 197609    5  7月 26 12:02 COMMIT_EDITMSG
-rw-r--r-- 1 IIWOWKS 197609  302  7月 26 12:03 config   /*存放仓库配置信息*/
-rw-r--r-- 1 IIWOWKS 197609   73  7月 26 10:20 description
-rw-r--r-- 1 IIWOWKS 197609   97  7月 28 16:29 FETCH_HEAD
-rw-r--r-- 1 IIWOWKS 197609  132  8月  3 17:21 gitk.cache
-rw-r--r-- 1 IIWOWKS 197609   23  7月 26 10:20 HEAD  /* 当前项目工作在哪个分支上面*/
drwxr-xr-x 1 IIWOWKS 197609    0  7月 26 10:21 hooks/
-rw-r--r-- 1 IIWOWKS 197609 1418  7月 26 12:02 index
drwxr-xr-x 1 IIWOWKS 197609    0  7月 26 10:20 info/
drwxr-xr-x 1 IIWOWKS 197609    0  7月 26 10:22 logs/
drwxr-xr-x 1 IIWOWKS 197609    0  7月 26 12:02 objects/
drwxr-xr-x 1 IIWOWKS 197609    0  7月 26 12:03 refs/
```
在`.git/refs/ `文件夹下
```
drwxr-xr-x 1 IIWOWKS 197609 0  7月 26 12:03 ./
drwxr-xr-x 1 IIWOWKS 197609 0  8月  3 17:48 ../
drwxr-xr-x 1 IIWOWKS 197609 0  7月 26 12:02 heads/   /*分支,一个独立的开发空间*/
drwxr-xr-x 1 IIWOWKS 197609 0  7月 26 12:03 remotes/
drwxr-xr-x 1 IIWOWKS 197609 0  7月 26 10:20 tags/    /*标签,项目的里程碑*/
```
在`.git/refs/heads/`文件夹下
```
$ cat master
67e670c799f97ffa62a09c57eaf0477726f2beb6   /*40位哈希值*/
```

### 对象

* `commit`对象相当于一整个项目（文件、目录）的快照
* `tree`对象相当于一个文件夹
* `blob`对象相当于一个文件
![image-commit](/media/post/git-commit.png)

### 分支

![image](/media/post/git-fenzhi.png)

```bash
$ gitk --all // gitk图形界面工具查看视图
$ git branch  -v // 查看分支
$ git branch -d fix_readme  //删除分支
$ git checkout master // 切换分支
$ git checkout -b fix_readme master // 基于master的commit创建分支
```

### 修改massage

```bash
$ git commit --amend // 对最近一次提交的massage修改
$ git rebase -i 父亲commit哈希值 // 对之前的commit修改massage
```

## rebase指令

* `git rebase --abort`退出rebase状态

### 修改历史git commit message

1. 命令行中输入`git rebase -i father_id`
2. `i`进入编辑模式
3. 修改 `pick xxxid message` 中的`pick`为`reword`，更改message
4. `esc`退出编辑  `shift + :`
5. 输入`wq!` 按`回车键`

![image](/media/post/git-rebase.png)

> [参考文章1](https://www.jianshu.com/p/5ce5a709ba44)
> [参考文章2](https://www.jianshu.com/p/4a8f4af4e803)