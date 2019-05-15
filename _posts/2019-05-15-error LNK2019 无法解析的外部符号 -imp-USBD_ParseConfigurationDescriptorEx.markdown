---
layout: post
title:  "error LNK2019 无法解析的外部符号 imp_USBD_ParseConfigurationDescriptorEx"

date:   2019-05-15 19:00:00 +0200
categories: 系统
---
#### 原因  
没有链接到Usbd.lib

#### 方法
右键依次击选择属性->配置属性->链接器->输入->附件依赖项，添加Usbd.lib。
