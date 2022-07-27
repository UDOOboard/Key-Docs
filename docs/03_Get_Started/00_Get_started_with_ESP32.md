

After speaking a long about technical specifications and boards components, let's start doing things in order to load firmware in flash memory of microcontrollers!

Now we will install all **dependencies** and **frameworks**, in Linux-based and Windows OSs, for ESP32 microcontroller and start **programming** it.  
The framework we chose is the official one, the [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/index.html), but several other frameworks can be used to programming the ESP32. Among the others the most used are [MicroPython](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html) and [Arduino](https://github.com/espressif/arduino-esp32). Choose the one you prefer!


## Linux

[**Here**](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html) you can find the official documentation that explains with many more details the installation. For a quick guide read below!  
Additionally you can watch in the video below the full installation procedure explained and executed on a PC.
<iframe
    style="border:none;overflow:hidden;display:block;margin:0 auto;"
    width="640"
    height="480"
    src="https://www.youtube.com/embed/HRT5CTC8D_4"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>

In addition to following packages, a text editor is required: you can use `VS Code` or `emacs` or whatever you want!

Open a terminal and type the following commands:

``` bash
# Install the essential dependencies
sudo apt install cmake wget git python3 python3-pip virtualenv
# Create the workspace folder (if it doesn't exist yet), clone the repository of ESP-IDF version 4.4.1 and install it
mkdir ~/ws/esp
cd ~/ws/esp
git clone --recursive https://github.com/espressif/esp-idf.git -b 4.4.1
cd esp-idf
bash install.sh esp32

# Before programming the ESP32, a set of environment variables need to be defined in the shell environment
#   Let's create an alias to easily load them and invoke it for each terminal you need
cd ~
echo "alias get_idf='. $HOME/ws/esp/esp-idf/export.sh'" >> ~/.bash_aliases
source $HOME/.bash_aliases
get_idf
# The environment now is correctly loaded!
```

---

Now it's the moment to create and load on your board the first program that makes the two on-board LEDs blink!  
Open a terminal and type:

``` bash
# First of all load the needed variables by calling the alias
get_idf
cd ~/ws/esp
# Create the project
idf.py create-project blinker
cd blinker/main
```

Open the `blinker.c` file inside current folder and copy the content below inside it.  
It is the entry-point of your firmware and contains the instruction to perform the actions we want.


``` C
#include <stdio.h>

#include <driver/gpio.h>
#include <freertos/FreeRTOS.h>
#include <freertos/task.h>

#define B_LED_PIN GPIO_NUM_32
#define Y_LED_PIN GPIO_NUM_33


void led_blinker_task () {
    gpio_pad_select_gpio(B_LED_PIN);
    gpio_set_direction (B_LED_PIN, GPIO_MODE_OUTPUT);
    gpio_pad_select_gpio(Y_LED_PIN);
    gpio_set_direction (Y_LED_PIN, GPIO_MODE_OUTPUT);

    while (1) {
        gpio_set_level(Y_LED_PIN, 0);
        gpio_set_level(B_LED_PIN, 0);

        gpio_set_level(B_LED_PIN, 1);
        vTaskDelay(pdMS_TO_TICKS(128));
        gpio_set_level(B_LED_PIN, 0);
        vTaskDelay(pdMS_TO_TICKS(128));
        gpio_set_level(B_LED_PIN, 1);
        vTaskDelay(pdMS_TO_TICKS(128));
        gpio_set_level(B_LED_PIN, 0);
        
        gpio_set_level(Y_LED_PIN, 1);
        vTaskDelay(pdMS_TO_TICKS(2000));
    }
}


void app_main(void) {
    xTaskCreate (&led_blinker_task, "led_blinker_task", 1024, NULL, 2, NULL);
}
```

Now that everything is ready, you can build and flash the program.
As explained in the video at the beginning of this page, you must leave the jumper **JP1** opened to drive the serial communication to ESP microcontroller and then you can connect your board to PC.  
After the connection, a serial port appears on your file system. Its path can be `/dev/ttyUSB0` or `/dev/ttyUSB1` or `/dev/ttyUSB2` and so on, depending if you already have connected serial devices. In the following commands, the port path is referred with `<PORT>` string.  
Finally you have to put the target MCU in flash mode, so close the jumper **JP2** and push the button **SW3** to reset it. The microcontroller can be programmed!

To do that, in a terminal with environment variales already loaded, type the following commands:
``` bash
cd ~/ws/esp/blinker
idf.py -p <PORT> build flash monitor
```

The above command will build the entire project (`build` command), will load the firmware into the ESP flash memory (`flash` command) and will monitor the output produced by the microcontroller and sent via the serial connection (`monitor` command).  
Keep in mind that you can also invoke `build`, `flash`, and `monitor` commands separately.  
Type the command `idf.py help` to get the full list of available commands.

At this point the board need to be resetted to execute the just flashed firmware.  
Let's open the jumper **JP2** and push the reset button **SW3** to see LEDs in action!

## Windows

For Windows OS installation, Espressif provides an installer which automatically performs everything.  
Firstly download the installer [here](https://dl.espressif.com/dl/esp-idf/?idf=4.4) and launch it.

After the installation, you can open a **ESP-IDF prompt** by searching for **ESP-IDF 4.4 CMD** entry in the Start menu.  
Once launched, a new prompt is executed with the environment already loaded.

Now you can create a project, copy the code and flash the ESP32 in the same way explained for the Linux OS using an **ESP-IDF command prompt**.

---

To obtain more information about the Windows OS, [**here**](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html) you can find the official documentation.  