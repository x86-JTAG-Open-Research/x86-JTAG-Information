# SmartProbe GDB commands

List of specific monitor commands available

:information_source: There commands have only been tested in real mode (x86)

:information_source: These commands have only been test on a Family 14h, Model 2h, Stepping 0h in real mode (x86)

## GDB commands 

### continue

*Description* : Carries on running the target from the current state. Blocking. Can be interrupted with ```^C```

*Usage* : ```(gdb)c```

*Example* : 
```
(gdb)c
Continuing
^C
(gdb)
```
### si

*Description* : Steps through a single assembly operation. Will print the called instruction

*Usage* : ```(gdb)si```

*Example* : 

```
(gdb)si
0xffffe000 in ?? ()
=> 0xffffe000:  fa                      cli
(gdb)
```
### info registers

*Description* : Dumps all currently cached registers in the gdb stub

*Usage* : ```(gdb)info registers```

*Example* : 

```
(gdb)info registers
eax            0x0                 0
ecx            0x0                 0
edx            0x500f20            5246752
ebx            0x0                 0
esp            0x0                 0x0
ebp            0x0                 0x0
esi            0x0                 0
edi            0x0                 0
eip            0xffffe000          0xffffe000
eflags         0x2                 [ ]
cs             0xf000              61440
ss             0x0                 0
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
cr0            0x60000010          1610612752
cr2            0x0                 0
cr3            0x0                 0
cr4            0x0                 0
(gdb)
```

### info all-registers

*Description* : Steps through a single assembly operation. Will print the called instruction

*Usage* : ```(gdb)info all-registers```

*Example* : 

```
(gdb)monitor helpinfo all-registers
eax            0x0                 0
ecx            0x0                 0
edx            0x500f20            5246752
ebx            0x0                 0
esp            0x0                 0x0
ebp            0x0                 0x0
esi            0x0                 0
edi            0x0                 0
eip            0xfffffff0          0xfffffff0
eflags         0x2                 [ ]
cs             0xf000              61440
ss             0x0                 0
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
st0            0                   (raw 0x00000000000000000000)
st1            0                   (raw 0x00000000000000000000)
st2            0                   (raw 0x00000000000000000000)
st3            0                   (raw 0x00000000000000000000)
st4            0                   (raw 0x00000000000000000000)
st5            0                   (raw 0x00000000000000000000)
st6            0                   (raw 0x00000000000000000000)
st7            0                   (raw 0x00000000000000000000)
fctrl          0x40                64
fstat          0x0                 0
ftag           0x5555              21845
fiseg          0x0                 0
fioff          0x0                 0
foseg          0x0                 0
fooff          0x0                 0
fop            0x0                 0
xmm0           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm1           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm2           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm3           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm4           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm5           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm6           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
xmm7           {v4_float = {0x0, 0x0, 0x0, 0x0}, v2_double = {0x0, 0x0}, v16_int8 = {0x0 <repeats 16 times>}, v8_int16 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}, v4_int32 = {0x0, 0x0, 0x0, 0x0}, v2_int64 = {0x0, 0x0}, uint128 = 0x0}
mxcsr          0x1f80              [ IM DM ZM OM UM PM ]
cr0            0x60000010          1610612752
cr2            0x0                 0
cr3            0x0                 0
cr4            0x0                 0
mm0            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm1            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm2            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm3            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm4            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm5            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm6            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
mm7            {uint64 = 0x0, v2_int32 = {0x0, 0x0}, v4_int16 = {0x0, 0x0, 0x0, 0x0}, v8_int8 = {0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0}}
```

## Monitor Commands

**Note** : All hex values are not prefixed with 0x, but just sent directly.

:warning: Sometimes combinations of these commands can freeze up the CPU if the SageProbe, if things start acting weird then just reset both.

### delay
*Description* : Delays for an unknown amount of time (short though). Could be measured through FW of the SmartProbe.

*Usage* : ```(gdb)monitor delay```

*Example* :

```
(gdb)monitor delay
(gdb)
```

### halt
*Description* : Send some JTAG command to halt the processor. Unknown if the node/core can be specified.

*Usage* : ```(gdb)monitor halt```

*Example* :

```
(gdb)monitor halt
(gdb)
```

### help
*Description* : Prints out a list of accepted monitor commands, including this command.

*Usage* : ```(gdb)monitor help```

*Example* :

```
(gdb)monitor help
delay
halt
help
reset
run
HaltedCores
IOread
IOwrite
MSRread
MSRwrite
PCIread
PCIwrite
Power
RegisterRead
RegisterWrite
MemRead
MemWrite
JTAGCLK
JTAGXCV
JTAGscan
JTAGLENGTH
CarOnReset
CPUID
HaltOnReset
Port
Version
String1
(gdb)
```

### reset

*Description* : This command resets the target system by pulsing SYS_RST# for 150 ms. Resets the processor/system.

*Usage* : ```(gdb)monitor reset```

*Example* 

```
(gdb)monitor reset 
(gdb)
```

### run

*Description* : This command lets the target system run. Unlike ```c``` in gdb, it does not block user input.

*Usage* : ```(gdb)monitor run```

*Example* 

```
(gdb)monitor run
(gdb)
```

### HaltedCores

*Description* : Provides a list of halted cores on the current (or 0-indexed node) by default, but an optional ```node``` can be specified. 
    The result will be in the format ```XX:YYYYYYYY```, where ```XX``` is the amount of cores present on the node, and ```YYYYYYYY``` is an integer that should be seen as a bitmask of the halt cores (eg, if cores 0 and 8 are halted, the result will be 0b100000001, or 0x101).

*Usage* : ```(gdb)monitor HaltedCores[,node]```

*Example* :

```
(gdb)monitor HaltedCores,0
02:00000001
(gdb)monitor HaltedCores
02:00000001
(gdb)monitor HaltedCores,1
ERR06:No Node/Core Available at the Requested Index
Protocol error with Rcmd: 06.
(gdb)
```

### IOread

*Description* : Reads an I/O port.

*Usage* : ```(gdb)monitor IOread,<PortNumber>,<Size>``` where ```<PortNumber>``` and ```<Size>``` are the port number and the size in bytes (32 bits for the former, and only 1,2 and 4 for the latter).

*Example* :

```
(gdb)monitor IOread,CF8,4
ffffffff
(gdb)monitor IOread,80,1
00
(gdb)
```

### IOwrite

*Description* : Writes to an I/O port.

*Usage* : ```(gdb)monitor IOwrite,<PortNumber>,<Size>,<Data>``` where ```<PortNumber>``` and ```<Size>``` are the port number and the size in bytes (32 bits for the former, and only 1,2 and 4 for the latter), and ```<Data>``` is the data to be written (ideally, it should match the number of desired write bytes).

*Example* : 

```
(gdb)monitor IOwrite,CF8,4,FAFAFAFA
(gdb)monitor IOread,CF8,4
80fafaf8
(gdb)
```
:information_source: Note that the CF8 I/O register for PCI address in PCI configuration space did not take into account some bytes written, this is normal.

### MSRread

*Description* : Reads a Machine Specific (MSR) register.

*Usage* : ```(gdb)monitor MSRread,<MsrReg>[,<Node>,<Core>]```, where ```<MsrReg>``` is the machine specific register to be read (32 bits). Two optional arguments ```<Node>``` and ```<Core>``` specify the node/core for which this should be run on. Returns the uper and lower 32 bits, respectively, of the 64 bit MSR.

*Example* 

```
(gdb) monitor MSRread,C0000010
deadbeef-deadbeef
(gdb) monitor MSRread,10
00000746-92833582
(gdb) monitor MSRread,10
00000747-bf0f5536
(gdb)
```
:information_source: Invalid registers are read as deadbeef-deadbeef on this example on architecture


### MSRwrite

*Description* : Writes to a Machine Specific (MSR) register.

*Usage* : ```(gdb)monitor MSRwrite <MsrReg>,<HighValue>,<LoValue>[,<Node>,<Core>]```, where where ```<MsrReg>``` is the machine specific register to be read (32 bits), and ```<HighValue>``` and,```<LoValue>``` are the high and low 32-bits of the 64-bit MSR. Two optional arguments ```<Node>``` and ```<Core>``` specify the node/core for which this should be run on.

*Example* 

```
(gdb)monitor MSRwrite,C0000101,FADAFADA,CAFECAFE
(gdb)monitor MSRwrite,C0000101,FADAFADA,CAFECAFE,0,0
(gdb)
```

### PCIread

*Description* : Reads from PCI configuration space (via 0xCF8/0xCFC).

*Usage* : ```(gdb)monitor PCIread```

*Example* 

```
(gdb)monitor 
(gdb)
```

### PCIwrite

*Description* : Writes to PCI configuration space (via 0xCF8/0xCFC).

*Usage* : ```(gdb)monitor PCIwrite```

*Example* 

```
(gdb)monitor 
(gdb)
```

### Power
*Description* : Turns the power on or off on the device. Also supports doing this via ACPI.

*Usage* : ```(gdb)monitor Power,<type>```, where ```<type>``` is the desired power operation (one of ```on```,```off``` or ```acpi```).

*Example* 

```
(gdb)monitor Power,off
(gdb)
```

:warning: Unable to test with current setup. ```on```and ```off``` do nothing over JTAG, and ```acpi``` just pulses TMS.

### RegisterRead
*Description* : Reads a register.

*Usage* : ```(gdb)monitor RegisterRead```

*Example* 

```
(gdb)monitor 
(gdb)
```

### RegisterWrite
*Description* : Writes to a register.

*Usage* : ```(gdb)monitor RegisterWrite```

*Example* 

```
(gdb)monitor 
(gdb)
```

### MemRead
*Description* : Reads from memory.

*Usage* : ```(gdb)monitor MemRead```

*Example* 

```
(gdb)monitor 
(gdb)
```

### MemWrite
*Description* : Writes to memory.

*Usage* : ```(gdb)monitor MemWrite```

*Example* 

```
(gdb)monitor 
(gdb)
```

### JTAGCLK
*Description* : Sets the JTAG clock speed.

*Usage* : ```(gdb)monitor JTAGCLK,<ClockSpeed>```, where ```<ClockSpeed>``` is the desired speed in Hz. Is limited by CPU clock speed/2 and possibly granularity at lower levels (to be determined). Responds with the actual speed it set in Hz.

*Example* 

```
(gdb) monitor JTAGCLK,800
2332
(gdb) monitor JTAGCLK,800000
800000
(gdb) monitor JTAGCLK,11000000
13333333
(gdb) monitor JTAGCLK,80000000
40000000
(gdb) monitor CPUID,0,0
ERR61:The Core Failed to Respond to the Debug Command
Protocol error with Rcmd: 61.
(gdb)
```

:information_source: Your wiring may or may not allow this speed to be functional if signal integrity is compromised.

:information source: Certain speeds may make things unstable. Speed is autodetected up to 8 MHz starting at 2 MHz in 1 MHz increments during a ```JTAGscan```. 

### JTAGXCV
*Description* : Do a lowlever JTAG operation.

*Usage* : ```(gdb)monitor JTAGXCV```, with unknown arguments.

*Example* :

```
(gdb)monitor JTAGXCV,.....
????
(gdb)
```

:information source: Arguments are not yet known. To be completed after investigation.

### JTAGscan
*Description* : Scans the JTAG bus. Unsure what it does at this time but PCI accesses are present over the device.

*Usage* : ```(gdb)monitor JTAGscan```

*Example* 

```
(gdb)monitor JTAGscan
(gdb)
```

### JTAGLENGTH
*Description* : Detect and indicates the JTAG chain length (devices) and IR size. 

*Usage* : ```(gdb)monitor JTAGLENGTH```

*Example* : 

```
(gdb) monitor JTAGLENGTH
IR Length=8
DeviceCount=1
(gdb)
```

:information_source: Unsure what happens when devices with different IR lengths are chained.

:information_source: The probe autodetects this over JTAG.

### CPUID
*Description* : Retreives CPUID information from the processor, including extended CPUID registers.

*Usage* : ```(gdb)monitor CPUID,<Register>,<LoHi>[,<Node>,<Core>]```, where ```<Register>``` is the CPUID register to read, ```<LoHi>``` is 0 or 1, where 0 shows EBX-EAX and 1 shows EDX-ECX, in that order. Two optional arguments ```<Node>``` and ```<Core>``` specify the node/core for which this should be un on.

*Example* :
```
(gdb) monitor CPUID,0,0
68747541-00000006
(gdb) monitor CPUID,0,1
69746e65-444d4163
(gdb) monitor CPUID,0,1,0,0
69746e65-444d4163
(gdb) monitor CPUID,0,1,0,1
ERR65:The Core Will NOT Respond to Debug Commands in its Current State
Protocol error with Rcmd: 65.
(gdb)
```
:information_source: The result we see is "AuthenticAMD" and the largest standard CPUID function implemented (6).

:information_source: Second core is currently disabled on the target so it does not execute the command.

### HaltOnReset
*Description* : Resets the device and halts execution at the reset vector (```eip``` should be set to ```0xFFFFFFF0```).

*Usage* : ```(gdb)monitor HaltOnReset```

*Example* 

```
(gdb)monitor HaltOnReset
(gdb)i r
eax            0x0                 0
ecx            0x0                 0
edx            0x500f20            5246752
ebx            0x0                 0
esp            0x0                 0x0
ebp            0x0                 0x0
esi            0x0                 0
edi            0x0                 0
eip            0xfffffff0          0xfffffff0
eflags         0x2                 [ ]
cs             0xf000              61440
ss             0x0                 0
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
cr0            0x60000010          1610612752
cr2            0x0                 0
cr3            0x0                 0
cr4            0x0                 0
(gdb)
```
### Port
*Description* : Monitors a I/O port and prints it out to the console when a write to this port is received.

*Usage* : ```(gdb)monitor Port,<portNumber>[,<status>]``` where ```<portNumber>``` is the I/O port to monitor in hex, and ```<status\``` is whether or not to enable (```1```) or disable (```0```) monitoring that port. Default without the optional status field is to enable.

*Example* 

```
(gdb)monitor Port,0xE9,1
(gdb)c
Hello World from port 0xE9!^C
Program received signal SIGTRAP, Trace/breakpoint trap.
0x000fe01b in ?? ()
=> 0x000fe01b:  eb fd                   jmp    0xfe01a
(gdb)
```
:warning: Monitoring multiple ports at the same time may cause issues. 
:information_source: Port monitoring is automatically disabled upon target reset.

### Version
*Description* : Prints out the version information of the SmartProbe.

*Usage* : ```(gdb)monitor Version```

*Example* 

```
(gdb)monitor Version
SmartProbe: 3.2_3743
(gdb)
```

### String1
*Description* : Seems to reply with the string presented after **String1**

*Usage* : ```(gdb)monitor String1,<String>``` where ```<String>```< is a placeholder for any string. Note : The firmware may limit the reply size to it's internal buffer (~250 chars).

*Example* 

```
(gdb)monitor String1,HelloWorld
HelloWorld
(gdb)
```

## Undocumented commands

:information_source: **Speculative** : These commands could be related to the personality board of the probe?

### CarOnReset

*Description* : Resets and configures the Processor's Cache as RAM (CAR) to be able to be used (eg, load code in RAM).

*Usage* : ```(gdb)monitor CarOnReset```

*Example* 

```
(gdb)monitor CarOnReset
(gdb)
```

:information_source: Might be an experimental command that works only under certain circumstances/with certain processors as it has rendered the target test on (G-T56N based thin client) inoperable until reboot.

### NVStorage

*Description* : Unsure.

*Usage* : ```(gdb)monitor NVStorage```

*Example* :

```
(gdb)monitor NVStorage
ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff
(gdb)
```

:information_source: Unsure what this command does. It does not send HDT commands via JTAG.


### Remaining Commands to Document

* May related to previous commands/alternate syntax:
  * ```IOred```
  * ```IOwrt```
  * ```MSRrd```
  * ```MSRwr```
  * ```PCIrd```
  * ```PCIwr```
  * ```Versn```

* Unknown for the moment, to be analyzed:
  * ```HDTst```
  * ```Featr```
  * ```Processor```
  * ```Targt```
  * ```Core```
  * ```Features```
  * ```FlashWrite```
  * ```Node```
  * ```NVStorage```
  * ```Probe```
  * ```Target```
  * ```Update```
  * ```UserRegs```
  * ```MemType```
  * ```MemAddr```
  * ```IoBreakPoint```
  * ```I2CSlave```
  * ```FamilyID```
