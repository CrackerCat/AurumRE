# AurumRE
Reverse engineering of Aurum anti-cheat driver

# NOTES

### Binary

```
Name: Aurum.sys
Size: 275680 bytes (269 KiB)
CRC32: 6D8C2E97
CRC64: BCFB88FF217CC4C5
SHA256: 49BD8C5CB273E1F15BB27A6BCF6F3DA4147D432103D25182B0592518B0071702
SHA1: 7F5573763DFF163D8B0F0906A671ED9F2D9CA703
BLAKE2sp: 63CF22AA2C704CF32C674318B92F2315AE424A622971F55879EF8FE5FC776B8F
```

- No anti kernel debugger

# IOCTL

### DEVICE

The WIN32 device name is `\\\\.\\Aurum`.

```
2: kd> !drvobj Aurum
Driver object (ffffc38f2664d6c0) is for:
 \Driver\Aurum
```

The device can be opened without any privileges.
Invalid IOCTL requests will resuled in getting last error code `0xE0000001`.

```cpp
hDevice = CreateFileW(L"\\\\.\\Aurum", ...);
DeviceIoControl(hDevice, 0x555); // GetLastError:0xE0000001
```

### DISPATCH ROUTINES

```
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
