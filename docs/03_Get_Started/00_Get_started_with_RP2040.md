
We learned how to program the ESP32 microcontroller and now it's time to get your hands on the RP2040!

We will install all the **dependencies**, in both Linux-based and Windows OSs, to play with the **MicroPython** framework.
We have chosen this development environment because it's easy to learn and has a great support from the community.

As for the other on-board microcontroller, there exist several frameworks that support the RP2040.
To write firmwares for the RP2040, you can use the official [C/C++ SDK](https://www.raspberrypi.com/documentation/microcontrollers/c_sdk.html), the [Rust crate](https://crates.io/crates/rp-pico) for the Pico board or the [Arduino SDK](https://github.com/earlephilhower/arduino-pico). Chose the one you feel more comfortable with.

---

We have recorded a vdeo in which all steps described below are directly executed on a PC.
<iframe
    width="640"
    height="480"
    src="https://www.youtube.com/embed/LbhPpFTLdg0"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>

Here a distinction between the Linux-based and Windows OSs is not needed, since MicroPython is independent on the host platform.

First of all you need to install `python3` and `python3-pip`, but they are already installed by following the [guide for ESP32 part](/03_Get_Started/00_Get_started_with_ESP32.md).  
You need also to install the `rshell` python package. It s needed to upload the python code and interact with the MicroPython interpreter running on the MCU.
In a command line, type:
```bash
python3 -m pip install rshell
```

Now upload the MicroPython firmware into RP flash.  
Donwload its latest release from [this page](https://micropython.org/download/rp2-pico/).  
Now, once the file is downladed, put the microcontroller in flash mode: firstly close the jumper **JP1** to allow the computer to interact with RP and connect the board to your PC using an USB Type-C cable. Now keep pressed the button **SW2** labeled as `BOOTSEL` and push the reset button **SW1**. After these operations, the board is detected as a removable device by your computer.  
Simply copy the just downloaded `.uf2` file and paste it into the removable drive. In this way you can program the Raspberry MCU!

Now that the MycroPython framework is loaded, crete a file called main.py and copy the following code on it.  
It will make the LED attached on pin 25 blinking each 750 milliseconds!

```python
from machine import Pin
import time

LED_PIN=25
led = Pin(LED_PIN, Pin.OUT)



while True :
    led.toggle ()
    time.sleep (.750)
```

To load the script on your board, move to the folder containing the `main.py` file using a command line (let's call it `rp` placed in `ws` folder), and type the following commands:
```bash
cd ws/rp
# Invoke the rshell program
rshell
# It will automatically find the board, if correctly plugged

# Now you can copy the main.py source file by copying it into /pyboard folder which represent the connected board
cp main.py /pyboard/main.py
```

To apply changes, close the `rshell` program and reset the board with on-board button **SW1**.

At this moment the LED will start blinking!

---

To implement complex project using MicroPyhton you can find [**its official documentation here**](https://docs.micropython.org/en/latest/) and the documentation for [**RP2040 specific functionalities here**](https://docs.micropython.org/en/latest/library/rp2.html).

Enjoy with your UDOO KEY!