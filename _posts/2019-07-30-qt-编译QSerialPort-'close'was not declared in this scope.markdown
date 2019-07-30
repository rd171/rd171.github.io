---
layout: post
title:  "qt-编译QSerialPort-'close'was not declared in this scope"
date:   2019-07-30 18:43:00 +0200
categories: matlab
---

### 错误
为ARM编译QSerialPort库，报如下错误：  
‘close’ was not declared in this scope  

### 方法
增加头文件  
#include <unistd.h>
