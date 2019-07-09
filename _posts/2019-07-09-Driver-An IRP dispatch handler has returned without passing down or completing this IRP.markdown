---
layout: post
title:  "Driver-An IRP dispatch handler has returned without passing down or completing this IRP"
date:   2019-07-09 19:00:00 +0200
categories: Driver
---
#### 错误
DRIVER_VERIFIER_IOMANAGER_VIOLATION (c9)
The IO manager has caught a misbehaving driver.
Arguments:
Arg1: 0000000000000226, An IRP dispatch handler has returned without passing down or completing this IRP,
	or someone forgot to return STATUS_PENDING.
Arg2: fffff80bd7b982b0, The address in the driver's code where the error was detected.
Arg3: ffff818c0aff4a60, IRP address.
Arg4: 0000000000000000    

#### 方法
```
NTSTATUS
_WDM_Write(
	IN PDEVICE_OBJECT DeviceObject,		// pointer to the device object (FDO)
	IN PIRP           Irp				// pointer to an I/O Rquest Packet
	)
{
	NTSTATUS ntStatus;

	WDM_IncrementIoCount(DeviceObject);
	if(wdm_AccessRejected( DeviceObject, Irp, &ntStatus )){			// ->*1
		WDM_KdPrint( DBGLVL_DEFAULT,("**_WDM_Write:Reject!!!\n"));
		return ntStatus;
	}

	ntStatus = USBCL_Write( DeviceObject, Irp );			// ->USBRw: 1
	return ntStatus;
}

```
修改为如下:     
```
NTSTATUS
_WDM_Write(
	IN PDEVICE_OBJECT DeviceObject,		// pointer to the device object (FDO)
	IN PIRP           Irp				// pointer to an I/O Rquest Packet
	)
{
	// Modified by ForHi 20190709 赋初值
	NTSTATUS ntStatus = STATUS_SUCCESS;

	WDM_IncrementIoCount(DeviceObject);
	if(wdm_AccessRejected( DeviceObject, Irp, &ntStatus )){			// ->*1
		WDM_KdPrint( DBGLVL_DEFAULT,("**_WDM_Write:Reject!!!\n"));
		return ntStatus;
	}

	ntStatus = USBCL_Write( DeviceObject, Irp );			// ->USBRw: 1
	return ntStatus;
}

```
