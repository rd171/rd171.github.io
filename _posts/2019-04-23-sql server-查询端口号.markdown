---
layout: post
title:  "查询端口号"
date:   2019-04-23 07:15:00 +0200
categories: sql server
---
#### 1、查询命令
```
exec sys.sp_readerrorlog 0, 1, 'listening'
```
