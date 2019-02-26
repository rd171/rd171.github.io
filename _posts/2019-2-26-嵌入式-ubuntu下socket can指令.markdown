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
