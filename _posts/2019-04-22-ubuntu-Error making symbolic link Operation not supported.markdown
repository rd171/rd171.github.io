---
layout: post
title:  "Error making symbolic link Operation not supported"
date:   2019-04-21 21:24:00 +0200
categories: ubuntu
---
#### 1、问题
```
出现这类问题，主要是由于在编译的时候，要用ln去建立一些软链接，而这些文件所在磁盘是NTFS格式，并通过VMWare的vmhgfs被Linux共享的，所以编译会报错。

概括来说，就是因为Windows磁盘是NTFS格式，Linux磁盘是ext4格式，ext4格式支持ln -s软连接，而NTFS不支持。
```
#### 2、方法
```
在VMWare下的Linux中，建立Samba服务，创建新samba用户和共享文件。该共享文件夹对Windows和Linux都可见。

与vmhgfs方式不同的是，此时共享文件夹所在磁盘是ext4格式的，所以ln -s 可行，问题解决
```
