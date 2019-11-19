---
layout: post
title:  "matlab-matlab生成色条值供应用程序使用"
date:   2019-11-19 19:00:00 +0200
categories: qt
---
### matlab代码   
```
clc;
% 将色阶更改为32
colormap(jet(64));
% 打开颜色编辑器，选择或编辑颜色后点击应用并关闭对话框
% colormapeditor;
% 获取当前颜色条
mycmap = colormap();
% 输出为RGB格式字符串
 for i=length(mycmap(:,1)):-1:1
%     disp(sprintf('RGB(%d,%d,%d),', floor(mycmap(i, 1:1)*255), floor(mycmap(i, 2:2)*255), floor(mycmap(i, 3:3)*255)));
    disp(sprintf('QColor(%d,%d,%d),', floor(mycmap(i, 1:1)*255), floor(mycmap(i, 2:2)*255), floor(mycmap(i, 3:3)*255)));
 end
```
### 运行结果  
```
QColor(127,0,0),
QColor(143,0,0),
QColor(159,0,0),
QColor(175,0,0),
QColor(191,0,0),
QColor(207,0,0),
QColor(223,0,0),
QColor(239,0,0),
QColor(255,0,0),
QColor(255,15,0),
QColor(255,31,0),
QColor(255,47,0),
QColor(255,63,0),
QColor(255,79,0),
QColor(255,95,0),
QColor(255,111,0),
QColor(255,127,0),
QColor(255,143,0),
QColor(255,159,0),
QColor(255,175,0),
QColor(255,191,0),
QColor(255,207,0),
QColor(255,223,0),
QColor(255,239,0),
QColor(255,255,0),
QColor(239,255,15),
QColor(223,255,31),
QColor(207,255,47),
QColor(191,255,63),
QColor(175,255,79),
QColor(159,255,95),
QColor(143,255,111),
QColor(127,255,127),
QColor(111,255,143),
QColor(95,255,159),
QColor(79,255,175),
QColor(63,255,191),
QColor(47,255,207),
QColor(31,255,223),
QColor(15,255,239),
QColor(0,255,255),
QColor(0,239,255),
QColor(0,223,255),
QColor(0,207,255),
QColor(0,191,255),
QColor(0,175,255),
QColor(0,159,255),
QColor(0,143,255),
QColor(0,127,255),
QColor(0,111,255),
QColor(0,95,255),
QColor(0,79,255),
QColor(0,63,255),
QColor(0,47,255),
QColor(0,31,255),
QColor(0,15,255),
QColor(0,0,255),
QColor(0,0,239),
QColor(0,0,223),
QColor(0,0,207),
QColor(0,0,191),
QColor(0,0,175),
QColor(0,0,159),
QColor(0,0,143),
```
