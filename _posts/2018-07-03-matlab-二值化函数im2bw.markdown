﻿---
layout: post
title:  "matlab-二值化函数im2bw"
date:   2018-07-03 19:12:00 +0200
categories: Matlab
---

**语法**  
&nbsp;&nbsp;BW = im2bw(I,level)  
&nbsp;&nbsp;BW = im2bw(X,cmap,level)  
&nbsp;&nbsp;BW = im2bw(RGB,level)  

**说明**  
BW = im2bw(I,level) 将灰度图像I转换为二进制图像BW, I中大于level的替换为1，否则替换为0.  
BW = im2bw(X,cmap,level) 通过颜色空间表将X转换为二进制图像.  
BW = im2bw(RGB,level) 将RGB值转换为二进制图像.  


**示例**  
```
data = [0.1 0.2 0.3 0.4 0.5 0.6]
data1= im2bw(data, 0.3)
```
data =  
   0.100000000000000   0.200000000000000   0.300000000000000   0.400000000000000   0.500000000000000   0.600000000000000   
data1 =  
0   0   0   1   1   1  
