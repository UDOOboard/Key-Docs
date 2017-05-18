This service manages the magnetometer **Freescale FXOS8700CQ**.  

It provides the following features:
* **Magnetic Field**: Returns the value of the magnetic field along the three axes. The value of each axis is stored in a two-byte field, as a signed integer. The three axes are stored in the following order: X, Y, Z; the least significant byte of each axis is transmitted first (see 4.2.2).
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: see description in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).


The magnetic field value returned by the feature has a fixed resolution of *0.1 mT*. As a result the integer value can be converted to real value in mT simply dividing the read value by *10*.
