In order to update the firmware through the serial connection you need:
* Texas Instrument [SmartRF Flash Programmer 2(SFP2)](http://www.ti.com/tool/flash-programmer) - at least version 1.7.1
* Serial converter (3.3V USB/TTL serial converter)


<span class="label label-warning">Heads up!</span> The following procedure is for **Windows** only.

The procedure is the following:
1. Download and install the official TI [SmartRF Flash Programmer 2(SFP2)](http://www.ti.com/tool/flash-programmer).
2. Run it.
3. Connect the 3.3V USB/TTL serial converter to the PC.
4. In the **Connected devices** menu on the left, select the entry **Unknown** of the relative USB Serial Port (COM*) <br> <img src="../img/blu_upload_serial_1.png" alt="UDOO BLU Manager screens" class="img-responsive" >

5. In the **Select Target Device...** dropdown menu in the bottom left of the software select **CC2650** <br> <img src="../img/blu_upload_serial_2.png" alt="UDOO BLU Manager screens" class="img-responsive" >

6. Connect the 3.3V USB/TTL serial converter to the UDOO BLU like shown the image below. <br> <img src="../img/blu_upload_serial_3.png" alt="UDOO BLU Manager screens" class="img-responsive" >

7. Power up the UDOO BLU. Make sure to short the `D7` pin of the UDOO BLU to `GND` before powering up the board, this will set the UDOO BLU in **boot hardware mode** that allows you to update the firmware.
8. In SFP2 do the following step:
    1. in the **Flash Image(s)** section select the binary .hex file containing the firmware you want to upload.
    2. in the **Actions** section tick the **Erase**, **Program** and **Verify** checkboxes.
    3. Run the firmware upload clicking the **Play** button. <br> <img src="../img/blu_upload_serial_4.png" alt="UDOO BLU Manager screens" class="img-responsive" >

9. Wait until the end of the uploading procedure. The **Status** window on the bottom logs the process status. If it ends correctly, the bottom bar becomes green.
10. Turn off the UDOO BLU, detach the serial converter and turn on the board again to load the firmware just uploaded. You should see the LEDs blinking.
