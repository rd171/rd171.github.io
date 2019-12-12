---
layout: post
title:  "ubuntu-ubuntu下qt集成svn"
date:   2019-12-12 19:00:00 +0200
categories: ubuntu
---
### 1、安装subversion
```
sudo apt-get install subversion subversion-tools
```

### 2、qt配置subversion
```
QT Creator -> Tools -> options -> Version Control -> Subversion   

Subversion command:/usr/bin/svn   
Username:xxxx
Passowrd:xxxx
```

### 3、subversion支持.a .so文件
```
1）打开/etc/subversion/config文件   
2）查找global-ignores 字段，即可看到下面有个 global-ignores 键名   
3）把 .so .so.[0-9]* *.a 也去掉
```

### 4、qt checkout仓库
```
QT Creator -> File -> New File or Project -> Import Project -> Subversion Checkout -> Choose
```
