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
%     disp(sprintf('RGB(%d,%d,%d),', floor(mycmap(i, 1:1)*255), floor(mycmap(i, 1:1)*255), floor(mycmap(i, 2:2)*255)));
    disp(sprintf('QColor(%d,%d,%d),', floor(mycmap(i, 1:1)*255), floor(mycmap(i, 1:1)*255), floor(mycmap(i, 2:2)*255)));
 end
```
### 运行结果  
```
QColor(127,127,0),
QColor(143,143,0),
QColor(159,159,0),
QColor(175,175,0),
QColor(191,191,0),
QColor(207,207,0),
QColor(223,223,0),
QColor(239,239,0),
QColor(255,255,0),
QColor(255,255,15),
QColor(255,255,31),
QColor(255,255,47),
QColor(255,255,63),
QColor(255,255,79),
QColor(255,255,95),
QColor(255,255,111),
QColor(255,255,127),
QColor(255,255,143),
QColor(255,255,159),
QColor(255,255,175),
QColor(255,255,191),
QColor(255,255,207),
QColor(255,255,223),
QColor(255,255,239),
QColor(255,255,255),
QColor(239,239,255),
QColor(223,223,255),
QColor(207,207,255),
QColor(191,191,255),
QColor(175,175,255),
QColor(159,159,255),
QColor(143,143,255),
QColor(127,127,255),
QColor(111,111,255),
QColor(95,95,255),
QColor(79,79,255),
QColor(63,63,255),
QColor(47,47,255),
QColor(31,31,255),
QColor(15,15,255),
QColor(0,0,255),
QColor(0,0,239),
QColor(0,0,223),
QColor(0,0,207),
QColor(0,0,191),
QColor(0,0,175),
QColor(0,0,159),
QColor(0,0,143),
QColor(0,0,127),
QColor(0,0,111),
QColor(0,0,95),
QColor(0,0,79),
QColor(0,0,63),
QColor(0,0,47),
QColor(0,0,31),
QColor(0,0,15),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
QColor(0,0,0),
```
