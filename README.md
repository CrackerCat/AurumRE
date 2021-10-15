# AurumRE
Reverse engineering of Aurum anti-cheat driver

# Dispatch Routines

```cpp
2: kd> !drvobj Aurum 7
Driver object (ffffc38f2664d6c0) is for:
 \Driver\Aurum

Driver Extension List: (id , addr)

Device Object list:
ffffc38f27034e10  

DriverEntry:   fffff80074885000	Aurum
DriverStartIo: 00000000	
DriverUnload:  fffff80074875360	Aurum
AddDevice:     00000000	

Dispatch routines:
[00] IRP_MJ_CREATE                      fffff80074864450	Aurum+0x14450
[01] IRP_MJ_CREATE_NAMED_PIPE           fffff80074864450	Aurum+0x14450
[02] IRP_MJ_CLOSE                       fffff80074864450	Aurum+0x14450
[03] IRP_MJ_READ                        fffff80074864450	Aurum+0x14450
[04] IRP_MJ_WRITE                       fffff80074864450	Aurum+0x14450
[05] IRP_MJ_QUERY_INFORMATION           fffff80074864450	Aurum+0x14450
[06] IRP_MJ_SET_INFORMATION             fffff80074864450	Aurum+0x14450
[07] IRP_MJ_QUERY_EA                    fffff80074864450	Aurum+0x14450
[08] IRP_MJ_SET_EA                      fffff80074864450	Aurum+0x14450
[09] IRP_MJ_FLUSH_BUFFERS               fffff80074864450	Aurum+0x14450
[0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff80074864450	Aurum+0x14450
[0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff80074864450	Aurum+0x14450
[0c] IRP_MJ_DIRECTORY_CONTROL           fffff80074864450	Aurum+0x14450
[0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff80074864450	Aurum+0x14450
[0e] IRP_MJ_DEVICE_CONTROL              fffff80074864450	Aurum+0x14450
[0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff80074864450	Aurum+0x14450
[10] IRP_MJ_SHUTDOWN                    fffff80074864450	Aurum+0x14450
[11] IRP_MJ_LOCK_CONTROL                fffff80074864450	Aurum+0x14450
[12] IRP_MJ_CLEANUP                     fffff80074864450	Aurum+0x14450
[13] IRP_MJ_CREATE_MAILSLOT             fffff80074864450	Aurum+0x14450
[14] IRP_MJ_QUERY_SECURITY              fffff80074864450	Aurum+0x14450
[15] IRP_MJ_SET_SECURITY                fffff80074864450	Aurum+0x14450
[16] IRP_MJ_POWER                       fffff80074864450	Aurum+0x14450
[17] IRP_MJ_SYSTEM_CONTROL              fffff80074864450	Aurum+0x14450
[18] IRP_MJ_DEVICE_CHANGE               fffff80074864450	Aurum+0x14450
[19] IRP_MJ_QUERY_QUOTA                 fffff80074864450	Aurum+0x14450
[1a] IRP_MJ_SET_QUOTA                   fffff80074864450	Aurum+0x14450
[1b] IRP_MJ_PNP                         fffff8006b544b80	nt!IopInvalidDeviceRequest


Device Object stacks:

!devstack ffffc38f27034e10 :
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffc38f27034e10  \Driver\Aurum      00000000  Aurum

Processed 1 device objects.
```
