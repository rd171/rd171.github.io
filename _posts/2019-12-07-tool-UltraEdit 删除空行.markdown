---
layout: post
title:  "tool-UltraEdit 删除空行"
date:   2019-12-7 19:00:00 +0200
categories: ubuntu
---
### 方法
```
打开UltraEdit，ctrl+r弹出替换对话框，点选启用正则表达式
在查找框输入 ^p^p:
在替换框输入 ^p
执行全部替换；
这种方法是对连续的两个回车换行，替换成一个回车换行；如果空行中含有空格或者制表符，则不能处理；
```
