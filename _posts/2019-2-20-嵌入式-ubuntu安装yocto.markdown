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
apt-get update
```
```
apt-get install wget git-core unzip make gcc g++ build-essentialsubversion sed autoconf automake texi2html texinfo coreutils diffstatpython-pysqlite2 docbook-utils libsdl1.2-dev libxml-parser-perl libgl1-mesa-devlibglu1-mesa-dev xsltproc desktop-file-utils chrpath groff libtool xterm gawkfop
```
###### 3.安装git   
```
sudo apt-get install git
```

###### 4.copy poky 的 morty 稳定分支   
```
git clone -b morty git://git.yoctoproject.org/poky.git
```

###### 5.进入poky目录，然后运行下面的命令为 Yocto 开发环境设置（设置/导出）一些环境变量   
```
source oe-init-build-env
```

###### 6.安装texinfo  
```
sudo apt-get install texinfo
```

###### 7.安装gawk  
```
sudo apt-get install gawk
```

###### 8.安装chrpath  
```
sudo apt-get install chrpath
```

###### 9.修改build/conf/local.conf文件  
默认增加如下行（代表8线程，8cpu）：  
BB_NUMBER_THREADS = '8'  
PARALLEL_MAKE = '-j 8'  

###### 10.执行编译  
```
bitbake core-image-minimal
```

参考：https://blog.csdn.net/masterbee/article/details/78687653  
https://blog.csdn.net/qq_38446366/article/details/79725864
