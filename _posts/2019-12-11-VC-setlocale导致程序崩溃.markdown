---
layout: post
title:  "VC-setlocale导致程序崩溃"
date:   2019-12-11 19:00:00 +0200
categories: VC
---
### 原因
```
setlocale不能跨线程使用
```

### 方法
```
与setlocale函数相关的还有一个函数，_configthreadlocale：
_configthreadlocale(_ENABLE_PER_THREAD_LOCALE)使setlocale只针对当前线程起作用_configthreadlocale(_DISABLE_PER_THREAD_LOCALE)使setlocale对所有线程的设置都有用(默认值)
默认情况下，调用了setlocale函数设置了区域，即对当前进程的所有线程都有效，所以只需在主线程里面调用一次setlocale，其它线程无需再重复调用。

setlocale函数还需要注意的一点就是:setlocale只能在各自的运行时库里生效
```
