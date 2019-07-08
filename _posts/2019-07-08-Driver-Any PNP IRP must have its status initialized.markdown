---
layout: post
title:  "Driver-Any PNP IRP must have its status initialized"
date:   2019-07-08 19:00:00 +0200
categories: Driver
---
#### 错误
DRIVER_VERIFIER_IOMANAGER_VIOLATION (c9)
The IO manager has caught a misbehaving driver.
Arguments:
Arg1: 000000000000020e, A PNP IRP has an invalid status. Any PNP IRP must have its status initialized
	to STATUS_NOT_SUPPORTED.
Arg2: fffff8085ec3a17b, The address in the driver's code where the error was detected.
Arg3: ffffed025313cb80, IRP address.
Arg4: 0000000000000000

Debugging Details:
------------------     

#### 方法
```
irp = IoAllocateIrp(pdoDeviceObject->StackSize, FALSE);
```
修改为如下:     
```
irp = IoAllocateIrp(pdoDeviceObject->StackSize, FALSE);
// Added by ForHi 20190808
irp->IoStatus.Status = STATUS_NOT_SUPPORTED;
```
