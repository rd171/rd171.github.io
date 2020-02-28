---
layout: post
title:  "ubuntu-在ubuntu上交叉编译用于ARM板子的eigen"
date:   2020-02-25 19:00:00 +0200
categories: ubuntu
---
### 1、下载或拷贝eigen代码到指定目录
```
sudo wget http://bitbucket.org/eigen/eigen/get/3.3.5.tar.gz
```
### 2、解压
```
tar -zxvf 3.3.5.tar.gz
```
### 3、安装cmake
```
sudo apt-get install cmake
```
### 4、路径切换到eigen库源码目录
```
cd /opt/eigen
```
### 5、创建编译文件生成目录
```
sudo mkdir build_dir
```
### 6、进入编译文件生成目录
```
cd build_dir
```
### 7、配置CMake
```
sudo cmake ..
```
### 8、编译
```
sudo make
```
### 9、生成
```
sudo make install
```
注意：会自动生成到目录:/usr/local/include/eigen3/

### 10、app中引用eigen库
在xxx.pro文件中增加如下内容：   
```
INCLUDEPATH += ../eigen3
```
注意：无需包含库
