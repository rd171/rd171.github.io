---
layout: post
title:  "matlab-stairs用法及与plot区别"
date:   2018-08-21 19:12:00 +0200
categories: matlab
---
**语法**  
&nbsp;&nbsp;stairs(Y)  
&nbsp;&nbsp;stairs(X,Y)  
&nbsp;&nbsp;stairs(___,LineSpec)  
&nbsp;&nbsp;stairs(___,Name,Value)  
&nbsp;&nbsp;stairs(ax,___)  
&nbsp;&nbsp;h = stairs(___)  
&nbsp;&nbsp;[xb,yb] = stairs(___)  

**说明**  
stairs(Y)横坐标自动，Y坐标为Y，画阶梯图  
stairs(X,Y)横坐标为X，Y坐标为Y，画阶梯图  
stairs(___,LineSpec)LineSpec为线条样式  

**示例**  
```
X = linspace(0,4*pi,40);
Y = sin(X);

figure
stairs(Y, 'r');
```
效果图  
![image](/img/2018-08-21-matlab-stairs用法及与plot区别/1.bmp "image")

**与plot区别**  
```
x1=0:0.1:1;
data=sin(x1);
hold on;
stairs(data);
x = 1:length(data);
plot(x, data);
hold off;
legend('stairs', 'plot');
```
效果图  
![image](/img/2018-08-21-matlab-stairs用法及与plot区别/2.bmp "image")
