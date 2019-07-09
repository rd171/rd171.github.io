---
layout: post
title:  "DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)"
date:   2019-07-09 19:00:00 +0200
categories: Driver
---
#### 错误
DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)   
An attempt was made to access a pageable (or completely invalid) address at an interrupt request level (IRQL) that is too high.  This is usually caused by drivers using improper addresses.   
If kernel debugger is available get stack backtrace.   
Arguments:   
Arg1: 0000000000000028, memory referenced   
Arg2: 0000000000000002, IRQL   
Arg3: 0000000000000001, value 0 = read operation, 1 = write operation   
Arg4: fffff803695e7d3e, address which referenced memory    

#### 方法
```
VOID drvTimeoutDPC(
	PKDPC Dpc,
	PVOID DeferredContext,
	PVOID SystemArgument1,
	PVOID SystemArgument2
	)
{
	PDEVICE_OBJECT pDeviceObject = (DEVICE_OBJECT*)DeferredContext;
	NTSTATUS ntStatus = STATUS_SUCCESS;
	PIO_STACK_LOCATION irpStack, nextStack;
	PDEVICE_EXTENSION deviceExtension = pDeviceObject->DeviceExtension;
	PURB urb;
	PIRP irp;
	PMDL mdl;
	PUSBCL_RW_CONTEXT context = NULL;
	PUSBCL_PIPE pipeHandle;
	PFILE_OBJECT fileObject;
	ULONG totalLength = 0, interruptOrBulkinIndex;
	CHAR stackSize;
	CHAR* va;
	NTSTATUS resetPipeStatus;
	KIRQL	oldIrql;
	int		DataSize;

	if (deviceExtension->BulkinComplete == FALSE) {
		goto USBCL_Read_Done;
	}

	interruptOrBulkinIndex = 1;

	pipeHandle = GetPipeHandle(pDeviceObject, 0);
	totalLength = (deviceExtension->BulkinBufferSize & 0xffff);
	va = ExAllocatePool(NonPagedPoolNx, totalLength);

	context = ExAllocatePool(NonPagedPoolNx, sizeof(struct _USBCL_RW_CONTEXT));
	context->pDataBuf = va;
	context->InterruptOrBulkinIndex = interruptOrBulkinIndex;

	irp = NULL;
	urb = NULL;
	mdl = NULL;

	stackSize = (CCHAR)(deviceExtension->TopOfStackDeviceObject->StackSize + 1);
	irp = IoAllocateIrp(stackSize, FALSE);
	// Added by ForHi 20190808
	irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

	if(irp){
		mdl = IoAllocateMdl(va,
							totalLength,
							FALSE,
							FALSE,
							NULL);
		irp->MdlAddress = mdl;
	}

	if (irp->MdlAddress == NULL) {
		IoFreeIrp(irp);
		goto USBCL_Read_Done;
	}
	try {
		MmProbeAndLockPages(irp->MdlAddress,
							KernelMode,
							IoWriteAccess);
	} except(EXCEPTION_EXECUTE_HANDLER) {
		if (irp->MdlAddress != NULL) {
			IoFreeMdl(irp->MdlAddress);
		}
		IoFreeIrp(irp);
		goto USBCL_Read_Done;
	}
	urb = USBCL_BuildAsyncRequest(pDeviceObject,
								  irp,
								  pipeHandle,
								  TRUE);


	if(urb && irp && mdl){
		context->DeviceObject = pDeviceObject;
		context->Urb = urb;
		context->Irp = irp;
		context->Mdl = mdl;
		context->pDataBuf = va;

		nextStack = IoGetNextIrpStackLocation(irp);
		nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
		nextStack->Parameters.Others.Argument1 = urb;
		nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;

		IoSetCompletionRoutine(irp,
							   InterruptReciveCompletion,
							   context,						
							   TRUE,						
							   TRUE,						
							   TRUE);						
		ntStatus = IoCallDriver(deviceExtension->TopOfStackDeviceObject, context->Irp);

	}
	else{
		ntStatus = STATUS_INSUFFICIENT_RESOURCES;
	}

	if(!NT_SUCCESS(ntStatus)){
		if(pipeHandle && WDM_CanAcceptIoRequests(pDeviceObject)){
			resetPipeStatus = STATUS_SUCCESS;
			if(!NT_SUCCESS(resetPipeStatus)){
				resetPipeStatus = USBCL_ResetDevice(pDeviceObject);			
			}
		}
	}
	goto USBCL_Read_Done;

USBCL_Read_Done:
	SetWaitTimer(&deviceExtension->BulkinTimer);
	return;
}
```
修改为如下:     
```
VOID drvTimeoutDPC(
	PKDPC Dpc,
	PVOID DeferredContext,
	PVOID SystemArgument1,
	PVOID SystemArgument2
	)
{
	PDEVICE_OBJECT pDeviceObject = (DEVICE_OBJECT*)DeferredContext;
	NTSTATUS ntStatus = STATUS_SUCCESS;
	PIO_STACK_LOCATION irpStack, nextStack;
	PDEVICE_EXTENSION deviceExtension = pDeviceObject->DeviceExtension;
	PURB urb;
	PIRP irp;
	PMDL mdl;
	PUSBCL_RW_CONTEXT context = NULL;
	PUSBCL_PIPE pipeHandle;
	PFILE_OBJECT fileObject;
	ULONG totalLength = 0, interruptOrBulkinIndex;
	CHAR stackSize;
	CHAR* va;
	NTSTATUS resetPipeStatus;
	KIRQL	oldIrql;
	int		DataSize;

	if (deviceExtension->BulkinComplete == FALSE) {
		goto USBCL_Read_Done;
	}

	interruptOrBulkinIndex = 1;

	pipeHandle = GetPipeHandle(pDeviceObject, 0);
	totalLength = (deviceExtension->BulkinBufferSize & 0xffff);
	va = ExAllocatePool(NonPagedPoolNx, totalLength);
	// Added by ForHi 20190709
	if ( NULL  == va )
		goto USBCL_Read_Done;

	context = ExAllocatePool(NonPagedPoolNx, sizeof(struct _USBCL_RW_CONTEXT));
	// Added by ForHi 20190709
	if ( NULL == context )
	{
		ExFreePool(va);
		goto USBCL_Read_Done;
	}
	context->pDataBuf = va;
	context->InterruptOrBulkinIndex = interruptOrBulkinIndex;

	irp = NULL;
	urb = NULL;
	mdl = NULL;

	stackSize = (CCHAR)(deviceExtension->TopOfStackDeviceObject->StackSize + 1);
	irp = IoAllocateIrp(stackSize, FALSE);
	// Added by ForHi 20190709
	if ( NULL == irp)
	{
		ExFreePool(va);
		ExFreePool(context);
		goto USBCL_Read_Done;
	}
	// Added by ForHi 20190808
	irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

	if(irp){
		mdl = IoAllocateMdl(va,
							totalLength,
							FALSE,
							FALSE,
							NULL);
		irp->MdlAddress = mdl;
	}

	if (irp->MdlAddress == NULL) {
		ExFreePool(va);
		ExFreePool(context);
		IoFreeIrp(irp);
		goto USBCL_Read_Done;
	}
	try {
		MmProbeAndLockPages(irp->MdlAddress,
							KernelMode,
							IoWriteAccess);
	} except(EXCEPTION_EXECUTE_HANDLER) {
		if (irp->MdlAddress != NULL) {
			IoFreeMdl(irp->MdlAddress);
		}
		ExFreePool(va);
		ExFreePool(context);
		IoFreeIrp(irp);
		goto USBCL_Read_Done;
	}
	urb = USBCL_BuildAsyncRequest(pDeviceObject,
								  irp,
								  pipeHandle,
								  TRUE);


	if(urb && irp && mdl){
		context->DeviceObject = pDeviceObject;
		context->Urb = urb;
		context->Irp = irp;
		context->Mdl = mdl;
		context->pDataBuf = va;

		nextStack = IoGetNextIrpStackLocation(irp);
		nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
		nextStack->Parameters.Others.Argument1 = urb;
		nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_URB;

		IoSetCompletionRoutine(irp,
							   InterruptReciveCompletion,
							   context,						
							   TRUE,						
							   TRUE,						
							   TRUE);						
		ntStatus = IoCallDriver(deviceExtension->TopOfStackDeviceObject, context->Irp);

	}
	else{
		ntStatus = STATUS_INSUFFICIENT_RESOURCES;
	}

	if(!NT_SUCCESS(ntStatus)){
		if(pipeHandle && WDM_CanAcceptIoRequests(pDeviceObject)){
			resetPipeStatus = STATUS_SUCCESS;
			if(!NT_SUCCESS(resetPipeStatus)){
				resetPipeStatus = USBCL_ResetDevice(pDeviceObject);			
			}
		}
	}
	goto USBCL_Read_Done;

USBCL_Read_Done:
	SetWaitTimer(&deviceExtension->BulkinTimer);
	return;
}
```
