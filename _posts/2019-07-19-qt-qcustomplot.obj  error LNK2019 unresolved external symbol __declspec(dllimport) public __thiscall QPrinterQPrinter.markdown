---
layout: post
title:  "qt-qcustomplot.obj  error LNK2019 unresolved external symbol __declspec(dllimport) public __thiscall QPrinterQPrinter"
date:   2019-07-19 19:00:00 +0200
categories: qt
---
### 解决方案  
项目属性 -> 配置(C): Debug”“项目属性 -> 配置属性 -> 链接器 -> 输入 -> 附加依赖项”里面添加“Qt5PrintSupportd.lib”；“项目属性 -> 配置(C): Release”“项目属性 -> 配置属性 -> 链接器 -> 输入 -> 附加依赖项”里面添加“Qt5PrintSupport.lib”
