This service manages the accelerometer **Freescale FXOS8700CQ**. In addition to the punctual and periodic reading of the acceleration value, it is possible to enable notifications related to particular events.  

The service provides the following features and descriptors:
* **Acceleration**: Returns the value of the acceleration along the three axes. The acceleration of each axis is stored in a field of *two bytes*, but only the *last 14 bits* contain the actual value. The three axes are stored in the following order: `X`, `Y`, `Z;` the least significant byte of each axis is transmitted first (see the Notes in the [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes)).
  * **Characteristic Client Configuration**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Enable**: see description in [Common Characteristics and Notes page ](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Full Scale Range**: It Specifies the scale for measuring acceleration. Are allowed only three values (`0`, `1`, `2`). It determine the reading resolution, as shown in Table below (where g = 9.80665 m / s²).

| Full Scale Range | Full Scale | Resolution[m*g*] | Resolution[bit/*g*] |
|------------------|------------|------------------|---------------------|
| 0                | 2*g*       | 0,244            | 4096                |
| 1                | 4*g*       | 0,488            | 2048                |
| 2                | 8*g*       | 0,977            | 1024                |


* **Notifind Period**: see description in [Common Characteristics and Notes page](!BLE_Firmware/Profile_and_Services/Common_Characteristics_and_Notes).
* **Detection Type**: It specifies the detection type of the sensor. Following the allowed values:
  * 0: disabled;
  * 1: linear acceleration;
  * 2: inclination;  

* **Detection Flags**: is a *bitfield*. If each bit is set to 1 has the effect shown in Table below.

| Bit | Name         | Meaning                                                                                                       | Detection Type |
|-----|--------------|---------------------------------------------------------------------------------------------------------------|----------------|
| 0   | Use_Ref_Vals | If 1, uses the X, Y and Z reference as initial values, otherwise it uses the current ones.                    | 2              |
| 1   | Upd_Refs     | If 1, it updates the values values at the time of the event, otherwise it always uses the initial ones.       | 2              |
| 2   | Enable_X     | If 1, the X axis is used for detection.                                                                       | 1              |
| 3   | Enable_Y     | If 1, the Y axis is used for detection.                                                                       | 1              |
| 4   | Enable_Z     | If 1, the Z axis is used for detection.                                                                       | 1              |
| 5-7 | -            | Not used                                                                                                      |                |


* **Detection threshold**: Sets the notification; the value is interpreted as a function of Detection Type feature.
* **Reference X, Y Reference, Reference Z**: three *16-bit integers* that represent each of the initial value of reference on which to calculate the deviation. The resolution is set to Full Scale Range. They are used only when Detection Type is `1`.

Whenever Detection Type is changed, the Flags Detection values and Detection Threshold are updated with the default values, reported in the Table below.

| Detection Type | Detection Flag | Det. Threshold | Reference X,Y,Z | Notes                                             |
|----------------|----------------|----------------|-----------------|---------------------------------------------------|
| 0              | 0              | 0              | 0, 0, 0         | No detection                                      |
| 1              | 0x0C           | 300            | 0, 0, 0         | Acceleration of about 0.3g in X and Y directions. |
| 2              | 0              | 261            | 0, 0, 0         | Inclination of about 15°.                         |


The acceleration conversion from integer values of the characteristic Acceleration with the actual values in m*g* can be obtained by multiplying each value read for the resolution.

### Events Detection

The characteristics Detection Type, Detection Flags, Detection Threshold, Reference X, Y, and Z define the events detectable by the accelerometer.  
To enable this function user needs to turn enable the sensor(Enable = 1) and that Detection Type has one of the values indicated above.  
To get notifications you must enable Characteristic Client Configuration (CCC) descriptor through. It should be noted that setting CCC to `1` (i.e. 2 for directions) are also activated periodic notifications. Is necessary to reset the value of Notifind Period if these are not desired. The tale below summarizes the periodic notifications and events settings. Regarding Detection Flags, the three bits Enable_X / Y / Z allow to limit the detection only to some axes. However, if you are all set to `0`, the detection does not occur.

| Acceleration CCC | Notifind Period | Detection Type | Result                             |
|------------------|-----------------|----------------|------------------------------------|
| 0                | -               | -              | No notifications                   |
| 1                | 0               | 0              | No notifications                   |
| 1                | >0              | 0              | Periodical notifications           |
| 1                | 0               | >0             | Events notifications               |
| 1                | >0              | >0             | Periodical and Event notifications |

As for the inclination, the t value to be included in the Detection Threshold is related angle α that is to be detected by the following formula:

    t = | 2 sin (α / 2) | * 1000

For example, to detect an inclination of 15° or more will have to be

    t = | 2 sin (7.5°) | * 1000 = 261

Note: the value to be entered in the Detection Threshold is independent of the value of Full Scale Range.

Note: Currently, the three LEDs are used as visual notification for event detection:
* Green LED on: detection activated (i.e. Detection Type ≠ 0).
* Yellow LED: Switches to any detection of a linear acceleration event.
* Red LED: Switches to any detection of an inclination event.
