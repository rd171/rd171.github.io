---
layout: post
title:  "ubuntu-sqlite安装"
date:   2020-2-21 19:00:00 +0200
categories: ubuntu
---

### 创建目录
```
mkdir sqlite
```

### 安装sqlite
```
 sudo apt-get install sqlite  sqlite3
```

### 安装SQLite 可视化工具
```
 sudo apt-get install sqlite  sqlitebrowser
```

### 常用命令
```
.tables            //显示数据库中所有的表
.schema            //显示所有的表的创建语句
.schema tableX     //显示表tableX的创建语句
.quit              //退出
```

### 进入数据库
```
sqlite3  test.db
```

### 创建表
```
create table mytable(id,name,age)
go
```

### 插入数据
```
insert into mytable(id,name,age) values(1,"张三","21")
go
```

### 查询表
```
select * from mytable
go
```

### 打开sqlitebrowser
```
打开sqlitebrowser
```
