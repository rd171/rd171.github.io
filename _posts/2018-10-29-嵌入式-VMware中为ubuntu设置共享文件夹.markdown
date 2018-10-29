---
layout: post
title:  "嵌入式-VMware中为ubuntu设置共享文件夹"
date:   2018-10-29 19:30:00 +0200
categories: 嵌入式
---

**设置**  
1、打开VMware并进入ubuntu系统  
2、在VMware上依次选择：虚拟机(M)->设置->选项->共享文件夹->添加  
3、选择下一步，在主机路径处选择要共享的文件夹，在名称中输入该共享文件夹在Ubuntu系统中显示的名称  

**参看**
1、在ubunttu中选择file  
2、然后选择Devices目录下的computer  
3、进入mnt/hgfs目录就会看见刚才设置的文件夹名称  
