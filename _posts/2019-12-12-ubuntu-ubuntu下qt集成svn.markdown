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

### 5、subversion操作命令
```
1）添加      
svn　add　文件名
svn add test.php   
2）提交   
svn　ci　-m　“提交备注信息文本“　[-N]　[--no-unlock]　文件名
svn ci -m “提交我的测试用test.php“ test.php
svn ci -m “提交我的测试用test.php“ -N --no-unlock test.php
3）更新
svn　update
svn　update　-r　修正版本　文件名
svn　update　文件名
svn  update
svn  update -r 200 test.cpp
svn  update test.php
4）删除
svn　delete　svn://路径(目录或文件的全路径) -m “删除备注信息文本”
svn delete svn://192.168.1.1/testapp/test.php -m “删除测试文件test.php”
svn　delete　文件名
svn　ci　-m　“删除备注信息文本”
svn delete test.php
svn ci -m “删除测试文件test.php”
5）比较差异
svn　diff　文件名
svn　diff　-r　修正版本号m:修正版本号n　文件名
svn  diff test.php
svn  diff -r 200:201 test.php
```

### 6、qt creator中使用subversion
```
QT Creator -> Tools -> subversion
```
