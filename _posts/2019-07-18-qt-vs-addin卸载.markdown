---
layout: post
title:  "Qt-vs-addin卸载"
date:   2019-07-18 19:00:00 +0200
categories: qt
---

打开注册表，找到
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\Qt5 Visual Studio Add-in xxx(xxx表示版本号)，将其删除即可
