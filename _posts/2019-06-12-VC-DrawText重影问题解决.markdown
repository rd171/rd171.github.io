---
layout: post
title:  "VC-DrawText重影问题解决"
date:   2019-06-12 19:00:00 +0200
categories: VC
---
#### 原因  
画笔背景色造成的
#### 方法
```
m_pMemDC->SetBkMode(OPAQUE);
```
