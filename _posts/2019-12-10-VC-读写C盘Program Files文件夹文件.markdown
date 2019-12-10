---
layout: post
title:  "VC-读写C盘Program Files文件夹文件"
date:   2019-12-10 19:00:00 +0200
categories: VC
---
### 方法
```
Solution -> Properties -> Configuration Properties -> Linker -> Manifest File -> UAC Execution Level 更改为：requireAdministrator(/level='requireAdministrator')
```
