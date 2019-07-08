---
layout: post
title:  "Driver-DRIVER_VERIFIER_DETECTED_VIOLATION (c4)."
date:   2019-07-08 19:00:00 +0200
categories: Driver
---
#### 错误
DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 0000000000002000, Code Integrity Issue: The caller specified an executable pool type. (Expected: NonPagedPoolNx)
Arg2: fffff808320f3448, The address in the driver's code where the error was detected.
Arg3: 0000000000000000, Pool Type.
Arg4: 0000000000000000, Pool Tag (if provided).   

#### 原因
https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type   
    
Starting with Windows 8, drivers should allocate most or all of their nonpaged memory from the no-execute (NX) nonpaged pool instead of the executable nonpaged pool. For more information, see the description of the NonPagedPoolNx pool type.     

#### 方法
```
urb = ExAllocatePool(NonPagedPool, sizeof(struct _URB_CONTROL_VENDOR_OR_CLASS_REQUEST));
```
修改为如下:     
```
urb = ExAllocatePool(NonPagedPoolNx, sizeof(struct _URB_CONTROL_VENDOR_OR_CLASS_REQUEST));
```
