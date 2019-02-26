---
layout: post
title:  "嵌入式-ubuntu下socket can指令"
date:   2019-2-26 19:30:00 +0200
categories: 嵌入式
---

###### 查看can设备列表  
```
ifconfig -a
```
###### 将设备can0设置为can类型    
```
ip link set can0 type can
```
###### 查看can0的状态  
```
ip -details -statistics link show can0
```    
###### 关闭设备can0
```
ip link set can0 down
```

###### 设置设备can0波特率为1Mbit/s
```
ip link set can0 up type can bitrate 1000000
```
###### 打开设备can0
```
ip link set can0 up
```
###### 设备can0接收数据(按CTRL + C终止接收)
```
candump can0
```
###### 设备can0发送数据(帧ID为:123，数据为:abcd,帧格式为:标准,帧类型:数据帧)
```
cansend can0 123#abcd
```
###### 设备can0发送数据(帧ID为:12300000，数据为:abcd,帧格式为:扩展帧,帧类型:数据帧)
```
cansend can0 12300000#abcd
```
###### 设备can0发送数据(帧ID为:123，数据为:abcd,帧格式为:标准帧,帧类型:远程帧)
```
cansend can0 123#Rabcd
```
