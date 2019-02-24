---
layout: post
title:  "嵌入式-ubuntu安装yocto"
date:   2019-2-20 6:44:00 +0200
categories: 嵌入式
---

###### 嵌入式-ubuntu安装yocto      
###### 1.安装ubuntu 16.04预留120G空间，推荐2G内存  
###### 2.更新
```
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
xz-utils debianutils iputils-ping libsdl1.2-dev xterm
```
###### 3.安装辅助软件   
```
sudo dpkg --configure -a
sudo apt install chrpath
chrpath gawk git makeinfo
```
