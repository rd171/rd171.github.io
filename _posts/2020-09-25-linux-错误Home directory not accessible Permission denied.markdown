---
layout: post
title:  "linux-错误Home directory not accessible Permission denied"
date:   2020-09-25 19:00:00 +0200
categories: linux
---

### 原因  
home文件夹权限不够

### 方法
```
chown -R $USER:$USER $HOME/
```
