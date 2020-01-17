---
layout: post
title:  "ubuntu-svn代码锁定无法更新和提交"
date:   2020-1-16 19:00:00 +0200
categories: ubuntu
---
### 1、进入代码根目录，更改.svn隐藏文件夹权限
```
sudo chmod -R 777 .svn
```
### 2、解除代码锁定
```
sudo svn cleanup
```
### 3、更新代码
```
sudo svn update
```
