
# ESP32

The UDOO KEY is powered by Espressif **ESP32-WROVER-E** MCU module, a powerful and versatile platform for Edge AI applications, ranging from low-power sensor networks to the most demanding tasks, such as voice encoding, music streaming and MP3 decoding. This module is provided with a PCB antenna.  
This fully programmable microcontroller is based on a **dual-core Xtensa 32-bit LX6**, with a 16 MB internal SPI flash memory, an additional 8 MB SPI Pseudo Static RAM (PSRAM), Wi-Fi and Bluetooth.

The core of the module is the **ESP32-D0WD-V3** chip, which is designed to be scalable and adaptive. It features two CPU cores that can be individually controlled, and the CPU clock frequency is adjustable from 80 MHz to 240 MHz. The chip is also provided with a low-power co-processor that can be used instead of the CPU to save power while performing tasks that do not require much computing power, such as perihperals monitoring.

Thanks to the ESP32 on board, you get full Wi-Fi 802.11b/g/n connectivity, Bluetooth and BLE v4.2. This ensures the UDOO KEY extreme versatility: the Wi-Fi allows to set up direct connection to the internet through a Wi-Fi router, while using the Bluetooth users can connect to their phones or broadcast low energy beacons for its detection.

Note that the ESP32 on board is not just a Wi-Fi, BT & BLE module. It gives you full access to the firmware of ESP32 and you can program it as you please. 
The sleep current of the ESP32 chip is less than 5 µA, making it suitable for battery powered and wearable electronics applications. The module supports a data rate of up to 150 Mbps, 802.11b at 13.5dBm, and 802.11g/n at 18.5 dBm of output power to the antenna to ensure the widest physical range. The module thus offers industry-leading specifications and the best performance for electronic integration, range, power consumption, and connectivity. Secure (encrypted) over the air (OTA) upgrade is also supported, so that users can upgrade their products even after their release, at minimum cost and effort.
For further information on Espressif ESP32, please refer to the dedicated page on [espressif.com](https://espressif.com).

In order to be able to interface the ESP32 with external integrated circuits, the target MCU is equipped with an UEXT connector following the pin map as reported in the table below.

| Pin number | Schematic pin name | ESP GPIO | Description |
| ---        | ---  | ---      | ---         |
|1|3V3| - |3.3V output, 150mA max|
|2|GND| - |Power ground|
|3|EXT_UART2_TX|GPIO13|UART transmission line|
|4|EXT_UART2_RX|GPIO26|UART reception line|
|5|ESP32_SCL|GPIO21|I²C clock line|
|6|ESP32_SDA|GPIO18|I²C data line|
|7|SPI_MISO|GPIO35|SPI master input - slave output|
|8|SPI_MOSI|GPIO12|SPI master output - slave input|
|9||SPI_SCK|GPIO14|SPI clock|
|10|SPI_CS|GPIO15|SPI chip select|


## RP2040

The Pico-compatible part of the UDOO KEY is built upon a **Raspberry Pi RP2040 microcontroller**, dual Arm Cortex-M0+, with a QSPI 8MB Flash, a 133MHz clock and 264KB of on-chip SRAM.
The RP2040 microcontroller is a chip from Raspberry Pi Foundation that integrates two Arm Cortex-M0+ CPUs that can be run up to 133MHz, featuring 264kB of on-chip SRAM and up to 16MB of off-chip Flash memory. This microcontroller can be used for machine learning, motor control, audio and so on.
The UDOO KEY is **100% compatible with Raspberry Pi Pico** both hardware and software-wise. This means that each and any expansion hardware as well as each and any software built for Raspberry Pi Pico will work out of the box on UDOO KEY.
For further information on RP2040, please refer to the dedicated page on [raspberrypi.com](htps://raspberrypi.com). 

**P1** and **P2** connectors of the Pico part can be used to connect external peripherals to the RP2040. Two 20-pin headers or castellated holes must be soldered on P1 and P2 in a proper manner to use them . The following tables summarize the possibilities offered by P1 and P2 connectors.

#### P1
| Pin number | Schematic pin name | SPI | UART interface | I²C | PWM | SIO/PIO |
| ---        | ---                | --- | ---            | --- | --- | ---     |
|1|N.C.|-|-|-|-|-|
|2|N.C.|-|-|-|-|-|
|3|GND|-|-|-|-|-|
|4|RPI_SDA|SPI0_SCK|UART0_CTS|I2C1_SDA|PWM1_A|SIO/PIO0/PIO1|
|5|RPI_SCL|SPI0_TX|UART0_RTS|I2C1_SCL|PWM1_B|SIO/PIO0/PIO1|
|6|GP4|SPI0_RX|UART1_TX|I2C0_SDA|PWM2_A|SIO/PIO0/PIO1|
|7|GP5|SPI0_CSn|UART1_RX|I2C0_SCL|PWM2_B|SIO/PIO0/PIO1|
|8|GND|-|-|-|-|-|
|9|GP6|SPI0_SCK|UART1_CTS|I2C1_SDA|PWM3_A|SIO/PIO0/PIO1|
|10|GP7|SPI0_TX|UART1_RTS|I2C1_SCL|PWM3_B|SIO/PIO0/PIO1|
|11|GP8|SPI1_RX|UART1_TX|I2C0_SDA|PWM4_A|SIO/PIO0/PIO1|
|12|GP9|SPI1_CSn|UART1_RX|I2C0_SCL|PWM4_B|SIO/PIO0/PIO1|
|13|GND|-|-|-|-|-|
|14|GP10|SPI1_SCK|UART1_CTS|I2C1_SDA|PWM5_A|SIO/PIO0/PIO1|
|15|GP11|SPI1_TX|UART1_RTS|I2C1_SCL|PWM5_B|SIO/PIO0/PIO1|
|16|GP12|SPI1_RX|UART0_TX|I2C0_SDA|PWM6_A|SIO/PIO0/PIO1|
|17|GP13|SPI1_CSn|UART0_RX|I2C0_SCL|PWM6_B|SIO/PIO0/PIO1|
|18|GND|-|-|-|-|-|
|19|GP14|SPI1_SCK|UART0_CTS|I2C1_SDA|PWM7_A|SIO/PIO0/PIO1|
|20|GP15|SPI1_TX|UART0_RTS|I2C1_SCL|PWM7_B|SIO/PIO0/PIO1|

</p>

**Pin number** **1** and **2** are not connected since are used for MCUs communication.

#### P2
| Pin number | Schematic pin name | SPI | UART interface | I²C | PWM | SIO/PIO |
| ---        | ---                | --- | ---            | --- | --- | ---     |
|1|GP16|SPI0_RX|UART0_TX|I2C0_SDA|PWM0_A|SIO/PIO0/PIO1|
|2|GP17|SPI0_CSn|UART0_RX|I2C0_SCL|PWM0_B|SIO/PIO0/PIO1|
|3|GND|-|-|-|-|-|
|4|GP18|SPI0_SCK|UART0_CTS|I2C1_SDA|PWM1_A|SIO/PIO0/PIO1|
|5|GP19|SPI0_TX|UART0_RTS|I2C1_SCL|PWM1_B|SIO/PIO0/PIO1|
|6|GP20|SPI0_RX|UART1_TX|I2C0_SDA|PWM2_A|SIO/PIO0/PIO1|
|7|GP21|SPI0_CSn|UART1_RX|I2C0_SCL|PWM2_B|SIO/PIO0/PIO1|
|8|GND|-|-|-|-|-|
|9|GP22|SPI0_SCK|UART1_CTS|I2C1_SDA|PWM3_A|SIO/PIO0/PIO1|
|10|RPI_RESET|-|-|-|-|-|
|11|GP26|SPI1_SCK|UART1_CTS|I2C1_SDA|PWM5_A|SIO/PIO0/PIO1|
|12|GP27|SPI1_TX|UART1_RTS|I2C1_SCL|PWM5_B|SIO/PIO0/PIO1|
|13|GND|-|-|-|-|-|
|14|GP28|SPI1_RX|UART0_TX|I2C0_SDA|PWM6_A|SIO/PIO0/PIO1|
|15|ADC_VREF|-|-|-|-|-|
|16|3V3|-|-|-|-|-|
|17|N.C.|-|-|-|-|-|
|18|GND|-|-|-|-|-|
|19|VSYS|-|-|-|-|-|
|20|VBUS|-|-|-|-|-|

</p>

**Pin number:**
+ **10** is reserved for RP2040 reset by ESP32
+ **16** provide 3.3V DC (315mA) in output
+ **17** is not connected
+ **19** provide 5V DC (500mA) filtered from USB Type-C connector (CN1)
+ **20** provide 5V DC (500mA) raw from USB Type-C connector (CN1)


#### P5

The **Serial Wire Debug** interface is available on the 1x3 poles connector **P5**. This header allows you to program and debug the RP2040 microcontroller externally.  
The following table shows the pin configuration.

| Pin number | Function |
| ---        | ---      |
| 1          | SWCLK    |
| 2          | GND      |
| 3          | SWDIO    |


## MCUs Connections



To let you to create projects that leverage the power of both microcontrollers, they are connected through a **serial connection**.  
Such connection uses **GPIO0** (TX) and **GPIO1** (RX) on RP2040 and, on ESP32, **IO19** (RX) and **IO22** (TX). On schematic file those connections are labeled with *RPI_UART_TX* and *RPI_UART_RX*.  
Keep in mind that RP GPIO0 is connected to ESP IO19 and, vice versa, GPIO1 is connected with IO22.  
Thanks to this connection you can exchange between the MCUs whichever stream of bytes. 

There can be exist cases in which the RP2040 must be restarted remotely: you can perform this operation from the ESP32.  
The pin number 10 on **P2** header (**RPI_RESET**) is connected to ESP pin **IO23**. By setting its output level **LOW** the RP2040 execution is disabled, while, setting output level **HIGH**, the RP2040 execution is restored.  
So, to reset the Raspberry microcontroller from ESP, let's set the output level LOW and then move to HIGH.

Moreover, to enable RP2040 OTA programming, its SWD lines are connected to ESP pins as shown in the following table.  
| ESP GPIO NUM | RP SWD interface |
| ---            | ---            |
| IO2            | SWDIO          |
| IO4            | SWCLK          |

Since the RP2040 can be programmed also through on-board SWD header **P5**, the user must ensure that, while he want to use such interface, the GPIO **IO5** level is set to **HIGH**. To use external headers, such GPIO must be set to **LOW** level.

Keep in mind that the IMU sensor is connected to both microcontrollers and, to select which of them can interact with it, a jumper must be inserted as explained in the following table. As explained in the schematic file, pin number 1 is the closest to the RP2040 and pin number 3 is the closest to the ESP32. 

| Jumper position | Microcontroller enabled |
| ---             | ---                     |
| Not placed      | ESP32 (Default)         |
| Pin 1-2         | RP2040                  |
| Ping 2-3        | ESP32                   |