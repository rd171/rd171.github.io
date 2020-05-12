---
layout: post
title:  "linux系统by lable获取u盘中文名称"
date:   2020-5-11 19:00:00 +0200
categories: qt
---
###问题
在linux系统下插入U盘，会在linux系统的dev/disk/by lable目录下生成u盘的卷标，如果卷标为中文，则会转换为16进制字符串，如下：
```
\xb2\xe2\xca\xd402
```
###方案
原因是linux以gbk编码方式，将其转换为utf-8即可，代码如下:
```
QTextCodec* gbk     = QtextCodec::codecForName("GB18030");
QTextCodec* utf8     = QtextCodec::codecForName("UTF-8");
char szGbk[4]       = {0xb2, 0xe2, 0xca, 0xd4};//汉字“测试”对应的gbk码
QString strUnicode  = gbk->toUnicode(szGbk, 4);
qDebug()<<strUnicode;
```
###utf-8转gbk
```
QTextCodec* gbk     = QtextCodec::codecForName("GB18030");
QTextCodec* utf8     = QtextCodec::codecForName("UTF-8");
QString str = "测试";
QString  unicode = utf8->toUnicode(str.toLocal8Bit());
QByteArray arr=gbk->fromUnicode(unicode);
for(int i=0; i <arr.size();i++)
{
  qDebug("%x",(unsigned char)arr[i]);
}
```
