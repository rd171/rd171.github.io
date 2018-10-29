---
layout: post
title:  "嵌入式-ubuntu安装sourceInsight"
date:   2018-10-29 19:30:00 +0200
categories: 嵌入式
---

**安装sourceInsight**  
1、进入ubuntu系统命令行，使用命令sudo apt-get install wine安装wine软件。  
2、下载[sourceinsight安装包]，并将安装包拷贝到ubuntu系统中的某个目录。  
3、进入ubuntu系统命令行，并进入sourceinsight安装包所在目录，使用命令$wine InsightSetup.exe（InsightSetup.exe为sourceinsight安装包名称）  
4、安装完成后会自动运行sourceinsight，并要求输入注册码，注册码为：SI3US-361500-17409  

**运行sourceInsight**  
1、选择file菜单  
2、选择home目录，并按组合键 ctrl + h 显示所有文件及文件夹  
3、进入目录：home/.wine/drive_c/program files/source insight3  
4、在Insight3.exe文件上点击右键，选择open with，接着选择Wine Windows ProgramLoader  


[sourceinsight安装包]:/img/20181029-嵌入式-ubuntu安装sourceInsight/sourceinsight.rar
