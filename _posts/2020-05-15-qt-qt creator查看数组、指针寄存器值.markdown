---
layout: post
title:  "qt creator查看数组、指针寄存器值"
date:   2020-5-15 19:00:00 +0200
categories: qt
---
### 语法   
变量名@长度   

### 示例
```
char szData[5] = {1, 2, 3, 4, 5};
char* pData    = szData;
```
查看变量szData， 右键选择Insert New Expression Evaluator在弹出的对对话框中输入szData@5   
查看变量pData， 右键选择Insert New Expression Evaluator在弹出的对对话框中输入pData[0]@5   
