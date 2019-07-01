---
layout: post
title:  "Driver-windbg更改路径后下次启动被还原问题"
date:   2019-07-01 19:00:00 +0200
categories: Driver
---
#### 原因
windbg有workspace概念，软件参数跟workspace挂钩

#### 方法
改完参数选择：File -> Save Workspace，下次启动就不会还原了。
