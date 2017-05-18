This service manages the gyroscope **Freescale FXAS21002C**.  

It provides different characteristics and some descriptors:
* **Angular Rate**: Returns the value of the angular velocity along the three axes. The angular velocity of each axis is stored in a two-byte field. The three axes are stored and read in the following order: X, Y, Z; the least significant byte of each axis is transmitted first (see 4.2.2).
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: see description in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Full Scale Range**: Specifies the scale for measuring angular velocity. They are allowed only five values, which also determine the resolution (sensitivity) of reading, as shown in Table below (where "dps" indicates the speed in degrees per second and "MDPS" the speed in thousandths of a degree per second).
* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).

The conversion of the angular velocity from the entire value of the characteristic to the actual value in MDPS can be obtained by multiplying the value read for resolution.


| Full Scale Range | Full Scale | Resolution  |
|------------------|------------|-------------|
| 0                | 2000 dps   | 62.5 mdps   |
| 1                | 1000 dps   | 31.25 mdps  |
| 2                | 500 dps    | 15.625 mdps |
| 3                | 250 dps    | 7.8125 mdps |
| 4                | 4000 dps   | 125 mdps    |
