This service manages the three LEDs on the board.  

There are three characteristics, one for each LED, with identical structure and functions.  

As example we demonstrate here the one for the **Green LED**. The Green Led characteristic presents a Value attribute divided into two parts, each *one byte long*. The first part (called `STATUS`) pilot ignition of the LEDs. It is composed of two bits:
* **ONOFF** (bit 0): the LED status:
  * 1 - LED ON,
  * 0 - LED OFF.  
* **BLINK** (bit 1): the LED blink:
  * 1 - blink active
  * 0 - blink inactive.

The bit **BLINK** overcomes the bit **ONOFF**. So if BLINK = 1, the ONOFF value is ignored.  
The other bits of the STATUS field are not significant. The default value is 0x00.

The second field (`BLINK_PERIOD`) defines the length of each period of on / off during the flashing, in units of 100 ms. `0` produces the cancellation of the flashing and the LED is switched off. The default value is `5` (for a blink cycle equal to 1 second).   
For example, to flash the Green LED every 200 ms you will need to write in the attribute Value `0x0302`, 0x01\*\* to keep it turned on and to turn it off 0x00\*\* (where the sign '\*' indicates that the value is not significant). 
