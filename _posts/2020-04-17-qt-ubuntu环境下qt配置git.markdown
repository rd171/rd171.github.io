---
layout: post
title:  "qt-ubuntu环境下qt配置git"
date:   2020-04-17 19:00:00 +0200
categories: qt
---
### 1、Ubuntu下安装git
```
apt install git
```

### 2、Clone源码
```
git clone http://192.168.1.xxx:20200/chenzm/bm-7i.git
```
之后会依次提示输入用户名和密码   

### 3、QtCreator配置git
1、启动qtCreator   
2、Tools -> Options -> Prepend to PATH输入/usr/bin/
3、打开Clone源码   

### 4、QtCreator提交代码
1、提交到本地库:Tools -> Git -> Local Repository -> Commit   
2、提交到远程库:Tools -> Git -> Remote Repository -> Pull Push   

### 5、QtCreator更新代码
Tools -> Git -> Remote Repository -> Pull

### 6、QtCreator更新删除的文件
Tools -> Git -> Local Repository -> Reset
