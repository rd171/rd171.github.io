---
layout: post
title:  "ubuntu-安装rapidsvn"
date:   2019-11-29 19:00:00 +0200
categories: ubuntu
---
### 1、安装RapidSVN   
```
sudo apt-get install rapidsvn
```

### 2、安装代码比较合并工具Meld
```
sudo apt-get install meld
```

### 3、打开RapidSVN
```
sudo rapidsvn
```
### 4、配置Diff Tool和Merge Tool   
RapidSVN -> View -> Preferences -> Programs   
Standard Editor 填写 gedit   
Standard Explorer 填写 nautilus   
Diff Tool 填写 meld    
Merge Tool 填写 meld   
