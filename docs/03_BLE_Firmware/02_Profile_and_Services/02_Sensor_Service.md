This service consists of a single characteristic, called **Sensors**, which displays a list of detected sensors to the I2C bus.  

The characteristic **Sensors** has a value attribute containing a *one byte long unsigned int*. Each bit represents a sensor, according to table below.

If the bit is `1`, the corresponding sensor has been detected and is working.

<span class="label label-warning">Heads up!</span> The Sensors value is set at the startup. If a sensor is connected/disconnected after the startup you need to restart the system to update the attribute value.

|Bit (position) | Sensor                |
|---------------|-----------------------|
|0              | Accelerometer         |
|1              | Magnetometer          |
|2              | Gyroscope             |
|3              | Temperature           |
|4              | Barometer/Altimeter   |
|5              | Humidity              |
|6              | Light                 |
|7              | *Reserved*            |
