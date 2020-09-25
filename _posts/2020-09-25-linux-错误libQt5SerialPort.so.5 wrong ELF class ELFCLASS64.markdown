---
layout: post
title:  "linux-错误libQt5SerialPort.so.5 wrong ELF class ELFCLASS64"
date:   2020-09-25 19:00:00 +0200
categories: linux
---

### 原因  
执行程序为32位，依赖的库为64位

### 方法
将Ubuntu开发机中的/opt/phytec-yogurt/BSP-Yocto-i.MX6-PD18.1.1/sysroots/cortexa9hf-neon-phytec-linux-gnueabi/usr/lib/libQt5SerialPort.so.5.9.7拷贝至目标板的/usr/lib/libQt5SerialPort.so.5
