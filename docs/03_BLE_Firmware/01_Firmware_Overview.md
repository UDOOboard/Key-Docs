When **UDOO BLU** is powered on, after a brief initialization process, it enters in advertising state and starts sending beacons every *1000 ms*.  
At this stage it is possible to connect to UDOO BLU from other devices, and optionally to perform the pairing and/or bonding operations. During all these stages UDOO BLU works in slave mode, while the other device works in master mode.  
During the connection stage UDOO BLU sends  "non-connectable" beacons. In other words, UDOO BLU continues to announce its presence, but it won't be possible to establish further connections to other devices. After the current connection, UDOO BLU returns to its normal advertising stage, and can accept again a new connection.  
The flowchart of the application is shown below.  

<img src="../img/blu_firmware_flowchart.png" alt="UDOO BLU application flowchart" class="img-responsive" >

<br/>

Users can manage the the UDOO BLU by the two buttons (`BTN1` and `BTN2`):
* Pressing `BTN2` for at least *2 seconds* terminates the current connection.
* Pressing `BTN1` and `BTN2` simultaneously and for at least *3 seconds* erases all the keys stored in memory (i.e. delete all bondings).
To know the current status of UDOO BLU user can check the LEDs, as shown in the table below.

| LED                  | Action                        | UDOO BLU's status         |
|----------------------|-------------------------------|---------------------------|
| Green, Yellow, Red   | Blink 1 time in sequence      | Ready. Initialization end |
| Yellow               | Blink 3 times                 | Advertisement mode start  |
| Green                | Blink 3 times                 | Connection established    |
| Red                  | Blink 3 times                 | Connection error          |
| Red                  | Blink 2 times                 | Connection end            |
| Green + Yellow + Red | Blink 1 time at the same time | Bounding reset            |


## Pairing and Bonding

Through the pairing, UDOO BLU performs authentication with another device (already connected) and generates the keys that will then be used for encrypt the connection to that device. The characteristics of the board (no keyboard and no display) do not allow to be protected against MITM (man in the middle). The key exchange it's based on the "just works" method, which does not require password.

The bonding allows user to store the keys in the non-volatile memory, so that they can be reused in subsequent connection skipping the step of pairing - LTK (long term key). UDOO BLU can store up to 10 LTK. User can also delete all LTK, but in that case it  needs to redo the pairing with all the devices. The new keys will not necessarily be the same as the old. To delete the keys is necessary that the UDOO BLU is not connected to other devices. Finally, since UDOO BLU acts as a slave, the pairing and the bonding processes must be initiated by the master.

## Official firmware binaries released

You can find the official firmwares released in the UDOO github at the following links:  
* [**1.0A**](https://udooboard.github.io/UDOOBlu/OADFirmware/v1.0A.bin)
* [**1.0B**](https://udooboard.github.io/UDOOBlu/OADFirmware/v1.0B.bin)
* [**1.0C**](https://udooboard.github.io/UDOOBlu/OADFirmware/v1.0C.bin)

#### Firmwares description

| SENSE.A (1.0A)               | NO SENSE.B (1.0B)             | SENSE.C (1.0C)  |
|------------------------------|-------------------------------|-----------------|
| GPIO                         | GPIO                          | GPIO            |
| LEDs                         | LEDs                          | LEDs            |
| Accelerometer & Magnetometer | Temperature                   | Accelerometer   |
| Gyroscope                    | Barometer                     | Magnetometer    |
| Temperature                  | Humidity                      | Gyroscope       |
| Barometer                    | Ambient Light                 | OAD             |
| OAD                          | OAD                           | -               |
