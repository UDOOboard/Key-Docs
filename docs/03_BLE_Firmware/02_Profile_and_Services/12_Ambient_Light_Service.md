This service allows you to manage the UDOO LIGHT BRICK sensor **TAOS TSL2561T**.  

It provides the following features and descriptors:
* **Illuminance**: returns the ambient light level, which is stored in a *two-byte field as an unsigned integer*. The return value is already expressed in lux and requires no additional conversions.
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: see description in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Sensing period**: specifies the duration of the measurement. Periods greater return more accurate values (higher resolution). The sensing period is specified in units of 10 ms, with a maximum value of 100 (equal to 1 second). The default value is `10`.
* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
