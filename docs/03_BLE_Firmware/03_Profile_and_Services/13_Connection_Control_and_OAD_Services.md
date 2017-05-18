**Connection Control** and **OAD** services manage the wireless OTA (Over-The-Air) firmware update using BLE.  

This procedure is called **OAD (Over-The-Air Donwload)** by Texas Instruments.

These two services were developed by Texas Instruments and included in this firmware without any modification.

For a description of the services and use reference check:
* Texas Instruments Inc., SimpleLink™ Bluetooth® low energy CC2640 wireless MCU – Over-the-Air
Download User’s Guide – For BLE-Stack™ Version: 2.1.0 / 2.1.1, January 2016.
* [CC2650 SensorTag User's Guide](http://processors.wiki.ti.com/index.php/CC2650_SensorTag_User's_Guide)

<span class="label label-warning">Heads up!</span> Services Connection Control and SROs have a base UUID different from that reported in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).  
Specifically, the base UUID for these services is:

    0xF000 **** 04514000B000000000000000.
