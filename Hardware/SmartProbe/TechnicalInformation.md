# SmartProbe Detailed Technical Information

## Connector Pinouts
### Embbeded HDT connector (16 pins)
| **Pin** | **Name**   | **Connection(s)** | **Notes**                                                                   |
|---------|------------|-------------------|-----------------------------------------------------------------------------|
| **1**   | APU_DBRDY  | Fpga Pin 4        | JTAG to debugged device                                                     |
| **2**   | APU_TDO    | Fpga Pin 3        | JTAG to debugged device                                                     |
| **3**   | GND        | -                 | -                                                                           |
| **4**   | APU_TDI    | Fpga Pin 2        | Debugged device may pull high to VCC via 1k                                 |
| **5**   | GND        | -                 | -                                                                           |
| **6**   | APU_TMS    | Fpga Pins 1,41    | Debugged device may pull high to VCC via 1k - double-driven by I/O on FPGA  |
| **7**   | GND        | -                 | -                                                                           |
| **8**   | APU_TCK    | Fpga Pins 42,48   | Debugged device may pull high to VCC via 1k - double-driven by I/O on FPGA  |
| **9**   | APU_DBREQ# | Fpga Pins 43,47   | Debugged device may pull high to VCC via 330 - double-driven by I/O on FPGA |
| **10**  | PWR_BTN#   | µC Pin 5          | Power Button pin for ACPI Reset simulation/request?                         |
| **11**  | 1.8V/VCC   | µC Pin 96         | Provided by debugged Device, FPGA VCCIB1 supply                             |
| **12**  | SYS_RST#   | µC Pin 1          |                                                                             |
| **13**  | LDT_RST#   | µC Pins 95,47     | Southbridge outputs signal to indicate reset, input on board                |
| **14**  | SCL1       | µC Pin 26         | I2C Slave 1 SCL                                                             |
| **15**  | GND        | -                 | -                                                                           |
| **16**  | SDA1       | µC Pin 27         | I2C Slave 1 SDA                                                             |

**Note** : APU_TRST# (on device to be debugged's board is pulled up to 1.8V/VCC by 1k.

### Personality Expansion connector (26 pins)
| **Pin** | **Name** | **Connection(s)** | **Notes**                                 |
|---------|----------|-------------------|-------------------------------------------|
| **1**   | 5V       | 5V, µC Pin 67     | 5V, possibly to power "personality board" |
| **2**   |          | Fpga Pin 7        | Unknown Function                          |
| **3**   |          | Fpga Pin  44      | Unknown Function                          |
| **4**   |          | Fpga Pin 8        | Unknown Function                          |
| **5**   | GND      | -                 | -                                         |
| **6**   |          | Fpga Pin 9        | Unknown Function                          |
| **7**   |          | µC Pin 72         | Unknown Function                          |
| **8**   |          | Fpga Pin 10       | Unknown Function                          |
| **9**   |          | Fpga Pin 45       | Unknown Function                          |
| **10**  |          | Fpga Pin 11       | Unknown Function                          |
| **11**  | GND      | -                 | -                                         |
| **12**  |          | Fpga Pin 12       | Unknown Function                          |
| **13**  |          | µC Pin 65         | Unknown Function                          |
| **14**  |          | Fpga Pin 13       | Unknown Function                          |
| **15**  |          | Fpga Pin 46       | Unknown Function                          |
| **16**  |          | Fpga Pin 14       | Unknown Function                          |
| **17**  | GND      | -                 | -                                         |
| **18**  |          | Fpga Pin 15       | Unknown Function                          |
| **19**  | GND      | -                 | -                                         |
| **20**  |          | Fpga Pin 16       | Unknown Function                          |
| **21**  | GND      | -                 | -                                         |
| **22**  |          | Fpga Pin 17       | Unknown Function                          |
| **23**  | GND      | -                 | -                                         |
| **24**  |          | Fpga Pin 20       | Unknown Function                          |
| **25**  | GND      | -                 | -                                         |
| **26**  |          | Fpga Pin 21       | Unknown Function                          |

**Note** : This is **NOT** a 26-pin HDT connector.

## Internal Structure

**Note** : 
* The "**Big HDT**" in this section refers to the personality expansion connector,
* The "**Little HDT**" in this section refers to Embbeded HDT connector (used on the GizmoBoard).

### Microcontroller
| **Pin** | **Name**      | **EPI mapping** | ****    | **PCB**                       | **Code Function**                                                                       | **Function**                                              |
|---------|---------------|-----------------|---------|-------------------------------|-----------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1**   | PE7           |                 |         | Little HDT Pin 12 (SYS_RST#)? | Output (System Reset?) - configured in code as OD with 8 ma drive                       | JTAG/HDT Control                                          |
| **2**   | PE6           |                 |         | Status LED                    | Output, used in conjunction with the ADC monitoring pins in code                        | Status indicator                                          |
| **3**   | VDDA          |                 |         | VDD 3.3V Plane via resistor?  |                                                                                         | Power                                                     |
| **4**   | GNDA          |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **5**   | PE5           |                 |         | Little HDT Pin 10             | OD with 8 ma drive                                                                      | JTAG/HDT Control                                          |
| **6**   | PE4           |                 |         | Connected but unused          | Connects to unused resistor pads                                                        | Unknown                                                   |
| **7**   | LDO           |                 |         | LDO (1.2V)                    |                                                                                         | Power                                                     |
| **8**   | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **9**   | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **10**  | PD0           |                 |         | Unused?                       | Unused?                                                                                 | ?                                                         |
| **11**  | PD1           |                 |         | FPGA Pin 40                   | Output/Used w/SSI(SPI)                                                                  | I/O w/FPGA                                                |
| **12**  | PD2           | EPI0S20         |         | FPGA Pin 39                   | Output/Used w/SSI(SPI)                                                                  | I/O w/FPGA                                                |
| **13**  | PD3           | EPI0S21         |         | FPGA Pin 38                   | Output, 8 mA drive,  PP w/weak pullup                                                   | I/O w/FPGA                                                |
| **14**  | PJ0           | EPI0S16         | DQM0    | DRAM Pin 15                   |                                                                                         | DRAM                                                      |
| **15**  | PH7           | EPI0S27         |         | FPGA Pin 27 (TRST)            | Output in FPGA update code at init, also in system code  8 mA drive,  PP w/weak pullup  | FPGA JTAG                                                 |
| **16**  | XTALPPHY      |                 |         | Ethernet Oscillator (25 MHz)  |                                                                                         | Ethernet Clock                                            |
| **17**  | XTALNPHY      |                 |         | Ethernet Oscillator (25 MHz)  |                                                                                         |                                                           |
| **18**  | PG1           | EPI0S14         | BA1/D14 | DRAM Pins 21,51               |                                                                                         | DRAM                                                      |
| **19**  | PG0           | EPI0S13         | BA0/D13 | DRAM Pins 21,50               |                                                                                         | DRAM                                                      |
| **20**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **21**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **22**  | PC7           | EPI0S5          | A5/D5   | DRAM Pins 10,30               |                                                                                         | DRAM                                                      |
| **23**  | PC6           | EPI0S4          | A4/D4   | DRAM Pins 8,29                |                                                                                         | DRAM                                                      |
| **24**  | PC5           | EPI0S3          | A3/D3   | DRAM Pins 7,26                |                                                                                         | DRAM                                                      |
| **25**  | PC4           | EPI0S2          | A2/D2   | DRAM Pins 5,25                |                                                                                         | DRAM                                                      |
| **26**  | PA0/U0RX      |                 |         | Little HDT Pin 14 (SCL)       | I2C Slave it would seem! (I2CS1)                                                        | I2C Slave for little HDT                                  |
| **27**  | PA1/U0TX      |                 |         | Little HDT Pin 16 (SDA)       | I2C Slave it would seem! (I2CS1)                                                        | I2C Slave for little HDT                                  |
| **28**  | PA2/SSl0Clk   |                 |         | FPGA Pin 29?                  | SSI/SPI pins                                                                            | I/O w/FPGA                                                |
| **29**  | PA3/SSl0Fss   |                 |         | FPGA Pin 30?                  | SSI/SPI pins                                                                            | I/O w/FPGA                                                |
| **30**  | PA4/SSI0RX    |                 |         | FPGA Pin 31?                  | SSI/SPI pins                                                                            | I/O w/FPGA                                                |
| **31**  | PA5/SSI0TX    |                 |         | FPGA Pin 32?                  | SSI/SPI pins                                                                            | I/O w/FPGA                                                |
| **32**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **33**  | ERBIAS        |                 |         | Ethernet Bias Resistor        |                                                                                         | Power                                                     |
| **34**  | PA6           |                 |         | FPGA Pin 36?                  | Output. Used in main Code as it's own function<br>Output, 8 mA drive,  PP w/weak pullup | I/O w/FPGA                                                |
| **35**  | PA7           |                 |         | FPGA Pin 37                   | Input, triggers interrupt on high/changing edges, PP w/weak pulldown                    | I/O w/FPGA                                                |
| **36**  | PG7           | EPI0S31         | CLK     | DRAM Pin 38                   |                                                                                         | DRAM                                                      |
| **37**  | RXIN          |                 |         | Ethernet RXI-                 |                                                                                         | Ethernet                                                  |
| **38**  | VDDC          |                 |         | LDO (1.2V)                    |                                                                                         | Power                                                     |
| **39**  | PJ2           | EPI0S18         | CASn    | DRAM Pin 17                   |                                                                                         | DRAM                                                      |
| **40**  | RXIP          |                 |         | Ethernet RXI+                 |                                                                                         | Ethernet                                                  |
| **41**  | PF5           | EPI0S15         | D15     | DRAM Pin 53                   |                                                                                         | DRAM                                                      |
| **42**  | PF4           | EPI0S12         | A12/D12 | DRAM Pin 48                   |                                                                                         | DRAM                                                      |
| **43**  | TXOP          |                 |         | Ethernet TXO-                 |                                                                                         | Ethernet                                                  |
| **44**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **45**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **46**  | TXON          |                 |         | Ethernet TXO+                 |                                                                                         | Ethernet                                                  |
| **47**  | PF0           |                 |         | Little HDT Pin 13 (LDT_RST#)  | Used as input w/ADC1, LDT Reset indicator from southbridge                              | JTAG/HDT Control                                          |
| **48**  | OSC0          |                 |         | Presumably NC                 |                                                                                         | System Clock                                              |
| **49**  | OSC1          |                 |         | Presumably NC                 |                                                                                         | System Clock                                              |
| **50**  | nWAKE         |                 |         | Tied High/Low                 |                                                                                         | Power Functions                                           |
| **51**  | nHIB          |                 |         | Tied High/Low                 |                                                                                         | Power Functions                                           |
| **52**  | XOSCO         |                 |         | Main Oscillator (16 MHz)      |                                                                                         | System Clock                                              |
| **53**  | XOSC1         |                 |         | Main Oscillator (16 MHz)      |                                                                                         | System Clock                                              |
| **54**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **55**  | VBAT          |                 |         | Presumably NC                 |                                                                                         | Power                                                     |
| **56**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **57**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **58**  | MDIO          |                 |         | Tied High/Low                 |                                                                                         | Ethernet (w/LEDs)                                         |
| **59**  | PF3           |                 |         | Ethernet LED Control          |                                                                                         | Ethernet (w/LEDs)                                         |
| **60**  | PF2           |                 |         | Ethernet LED Control          |                                                                                         | Ethernet (w/LEDs)                                         |
| **61**  | PF1           |                 |         | Unused?                       | Unused?                                                                                 | ?                                                         |
| **62**  | PH6           | EPI0S26         |         | Unused?                       | Unused?                                                                                 | ?                                                         |
| **63**  | PH5           | EPI0S11         | A11/D11 | DRAM Pins 35, 47              |                                                                                         | DRAM                                                      |
| **64**  | nRST          |                 |         | Test Point TP5                | Pulled Up                                                                               | Reset                                                     |
| **65**  | PB3/I2C0SDA   |                 |         | Big HDT 13?                   |                                                                                         | Unknown                                                   |
| **66**  | PB0/USB0ID    |                 |         | Unused?                       | Unused?                                                                                 | ?                                                         |
| **67**  | PB1/USB0VBUS  |                 |         | USB 5V Power                  | Usb Power Detection                                                                     | USB Power Detection                                       |
| **68**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **69**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **70**  | USB0DM        |                 |         | USB Connector D- Pin          |                                                                                         | USB                                                       |
| **71**  | USB0DP        |                 |         | USB Connector D+ Pin          |                                                                                         | USB                                                       |
| **72**  | PB2/I2C0SCL   |                 |         | Big HDT Pin 7                 |                                                                                         | HDT Control?                                              |
| **73**  | USB0RBIAS     |                 |         | USB Bias Resistor             |                                                                                         | USB                                                       |
| **74**  | PE0           | EPI0S8          | A8/D8   | DRAM Pins 33, 42              |                                                                                         | DRAM                                                      |
| **75**  | PE1           | EPI0S9          | A9/D9   | DRAM Pins 34, 44              |                                                                                         | DRAM                                                      |
| **76**  | PH4           | EPI0S10         | A10/D10 | DRAM Pins 22, 45              |                                                                                         | DRAM                                                      |
| **77**  | PC3/TDO       |                 |         | Test Point TP4                | µC JTAG TDO                                                                             | µC JTAG                                                   |
| **78**  | PC2/TDI       |                 |         | Test Point TP3                | µC JTAG TDI                                                                             | µC JTAG                                                   |
| **79**  | PC1/TMS       |                 |         | Test Point TP2                | µC JTAG TMS - configured as input                                                       | µC JTAG                                                   |
| **80**  | PC0/TCK       |                 |         | Test Point TP1                | Input in main code. Brick jtag entry?                                                   | µC JTAG                                                   |
| **81**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **82**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **83**  | PH3           | EPI0S0          | A0/D0   | DRAM Pins 2, 23               |                                                                                         | DRAM                                                      |
| **84**  | PH2           | EPI0S1          | A1/D1   | DRAM Pins 4, 24               |                                                                                         | DRAM                                                      |
| **85**  | PH1           | EPI0S7          | A7/D7   | DRAM Pins 13, 32              |                                                                                         | DRAM                                                      |
| **86**  | PH0           | EPI0S6          | A6/D6   | DRAM Pins 11, 31              |                                                                                         | DRAM                                                      |
| **87**  | PJ1           | EPI0S17         | DQM1    | DRAM Pin 39                   |                                                                                         | DRAM                                                      |
| **88**  | VDDC          |                 |         | LDO (1.2V)                    |                                                                                         | Power                                                     |
| **89**  | PB7           |                 |         | FPGA Pin 23 (TDI)             | JTAG control of FPGA in updater FW                                                      | FPGA JTAG                                                 |
| **90**  | PB6           |                 |         | FPGA Pin 24 (TMS)             | JTAG control of FPGA in updater FW                                                      | FPGA JTAG                                                 |
| **91**  | PB5           | EPI0S22         |         | FPGA Pin 26 (TDO)             | JTAG control of FPGA in updater FW                                                      | FPGA JTAG                                                 |
| **92**  | PB4           | EPI0S23         |         | FPGA Pin 22 (TCK)             | JTAG control of FPGA in updater FW                                                      | FPGA JTAG                                                 |
| **93**  | VDD           |                 |         | VDD 3.3V Plane                |                                                                                         | Power                                                     |
| **94**  | GND           |                 |         | Ground Plane                  |                                                                                         | Power                                                     |
| **95**  | PE2           | EPI0S24         |         | Little HDT Pin 13 (LDT_RST#)  | Analog ADC Input (ADC1)                                                                 | JTAG/HDT Control                                          |
| **96**  | PE3           | EPI0S25         |         | Little HDT Pin 11 (VCC)       | Analog ADC Input (ADC0)                                                                 | Monitor 1.8V from debugged device on little HDT connector |
| **97**  | PD4           | EPI0S19         | RASn    | DRAM Pin 18                   |                                                                                         | DRAM                                                      |
| **98**  | PD5           | EPI0S28         | Wen     | DRAM Pin 16                   |                                                                                         | DRAM                                                      |
| **99**  | PD6           | EPI0S29         | CSn     | DRAM Pin 19                   |                                                                                         | DRAM                                                      |
| **100** | PD7           | EPI0S30         | CKE     | DRAM Pin 37                   |                                                                                         | DRAM                                                      |

### FPGA
| **Pin** | **Name**      | **PCB**                                     | **Function**           |
|---------|---------------|---------------------------------------------|------------------------|
| **1**   | GEC0/IO37RSB1 | FPGA Pin 41, Little HDT Pin 6 (APU_TMS)     | Little HDT signals     |
| **2**   | IO36RSB1      | Little HDT Pin 4 (APU_TDI)                  | Little HDT signals     |
| **3**   | GEA0/IO34RSB1 | Little HDT Pin 2 (APU_TDO)                  | Little HDT signals     |
| **4**   | IO22RSB1      | Little HDT Pin 1  (APU_DBRDY)               | Little HDT signals     |
| **5**   | GND           | Ground Plane                                | Power                  |
| **6**   | VCCIB1        | Provided as VIO from debugged device        | Power                  |
| **7**   | IO24RSB1      | Big HDT Pin 2                               | Big HDT signals        |
| **8**   | IO33RSB1      | Big HDT Pin 4                               | Big HDT signals        |
| **9**   | IO26RSB1      | Big HDT Pin 6                               | Big HDT signals        |
| **10**  | IO32RSB1      | Big HDT Pin 8                               | Big HDT signals        |
| **11**  | IO27RSB1      | Big HDT Pin 10                              | Big HDT signals        |
| **12**  | IO29RSB1      | Big HDT Pin 12                              | Big HDT signals        |
| **13**  | IO30RSB1      | Big HDT Pin 14                              | Big HDT signals        |
| **14**  | FF/IO31RSB1   | Big HDT Pin 16                              | Big HDT signals        |
| **15**  | IO28RSB1      | Big HDT Pin 18                              | Big HDT signals        |
| **16**  | IO25RSB1      | Big HDT Pin 20                              | Big HDT signals        |
| **17**  | IO23RSB1      | Big HDT Pin 22                              | Big HDT signals        |
| **18**  | VCC           | Taken from µC pin7 (VCORE)                  | Power                  |
| **19**  | VCCIB1        | Provided as VIO from debugged device        | Power                  |
| **20**  | IO17RSB1      | Big HDT Pin 24                              | Big HDT signals        |
| **21**  | IO14RSB1      | Big HDT Pin 26                              | Big HDT signals        |
| **22**  | TCK           | µC Pin  92                                  | FPGA programming       |
| **23**  | TDI           | µC Pin  89                                  | FPGA programming       |
| **24**  | TMS           | µC Pin 90                                   | FPGA programming       |
| **25**  | VPUMP         | VDD 3.3V Plane                              | Power                  |
| **26**  | TDO           | µC Pin 91                                   | FPGA programming       |
| **27**  | TRST          | µC Pin 15                                   | FPGA programming       |
| **28**  | VJTAG         | VDD 3.3V Plane                              | Power                  |
| **29**  | IO11RSB0      | µC Pin 28 (SSIO_CLK)                        | µC SSI slave for comms |
| **30**  | IO10RSB0      | µC Pin 29 (SSIO_FSS)                        | µC SSI slave for comms |
| **31**  | IO09RSB0      | µC Pin 30 (SSIO_RX)                         | µC SSI slave for comms |
| **32**  | IO08RSB0      | µC Pin 31 (SSIO_TX)                         | µC SSI slave for comms |
| **33**  | VCCIB0        | VDD 3.3V Plane                              | Power                  |
| **34**  | GND           | Ground Plane                                | Power                  |
| **35**  | VCC           | Taken from µC pin7 (VCORE)                  | Power                  |
| **36**  | IO07RSB0      | µC Pin 34?                                  | µC communications      |
| **37**  | IO06RSB0      | µC Pin 35                                   | µC communications      |
| **38**  | GDA0/IO05RSB0 | µC Pin 13                                   | µC communications      |
| **39**  | IO03RSB0      | µC Pin 12                                   | µC communications      |
| **40**  | GDC0/IO01RSB0 | µC Pin 11                                   | µC communications      |
| **41**  | IO12RSB1      | Fpga Pin 1, little HDT Pin 6 (APU_TMS)      | Little HDT signals     |
| **42**  | IO13RSB1      | Fpga Pin 48, Little HDT pin 8 (APU_TCK)     | Little HDT signals     |
| **43**  | IO15RSB1      | Fpga Pin 47, little HDT pin 9 (APU_DBREQ#)  | Little HDT signals     |
| **44**  | IO16RSB1      | Big HDT Pin 3                               | Big HDT signals        |
| **45**  | IO18RSB1      | Big HDT pin 9                               | Big HDT signals        |
| **46**  | IO19RSB1      | Big HDT pin 15                              | Big HDT signals        |
| **47**  | IO20RSB1      | FPGA Pin 43, little HDT pin 9  (APU_DBREQ#) | Little HDT signals     |
| **48**  | IO21RSB1      | FPGA pin 42, little HDT pin 8 (APU_TCK)     | Little HDT signals     |
| **PAD** | GND           | Ground Plane                                | Power                  |