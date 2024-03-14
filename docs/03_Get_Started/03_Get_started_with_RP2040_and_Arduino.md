
In this guide you will learn how to play with the **Arduino** framework and the *RP2040* microcontroller of your new **UDOO KEY board**.  
It is quite easy since it works like any other Raspberry Pi PICO board.

First of all, let's download and install the Arduino IDE following the [official documentation](https://support.arduino.cc/hc/en-us/articles/360019833020-Download-and-install-Arduino-IDE).

Now you have to properly setup the IDE in order to use the board.

Close the jumper labeled with `Serial Sel` to drive the USB communication to the RP2040 and connect the board to your PC using a USB cable.
The connected device will be discovered by your PC as COM6 port in Windows OS or as `/dev/ttyACM0` device in Linux based OSs.
Check the correct port or device before continuing.

Once the port has been found, open the IDE and follow the instructions below to **add the Raspberry Pi Pico to the board manager**.

Open Preferences window by selecting `File` and then `Preferences...`.
<img src="../img/programming_pico_s0.png" alt="Programming Pico - step 0" style="width:500px;"></img>

On the *Settings* tab, insert the URL [https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json](https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json) in `Additional boards manager URLs` field and then click on the `OK` button.
<img src="../img/programming_pico_s1.png" alt="Programming Pico - step 1" style="width:500px;"></img>

Install the RP2040 board support from the Boards Manager by selecting `Tools`, `Board` and `Boards Manager...`.
<img src="../img/programming_pico_s2.png" alt="Programming Pico - step 2" style="width:500px;"></img>

Search the `pico` text and, among the filtered results, select **Raspberry Pi Pico/RP2040** and click the **INSTALL** button.
<img src="../img/programming_pico_s3.png" alt="Programming Pico - step 3" style="width:500px;"></img>

When the installation has finished, select the correct connected board and its port, depending on the OS.
On Windows it will be something like COM6 (use the `Device Manager` to find the correct one) and on Linux based OSs you will have a device file like `/dev/ttyACM0`.
<img src="../img/programming_pico_s4.png" alt="Programming Pico - step 4" style="width:500px;"></img>

Now choose the example you want to load on the microcontroller clicking on `File`, `Examples`, `rp2040` and then on the project.
In this guide we will flash the `Fade` sketch.
<img src="../img/programming_pico_s5.png" alt="Programming Pico - step 5" style="width:500px;"></img>

Finally you can upload the sketch to the microcontroller by clicking the "Upload" button.
The IDE will put automatically the MCU in flash mode without the need of additional user operations.
<img src="../img/programming_pico_s6.png" alt="Programming Pico - step 6" style="width:500px;"></img>

Once the upload has finished, the on-board led will start to fade as expected!
