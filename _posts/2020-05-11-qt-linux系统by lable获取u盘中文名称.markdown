---
layout: post
title:  "linux系统by lable获取u盘中文名称"
date:   2020-5-11 19:00:00 +0200
categories: qt
---
###问题
在linux系统下插入U盘，会在linux系统的dev/disk/by
```
\xb2\xe2\xca\xd402
```
###方案
原因是linux以gbk编码方式，将其转换为utf-8即可，代码如下:
```
char szGbk[4]       = {0xb2, 0xe2, 0xca, 0xd4};
QString strUnicode  = gbk->toUnicode(szGbk, 4);
qDebug()<<strUnicode;
```
