---
layout: post
title:  ""
date:   qt-QLabel不支持text-align
categories: qt
---
### 1、问题
QLabel不支持text-align,见帮助手册
```
The alignment of text and icon within the contents of the widget.
If this value is not specified, it defaults to the value that depends on the native style.
Example:

  QPushButton {
      text-align: left;
  }

This property is currently supported only by QPushButton and QProgressBar.
```

### 2、方法
使用QLabel的setAlignment方法
