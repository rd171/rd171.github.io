---
layout: post
title:  "qt-在线调试提示Cannot exec xxx Exec format error"
date:   2019-08-22 19:00:00 +0200
categories: matlab
---

### 1、原因  
在线调试目录下执行程序未生成、或生成错误、或权限不够。  


### 2、测试方法  
进入xx.pro文件中target.path指向的目录，看是否生成了执行程序，使用./xxx命令看是否能启动。

### 3、解决方案  
先删除已存的执行程序，再远程调试生成执行程序，再使用chmod 777命令给执行程序配置权限。  
