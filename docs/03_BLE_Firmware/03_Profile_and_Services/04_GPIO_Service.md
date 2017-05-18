This service can check the `8 GPIO Pins` (A0, A1, A2, A3, A4, A5, D6, D7).  

Check the [Pinout page](!Hardware_Reference/Pinout) to locate this Pins in the Pinout of the UDOO BLU.


They can work as:
* [*Digital* Pins in *Input or Output* mode](https://en.wikipedia.org/wiki/General-purpose_input/output).  
* [*PWM Output*](https://en.wikipedia.org/wiki/Pulse-width_modulation) signal.
* *Analog Input* voltage data (Only the Pins: A0, A1, A2, A3, A4, A5)


User can manage these functions by the following characteristics:  

### Pin Mode

exposes a Value attribute composed by an *unsigned integer 16 bits long*. It's logically divided in 8 2-bit pairs. Each pair represents the pin operating mode.  

The following tables shows respectively the mapping of bit pairs of each pin, and the different operation modes.

| Pin | Bit Pair |
|-----|----------|
| A0  | 0:1      |
| A1  | 2:3      |
| A2  | 4:5      |
| A3  | 6:7      |
| A4  | 8:9      |
| A5  | 10:11    |
| D6  | 12:13    |
| D7  | 14:15    |

| Pair Value | Pin Mode       |
|------------|----------------|
| 00         | Digital Output |
| 01         | Digital Input  |
| 10         | Analog         |
| 11         | PWM            |

For example, to set the pin `D6` in `PWM` mode, you will need to write in the characteristic value `0x0300`.


### Digital Data
Exposes Value attribute composed by an *8-bit unsigned int*.  
Each bit represents the pin status:
* 0 LOW (GND)
* 1 HIGH (VDD).  

The write operation is performed only when the corresponding pin is set as *Digital Output* (see Pin Mode).  
The read operation, on the other hand, is always possible, but the value of each bit is meaningful only if the corresponding pin is in *Digital Input* or *Digital Output mode*.  
In *Digital Input* mode "floating" pins are read as `1`.  

The diagram below shows the mapping of the physical pin on the bits of the value of this feature:

|Bit (position) | Pin   |
|---------------|-------|
|0              | A0    |
|1              | A1    |
|2              | A2    |
|3              | A3    |
|4              | A4    |
|5              | A5    |
|6              | D6    |
|7              | D7    |

**Client Configuration Characteristic**: this descriptor is used to activate notifications for **Digital Data** characteristic. The notification is sent when a pin changes its state, and sends the entire Value attribute of **Digital Data**. The time interval specified in the characteristic **Notifind Period** is ignored.

### Analog Read
Allows the user to read an analog value of a pin. The pin to be read is selected by the Index characteristic (see below). The Value attribute is *two bytes long*, but only the *last 12 bits are significant* and provide the ADC data.  

**Characteristic Client Configuration**: see description in [Common Characteristics and Notes](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).

### Index
This value is an *unsigned 8 bits integer* field used to indicate which pin will be used in the next operation.  
Allowed values from `0` to `7` (corresponding to the pin A0, A1, A2, A3, A4, A5, D6, D7) or `0xFF`, but, as indicated in the table below, not all values are allowed for both operations. It is used to read all analog pin in sequence if set to `0xFF`.  
Each reading it is increased automatically, from 0 to 5.  
A further reading returns the index to 0, allowing a new cycle on all pins. If Pin Mode is different from `10` (Analog mode) it will return the value 0. It should be noted that, since the operation of Analog Read and PWM Config occurs subsequently to writing Index, UDOO BLU verifies only that the value Index falls within {0-7, FF}. If operation is requested later with an Index value not legal, it is silently ignored.

| Operation | Proper Index Value     |
|-----------|------------------------|
|Analog Read| 0, 1, 2, 3, 4, 5, FF   |
|PWM Config | 0, 1, 2, 3, 4, 5, 6, 7 |

### PWM Config
this characteristic is composed by two fields:
* **Frequency**: is an *32 bits unsigned integer* field used to set the PWM signal  frequency (Hz). It can vary from a minimum of `3` to a maximum of `24000000` (24 MHz). PWM signal starts immediately after the value is written. Writing `0` interrupt the signal.
* **Duty cycle**: is an *8-bit unsigned integer* field that is used to set the fraction of the period in which the PWM signal is high. It's percentage and vary between `0` and `100`.
It should be noted that the signal resolution is limited by the timer length, which is equal to 24 bits. For higher frequencies, frequency and duty cycle will be rounded to the nearest binary value. For example, a signal at 24 MHz may have 0% duty cycle only, 50% or 100%.  

**Notifind Period**: see description in [Common Characteristics and Notes](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes); the value is significant only when reading Analog pin.
