---
layout: post
title:  "matlab-读取tdms文件"
date:   2019-08-12 19:00:00 +0200
categories: matlab
---

### 1、convertTDMS

[ConvertedData,ConvertVer,ChanNames]=convertTDMS(SaveConvertedFile,filename)

输入：

SaveConvertedFile（必填）- 确定是否创建MAT文件的逻辑标志（true / false）。如果为0，则不创建MAT文件，如果为1，创建MAT文件，MAT文件的名称与'filename'相同，只是'TDMS'文件扩展名被替换为'MAT'。 MAT文件保存在同一文件夹中，将在不发出警告的情况下覆盖现有文件。 MAT文件包含所有输出变量。

filename（选填） - 要转换的文件名（完全定义）。如果未提供，则会向用户提供“文件打开”对话框以导航到文件。 可以是用于批量转换的单元格数组。

输出：

ConvertedData（必填） - 所有数据对象的结构。

ConvertVer（选填） - 此函数的版本号。

ChanNames（选填） - 通道名称的单元数组。

GroupNames（选填） - 组名称的单元格数组。

ci（选填） - 通道索引的结构（通道的所有信息都驻留在文件中的索引）。

此文调用的方法是：

data=convertTDMS(0,'simple_test.tdms');

2015-02-05,100k,UI1.tdms为样本，不存储为mat格式文件，因为直接存储为mat格式，将会是struct格式，复杂不直观，将在后续的步骤中逐渐抽出所需数据。

### 2、struct2mat.m

使用方法极为简单

data3 = struct2mat(data3);

这里强调此函数的原因是由于matlab中没有直接将结构体数据转换成mat的内置函数，只有自己去找一个了。

当你使用save保存数据后，需要使用load指令上传数据，上传的数据是一个1*1的结构体，需要转换成mat格式方便数据处理。

### 代码获取方法
[convertTDMS]

[convertTDMS]:/20190812matlab-读取tdms文件/ConvertTDMS.rar
