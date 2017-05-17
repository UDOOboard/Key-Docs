This service allows you to control the UDOO Temperature BRICK sensor **Texas Instruments TMP75B** if connected.  

This service includes four characteristics:

* **Temperature**: Returns the last sensor reading.
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: see description in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Resolution**: displays and changes the resolution of the sensor.
* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).

The temperature is expressed as a signed integer of a variable number of bits between `9` and `12`.  

The default value of the resolution is *9 bits*. It corresponds to a *temperature resolution of 0.5 °C*.

The temperature reading returns a value of *two bytes*, only the first R bits are significant. The R number is determined by the resolution as indicated by Table below (the significant bits are indicated by X).  

The conversion of the temperature from the entire value to the actual value in °C can be obtained by multiplying the value read and resolution.

| Resolution (bit) | Significant Bit     | Resolution (°C) |
|------------------|---------------------|-----------------|
| 9                | XXXX XXXX X000 0000 | 0.5             |
| 10               | XXXX XXXX XX00 0000 | 0.25            |
| 11               | XXXX XXXX XXX0 0000 | 0.125           |
| 12               | XXXX XXXX XXXX 0000 | 0.0626          |


If you need Fahrenheit degrees you can convert the Celsius temperature to Fahrenheit temperature using a simple formula.

The temperature T in degrees Fahrenheit (°F) is equal to the temperature T in degrees Celsius (°C) times 9/5 plus 32:

    T(°F) = T(°C) × 9/5 + 32

or

    T(°F) = T(°C) × 1.8 + 32
