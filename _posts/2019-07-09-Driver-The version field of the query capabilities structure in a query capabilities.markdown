---
layout: post
title:  "Driver-The version field of the query capabilities structure in a query capabilities"
date:   2019-07-09 19:00:00 +0200
categories: Driver
---
#### 错误

DRIVER_VERIFIER_IOMANAGER_VIOLATION (c9)   
The IO manager has caught a misbehaving driver.   
Arguments:   
Arg1: 0000000000000233, The version field of the query capabilities structure in a query capabilities IRP was not properly initialized.   
Arg2: fffff80237bca1c9, The address in the driver's code where the error was detected.   
Arg3: ffff820a8feb2b80, IRP address.   
Arg4: 0000000000000000    

#### 方法
```
NTSTATUS
WDM_QueryCapabilities(
	IN PDEVICE_OBJECT			pdoDeviceObject,
	IN PDEVICE_CAPABILITIES		DeviceCapabilities
	)
{
	PIO_STACK_LOCATION nextStack;
	PIRP irp;
	NTSTATUS ntStatus;
	KEVENT event;

	PAGED_CODE();

	irp = IoAllocateIrp(pdoDeviceObject->StackSize, FALSE);
	// Added by ForHi 20190809
	irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

	if(!irp){
		return STATUS_INSUFFICIENT_RESOURCES;
	}

	nextStack = IoGetNextIrpStackLocation(irp);
	nextStack->MajorFunction = IRP_MJ_PNP;
	nextStack->MinorFunction = IRP_MN_QUERY_CAPABILITIES;

	// init an event to tell us when the completion routine's been called
	KeInitializeEvent(&event, NotificationEvent, FALSE);

	// Set a completion routine so it can signal our event when
	//  the next lower driver is done with the Irp
	IoSetCompletionRoutine(irp,
	                       WDM_IrpCompletionRoutine,			// ->WDMpnp.c: 1
						   &event,		// pass the event as Context to completion routine
						   TRUE,		// invoke on success
						   TRUE,		// invoke on error
						   TRUE);		// invoke on cancel of the Irp

	// Set our pointer to the DEVICE_CAPABILITIES struct
	nextStack->Parameters.DeviceCapabilities.Capabilities = DeviceCapabilities;

	ntStatus = IoCallDriver(pdoDeviceObject, irp);
	if(ntStatus==STATUS_PENDING){
		// wait for irp to complete
		KeWaitForSingleObject(
			&event,
			Suspended,
			KernelMode,
			FALSE,
			NULL);
	}
	IoFreeIrp(irp);
	WDM_KdPrint( DBGLVL_DEFAULT,("Passed WDM_QueryCapabilities()\n"));

	return ntStatus;
}
```
修改为如下:     
```
NTSTATUS
WDM_QueryCapabilities(
	IN PDEVICE_OBJECT			pdoDeviceObject,
	IN PDEVICE_CAPABILITIES		DeviceCapabilities
	)
{
	PIO_STACK_LOCATION nextStack;
	PIRP irp;
	NTSTATUS ntStatus;
	KEVENT event;

	PAGED_CODE();

	irp = IoAllocateIrp(pdoDeviceObject->StackSize, FALSE);
	// Added by ForHi 20190809
	irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

	if(!irp){
		return STATUS_INSUFFICIENT_RESOURCES;
	}

	nextStack = IoGetNextIrpStackLocation(irp);
	nextStack->MajorFunction = IRP_MJ_PNP;
	nextStack->MinorFunction = IRP_MN_QUERY_CAPABILITIES;

	// init an event to tell us when the completion routine's been called
	KeInitializeEvent(&event, NotificationEvent, FALSE);

	// Set a completion routine so it can signal our event when
	//  the next lower driver is done with the Irp
	IoSetCompletionRoutine(irp,
	                       WDM_IrpCompletionRoutine,			// ->WDMpnp.c: 1
						   &event,		// pass the event as Context to completion routine
						   TRUE,		// invoke on success
						   TRUE,		// invoke on error
						   TRUE);		// invoke on cancel of the Irp

	// Set our pointer to the DEVICE_CAPABILITIES struct
	RtlZeroMemory(DeviceCapabilities, sizeof(DEVICE_CAPABILITIES));
	DeviceCapabilities->Size = sizeof(DEVICE_CAPABILITIES);
	DeviceCapabilities->Version = 1;
	DeviceCapabilities->Address = -1;
	DeviceCapabilities->UINumber = -1;
	nextStack->Parameters.DeviceCapabilities.Capabilities = DeviceCapabilities;

	ntStatus = IoCallDriver(pdoDeviceObject, irp);
	if(ntStatus==STATUS_PENDING){
		// wait for irp to complete
		KeWaitForSingleObject(
			&event,
			Suspended,
			KernelMode,
			FALSE,
			NULL);
	}
	IoFreeIrp(irp);
	WDM_KdPrint( DBGLVL_DEFAULT,("Passed WDM_QueryCapabilities()\n"));

	return ntStatus;
}
```
