This service manages the UDOO BAROMETER/ALTIMETER BRICK sensor **Freescale MPL3115A2**. It provides alternately measure the pressure (in Pascal) or altitude (in meters).

The following features are available:
* **Pressure**: Returns an unsigned integer 3 bytes long, of which only the last 20 bits are significant, containing the pressure value in Q18.2 format (ie 18 bits for the integer part and 2 bits for the part fractional).
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Altitude**: Returns a signed integer 3 bytes long, of which only the last 20 bits containing the altitude value in Q16.4 (ie 16-bit format for the integer part and 4 bits for the fractional part).
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: This feature differs slightly from what is described in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes) because the sensor can alternatively measure the pressure or the altitude, the value of this characteristic is used to select one of two magnitudes. The possible values are shown in Table below.

| Enable | Effect               |
|--------|----------------------|
| 0      | Sensor Disabled      |
| 1      | Pressure measurement |
| 2      | Altitude measurement |

* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).


It should be noted that, despite this service have two CCC descriptors, i.e. one for each size, notifications/directions can only be active for a magnitude at a time (which must still be enabled using the feature Enable).  

The **pressure** value returned by the feature can be converted to real value in **Pa** dividing the read value by `4`.  

The **altitude** value returned by the feature can be converted to real value in **meters** by dividing the read value by `16`.
