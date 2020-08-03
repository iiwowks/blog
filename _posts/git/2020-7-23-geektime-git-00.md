---
layout:    post
title:     "git learn"
date:      2020-08-02
category:  Git
author:    iiwowks
published: true
syntaxhighlight: false
---

### 配置user信息

```
git config --global user.name 'name'
git config --global user.email 'email'
git config --global --list
```

### config的三个作用域

```
git config --local //local 只对某个仓库有效
git config --global //global 对当前用户所有仓库有效
git config --system  //system 对系统所有登录的用户有效
```

### 建git仓库

* 把已有项目代码纳入git管理

```
cd folder
git init
```

* 新建项目直接用代码管理

```
cd 某个文件夹
git init your_project
cd your_project
```

