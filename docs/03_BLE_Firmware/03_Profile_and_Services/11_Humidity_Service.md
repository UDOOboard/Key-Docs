This service lets you manage the UDOO Humidity BRICK sensor **Silicon Labs Si7006-A20**. It provides measuring relative humidity (RH) and optionally also the measurement of temperature.

The following features are available:
* **Relative Humidity**: Returns the last sensor reading.
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Temperatures**: Returns the last sensor reading.
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: This feature differs slightly from what is described in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes) because the sensor can measure both humidity and temperature, the value of this characteristic is used to select one of two sizes, or both. The possible values are shown in Table below.

| Enable | Effect                                        |
|--------|-----------------------------------------------|
| 0      | Sensor Disabled                               |
| 1      | Relative Humidity measurement                 |
| 2      | Temperature measurement                       |
| 3      | Relative Humidity and Temperature measurement |


* **Resolution**: exposes and allows you to change the resolution of the sensor.
* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).

The sensor reading (both humidity and temperature) returns an *unsigned integer value of two bytes*, of which only the first R bits are significant. The R number is determined by the resolution, and can take the values shown in Table below. By The temperature resolution is calculated automatically according to the correspondences in Table below.


The **default value** of the resolution is *12 bits* for the humidity and *14 bits* for the temperature.

| Humidity Resolution (bit) | Temperature Resolution (bit) |
|---------------------------|------------------------------|
| 8                         | 12                           |
| 10                        | 13                           |
| 11                        | 11                           |
| 12                        | 14                           |


 The sensor values can be converted to values in the international system according to the following formula:

    RH [%] = 125 * {Relative Humidity} / 65536-6

    Temperature [° C] = 175.72 * {Temperature} / 65536 - 46.85

Because of the accuracy of the sensor changes, it is possible that the RH value [%] returned by the formula is slightly less than 0 or greater than 100. This is a normal behavior, user can to limit the value returned by the formula interval [0,100].
