## Overview

The **Texas Instruments CC2650** device is a wireless MCU targeting *Bluetooth*, *6LoWPAN* and *ZigBee®*, and ZigBee RF4CE remote control applications.  
The device is a member of the CC26xx family of cost-effective, ultralow power, 2.4-GHz RF devices. Very low active RF and MCU current and low-power mode current consumption provide excellent battery lifetime and allow for operation on small coin cell batteries and in energy-harvesting applications. The CC2650 device contains a 32-bit ARM Cortex-M3 processor that runs at 48 MHz as the main processor and a rich peripheral feature set that includes a unique ultralow power sensor controller. This sensor controller is ideal for interfacing external sensors and for collecting analog and digital data.

The Bluetooth Low Energy controller and the IEEE 802.15.4 MAC are embedded into ROM and are partly running on a separate ARM Cortex-M0 processor. This architecture improves overall system performance and power consumption and frees up flash memory for the application.

## Block Diagram

<a href="../img/cc2650_block_diagram.gif" target="_blank"><img style="width:500px; " src="../img/cc2650_block_diagram.gif"></a>

## Documentation Support

Here you can find the [TI CC2650 Datasheet](http://www.ti.com/product/CC2650/datasheet)

To receive notification of documentation updates, navigate to the device product folder on [ti.com (CC2650)](http://www.ti.com/product/CC2650).  
In the upper right corner, click on Alert me to register and receive a weekly digest of any product information that has changed. For change details, review the revision history included in any revised document. The current documentation that describes the CC2650 devices, related peripherals, and other technical collateral is listed in the following.

## Pin Diagram – RGZ Package

<a href="../img/cc2650_pinout.png" target="_blank"><img style="width:500px; " src="../img/cc2650_pinout.png"></a>

## RF Core
The RF Core contains an **ARM Cortex-M0** processor that interfaces the analog RF and base-band circuitries, handles data to and from the system side, and assembles the information bits in a given packet structure.  
The RF core offers a high level, command-based API to the main CPU. The RF core is capable of autonomously handling the time-critical aspects of the radio protocols (802.15.4 RF4CE and ZigBee, Bluetooth Low Energy) thus offloading the main CPU and leaving more resources for the user application. The RF core has a dedicated 4-KB SRAM block and runs initially from separate ROM memory. The ARM Cortex-M0 processor is not programmable by customers.
