---
layout: post
title:  "arm-移植sqlite"
date:   2020-03-09 19:00:00 +0200
categories: arm
---
### 1、下载sqlite源码，路径如下
```
https://www.sqlite.org/2020/sqlite-autoconf-3310100.tar.gz
```
### 2、解压
```
tar -zxvf sqlite-autoconf-3310100.tar.gz
```
### 3、进入sqlite源码目录
```
cd /home/kevin/Downloads/sqlite-autoconf-3310100
```
### 5、导入ARM板的SDK编译环境
```
. /opt/phytec-yogurt/BSP-Yocto-i.MX6-PD18.1.1/environment-setup-cortexa9hf-neon-phytec-linux-gnueabi
```
本例使用的phytec公司的cortexa9板子，SDK安装在Ubuntu系统的/opt/phytec-yogurt目录中，所以使用上面的路径。注意：“. /opt/”点号与后面的斜杠有一个空格   
### 6、建立编译生成目录
```
sudo mkdir build_dir
sudo chmod -R 777 build_dir
```
### 7、编译
```
./configure --prefix=//home/kevin/Downloads/sqlite-autoconf-3310100/build_dir --host=arm-linux
```
### 8、编译
```
make
```
### 9、生成
```
make install
```
### 10、移植到目标机器
将bin文件夹中的文件拷贝到开发板的/bin中，并将lib中的文件拷贝到开发板的/lib中   
### 12、在目标机器上建立连接
```
cd /lib
ln -s libsqlite3.so.0.8.6 libsqlite3.so.0
ln -s libsqlite3.so.0.8.6 libsqlite3.so
```
### 13、检验是否安装成功
输入以下命令  
```
sqlite3  
```
成功则会出现如下提示   
```
SQLite version 3.31.1 2020-01-27 19:55:54
```
### 14、检验数据库
```
sqlite3
.open /usr/bin/usrdb.db
go
select * from TabPatiInfo
go
```
