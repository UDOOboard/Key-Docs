This section contains the description of the custom BLE Profile and the various services included in it.  

# GATT Description Table
You can find the [GATT Description Table] here.

# Common Characteristics and Descriptors
Some features and some descriptors are common to most services. To avoid repetition, they are described in this section. Any variations will be described where necessary.

### User Description
It's a descriptor that contains a short text string. It's useful to identify the associated feature, especially when debugging and testing.  
This descriptor is defined by a specific standard Bluetooth GATT, [Characteristic User Description](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.descriptor.gatt.characteristic_user_description.xml), and has not been modified.  
All the implemented features include this descriptor.

### Characteristic Client Configuration (CCC)
It's a descriptor that enables notifications / instructions for the related feature.  
The time interval is usually specified in the characteristic **Notifind Period**.  
This descriptor is defined by a specific standard Bluetooth GATT, [Characteristic Client Configuration](https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.descriptor.gatt.client_characteristic_configuration.xml), and has not been modified.

### Enable
It's a feature with a Boolean field that enables (`1`) or disables (`0`) the sensor related to the service it belongs.

* `0` is for **Disabled**
* `1` is for **Enabled**

The default value is usually `0`.  

It's necessary to enable the sensor before using it.  

Reading the value of a disabled sensor returns `0`. It's a custom feature with a *128-bit UUID*.

### Notifind Period
It's a feature used to specify the time interval for notifications and / or directions. It's expressed in units of 10 ms. The Value attribute is a *16 bits unsigned integer*.  
Allowed values are between `0` and `6000` (maximum interval: 60s ).  
The notification / indication is automatically disabled when `0` is written.  
The default value is `10` (or 100 ms).

# Notes on the values of the UUID and attributes

### 16 and 128 bit UUID
The UUID values shown in the tables are always indicated by 16-bit (short UUID).
In fact, all the custom services and attributes are represented by 128 bits.
For these custom services / attributes we defined a base UUID:

    0xD7720000-79C6-452F-994C-9829DA1A4229 (base UUID)

To switch from a 16-bit UUID to the corresponding 128-bit value we need to replace the third and fourth bytes with the short UUID value.
For example, the short UUID of the of the temperature Resolution characteristic service is `0x69BB`, therefore its full UUID is:

    0xD77269BB-79C6-452F-994C-9829DA1A4229

In the [table of attributes], shorts UUID of personalized services are indicated by an asterisk (\*).

###  Inversion of attribute bytes
The CC2650 microcontroller operates in little-endian mode, but the transmission is performed in big-endian (network byte order) mode.
For that reason, the values of the attributes longer than 1 byte are transmitted in the reverse order: the least significant byte (LSB)  is transmitted as first and the most significant bit (MSB) as last. In values composed by multiple fields, the field order is preserved, but longer fields than byte are also inverted. Take for example:

* The attribute GATT Primary Service Declaration, whose value is `0x1800`, but is transmitted as `00:18`.
* The Value attribute of GreenLed characteristic, composed by the  two "status fields" and "blink_period" - default values are `0x00` and `0x05`: they are transmitted as `00:05`.
* The Accelerometer service attributes, consisting of three fields (X, Y, and Z) of two bytes each, are transmitted as XLSB: XMSB: YLSB: YMSB: ZLSB: ZMSB.
