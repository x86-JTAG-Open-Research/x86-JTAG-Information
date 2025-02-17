# Sage Electronic Engineering SmartProbe

## Technical Overview
### Hardware
- TI/Stellaris LM3S9B90 microcontroller
- Actel AGLN010 FPGA/CPLD
- Winbond W9864G6JH 1M x 4B x 16 bits DRAM
- USB/Ethernet Connectivity
- Embedded 16-pin header, extended support header (26-pin, is not regular HDT header).
### Software
- FPGA Updated via DirectC (Actel/Microsemi update library for ISP)
- LWIP stack for Ethernet
- Stellaris ROM for support functions
- Note : certain LM3S9B90 IC revisions have broken ROMS, so StellarisWare is probably integrated into the FW flash image to replace it. There are 2 different FW versions (at least).
- Acts as gdb stub for debugging

## Detailed Information
* [Pinouts & Internal board routing](./SmartProbe/TechnicalInformation.md)
* [GDB Commands Supported](./SmartProbe/GdbCommands.md)

## Pictures
![SmartProbe 1](./SmartProbe/pictures/SmartProbe_1.jpg)
![SmartProbe 2](./SmartProbe/pictures/SmartProbe_2.jpg)
![SmartProbe 3](./SmartProbe/pictures/SmartProbe_3.jpg)
![SmartProbe 4](./SmartProbe/pictures/SmartProbe_4.jpg)
![SmartProbe 5](./SmartProbe/pictures/SmartProbe_5.png)
![SmartProbe 6](./SmartProbe/pictures/SmartProbe_6.png)