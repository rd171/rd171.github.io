---
layout: post
title:  "qt-ubuntu下qt无法输入中文"
date:   2019-12-13 19:00:00 +0200
categories: ubuntu
---

### 1、安装搜狗输入法
1）添加FCITX仓库
```
sudo add-apt-repository ppa:fcitx-team/nightly
```
2）更新仓库
```
sudo apt-get update
```

3）安装fcitx输入法框架
```
sudo apt-get install fcitx
```
4）ubuntu系统配置
system settings->language support->install/remove languages，在弹出的菜单中选择Chinese(simplified),点击apply  

system settings->language support->keyboard input method system，选择fcitx

### 2、Qt Creator支持搜狗输入法配置
1）进入qt安装目录
```
cd /opt/Qt5.9.6/Tools/QtCreator/lib/Qt/plugins/platforminputcontexts
```
2）将搜狗输入法插件库到qt插件库目录中
```
 cp /usr/lib/x86_64-linux-gnu/qt5/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so .
```
3）配置qt插件库中搜狗输入法插件库文件权限
```
chomd +x libfcitxplatforminputcontextplugin.so
```
