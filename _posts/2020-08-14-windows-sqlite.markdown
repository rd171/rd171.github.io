---
layout: post
title:  "windows-sqlite"
date:   2020-08-14 19:00:00 +0200
categories: arm
---
### 1、下载sqlite源码，路径如下
```
https://www.sqlite.org/2020/sqlite-tools-win32-x86-3320300.zip解压到C盘   
```
### 2、配置
将sqlite-tools-win32-x86-3320300.zip解压到C盘   
将c:\sqlite-tools-win32-x86-3320300添加到环境变量中

### 3、打开数据库
打开cmd   
输入如下命令
```
sqlite3
.open /usr/bin/usrdb.db
go
select * from TabPatiInfo
go
```
### 4、安装可视化工具sqlite studio
下载链接：https://github-production-release-asset-2e65be.s3.amazonaws.com/117119718/24801180-2b12-11ea-9dc5-46cc76f8f7bb?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20200814%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20200814T112928Z&X-Amz-Expires=300&X-Amz-Signature=464e5a61a543731c13449505d08bcc0a88cec16c7306d80d76fdbc2caf479aff&X-Amz-SignedHeaders=host&actor_id=0&repo_id=117119718&response-content-disposition=attachment%3B%20filename%3DSQLiteStudio-3.2.1.zip&response-content-type=application%2Foctet-stream
