

To let you to create projects that leverage the power of both microcontrollers, they are connected through a **serial connection**.  
Such connection uses **GPIO0** (TX) and **GPIO1** (RX) on RP2040 and, on ESP32, **IO19** (TX) and **IO22** (RX). On schematic file those connections are labeled with *RPI_UART_TX* and *RPI_UART_RX*.  
Keep in mind that RP GPIO0 is connected to ESP IO22 and, vice versa, GPIO1 is connected with IO19.  
Thanks to this connection you can exchange between the MCUs whichever stream of bytes. 

There are cases in which the RP2040 must be restarted remotely: you can perform this operation from the ESP32.  
The pin number 10 on **P2** header (**RPI_RESET**) is connected to ESP pin **IO23**. By setting its output level **LOW** the RP2040 execution is disabled, while, setting output level **HIGH**, the RP2040 execution is restored.  
So, to reset the Raspberry microcontroller from ESP, let's set the output level LOW and then move to HIGH.

Moreover, to enable RP2040 OTA programming, its SWD lines are connected to ESP pins as shown in the following table.  
| ESP GPIO NUM | RP SWD interface |
| ---            | ---            |
| IO2            | SWDIO          |
| IO4            | SWCLK          |

Since the RP2040 can be programmed also through on-board SWD header **P5**, the user must ensure that, while he want to use such interface, the GPIO **IO5** level is set to **HIGH**. To use external headers, such GPIO must be set to **LOW** level.

Keep in mind that the IMU sensor is connected to both microcontrollers and, to select which of them can interact with it, a jumper must be inserted as explained in the following table. As explained in the schematic file, pin number 1 is the closest to the RP2040 and pin number 3 is the closest to the ESP32. 

| Jumper position | IMU Sensor connected to |
| ---             | ---                     |
| Not placed      | ESP32 (Default)         |
| Pin 1-2         | RP2040                  |
| Pin 2-3         | ESP32                   |