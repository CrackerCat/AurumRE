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

```
# of Bytes: 258184
# of Memory Blocks: 10
# of Instructions: 0
# of Defined Data: 1227
# of Functions: 0
# of Symbols: 33
# of Data Types: 54
# of Data Type Categories: 4

Comments: Aurum Driver
CompanyName: Activision Blizzard, Inc.
Compiler: visualstudio:unknown

Created With Ghidra Version: 10.0.1
Executable Format: Portable Executable (PE)

ProductName: Aurum Driver
ProductVersion: V1.0.0.0
Relocatable: true
PDB Age: 1
PDB File: Aurum.pdb
PDB GUID: 7db1926f-b5eb-40da-9f5e-47207d60bfca
PDB Version: RSDS
Section Alignment: 4096
```

See full IDA disassembly at [ida_disasm_full.asm](ida_disasm_full.asm)

- No anti kernel debugger

### PE Sections

```
.text IMAGE_SCN_CNT_CODE | IMAGE_SCN_MEM_NOT_PAGED | IMAGE_SCN_MEM_EXECUTE | IMAGE_SCN_MEM_READ
.rdata IMAGE_SCN_CNT_INITIALIZED_DATA | IMAGE_SCN_MEM_NOT_PAGED | IMAGE_SCN_MEM_READ | IMAGE_SCN_MEM_WRITE
.data IMAGE_SCN_CNT_INITIALIZED_DATA | IMAGE_SCN_MEM_NOT_PAGED | IMAGE_SCN_MEM_READ | IMAGE_SCN_MEM_WRITE
.pdata IMAGE_SCN_CNT_INITIALIZED_DATA | IMAGE_SCN_MEM_NOT_PAGED | IMAGE_SCN_MEM_READ | IMAGE_SCN_MEM_WRITE
.INIT IMAGE_SCN_CNT_CODE | IMAGE_SCN_MEM_EXECUTE | IMAGE_SCN_MEM_READ
.rsrc IMAGE_SCN_CNT_INITIALIZED_DATA | IMAGE_SCN_MEM_READ | IMAGE_SCN_MEM_WRITE
.reloc IMAGE_SCN_CNT_INITIALIZED_DATA | IMAGE_SCN_MEM_READ | IMAGE_SCN_MEM_WRITE
.text IMAGE_SCN_CNT_CODE | IMAGE_SCN_MEM_EXECUTE | IMAGE_SCN_MEM_READ
```

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

### DeviceIoControl Handler

Now we know that the dispatch routine is at offset `0x14450`.

```asm
2: kd> u Aurum+0x14450
Aurum+0x14450:
fffff800`74864450 e960deffff      jmp     Aurum+0x122b5 (fffff800`748622b5) ; jmp
fffff800`74864455 3da7bc1300      cmp     eax,13BCA7h
fffff800`7486445a 0f84f7a20000    je      Aurum+0x1e757 (fffff800`7486e757)
fffff800`74864460 e9ffd00200      jmp     Aurum+0x41564 (fffff800`74891564)
fffff800`74864465 4d0fafc1        imul    r8,r9
fffff800`74864469 498bc0          mov     rax,r8
fffff800`7486446c 48c1e820        shr     rax,20h
fffff800`74864470 493bc3          cmp     rax,r11
```

```asm
2: kd> u Aurum+0x122b5
Aurum+0x122b5:
fffff800`748622b5 48895c2408      mov     qword ptr [rsp+8],rbx
fffff800`748622ba 4889742418      mov     qword ptr [rsp+18h],rsi
fffff800`748622bf 57              push    rdi
fffff800`748622c0 4154            push    r12
fffff800`748622c2 4155            push    r13
fffff800`748622c4 4156            push    r14
fffff800`748622c6 4157            push    r15
fffff800`748622c8 4881ec60020000  sub     rsp,260h
```

See full disassembly at [asm_Aurum%2B0x122b5.asm](asm_Aurum%2B0x122b5.asm)
