---
layout: post
title:  "samba配置"
date:   2019-04-21 20:08:00 +0200
categories: ubuntu
---
#### 1、更新源列表
```
sudo apt-get update
```
#### 2、安装samba
```
sudo apt-get install samba samba-common
```
#### 3、新建共享目录并设置权限
```
sudo mkdir /home/share
sudo chmod 777 /home/share
```
#### 5、打开配置文件smb.conf
```
sudo gedit /etc/samba/smb.conf
```
#### 6、修改配置文件smb.conf
```
# Cap the size of the individual log files (in KiB).
    max log size = 1000
增加如下内容，表示需要输入账号和密码才能访问共享目录
    security = user

在文件末尾增加如下内容
[myshare]
comment=my share directory
path=/home/share
browseable=yes
writable=yes
```
#### 7、新建访问共享资源的用户和设置密码
```
sudo useradd smbuser
sudo smbpasswd -a smbuser
sudo service smbd restart
```
#### 8、查看ubuntu系统中的ip
```
ifconfig
```
#### 9、用第8步中的ip访问共享名为myshare的共享目录，用户名为smbuser
```
在"运行"窗口中输入"\\192.168.1.4"-->回车-->双击打开myshare-->回车-->输入用户名和密码-->回车-->访问成功。
```
