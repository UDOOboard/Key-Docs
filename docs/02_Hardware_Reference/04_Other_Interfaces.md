## LEDs and Buttons

UDOO BLU features **3 LEDs** with different colors:

* Green
* Yellow
* Red

**LED Status table**

Using one of the official UDOO firmwares you will find the LED behaviors listed in the table below:

| LED                  | Action                        | UDOO BLU's status         |
|----------------------|-------------------------------|---------------------------|
| Green, Yellow, Red   | Blink 1 time in sequence      | Ready. Initialization end |
| Yellow               | Blink 3 times                 | Advertisement mode start  |
| Green                | Blink 3 times                 | Connection established    |
| Red                  | Blink 3 times                 | Connection error          |
| Red                  | Blink 2 times                 | Connection end            |
| Green + Yellow + Red | Blink 1 time at the same time | Bounding reset            |


**Buttons**

UDOO BLU features **2 Buttons** to be used by the user.


## Bricks connector

**UDOO BRICKS** are modules you can use to augment your UDOO BOARDS and make them more versatile. Attach them into I2C Bricks snap-in connector with the related cable. UDOO BRICKS work along a cascade configuration, so you can attach them all together without wasting space in a truly intuitive way. Thanks to such configuration you can use cables up to 3,5 m long to connect UDOO BRICKS one another.

In the **UDOO BLU** the I2C Bricks snap-in connector is connected to the **I2C2** of the TI CC2650 MCU.

<a href="../img/blu_brick_connector.png" target="_blank"><img style="width:250px; " src="../img/blu_brick_connector.png"></a>
