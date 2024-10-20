# AMD 16-pin Embedded Probe
## Populated
![Populated](./EmbeddedProbe/EmbeddedProbe_P.jpg)
## Not populated
TODO

## Pinout for (16-pin) Embedded HDT Connector    

| Pin | Name       | Notes                                               |
|-----|------------|-----------------------------------------------------|
| 1   | APU_DBRDY  |                                                     |
| 2   | APU_TDO    |                                                     |
| 3   | GND        |                                                     |
| 4   | APU_TDI    | Debugged device may pull high to VCC via 1kOhms     |
| 5   | GND        |                                                     |
| 6   | APU_TMS    |                                                     |
| 7   | GND        |                                                     |
| 8   | APU_TCK    | Debugged device may   pull high to VCC via 1k       |
| 9   | APU_DBREQ# | Debugged device may   pull high to VCC via 330 ohms |
| 10  | PWR_BTN#   |                                                     |
| 11  | 1.8V/VCC   |                                                     |
| 12  | SYS_RST#   |                                                     |
| 13  | LDT_RST#   |                                                     |
| 14  | SCL1       |                                                     |
| 15  | GND        |                                                     |
| 16  | SDA1       |                                                     |

APU_TRST# (on debugee's board) can be pulled up to 1.8V/VCC by 1kOhms
