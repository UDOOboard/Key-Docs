

After speaking a long about technical specifications and boards components, let's start doing things in order to load firmware in flash memory of microcontrollers!

Now we will install all **dependencies** and **framworks**, in Linux-based and Windows OSs, for ESP32 microcontroller and start **programming** it.  
The framework we chosen is the official one, the [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/index.html), but several other frameworks can be used to programming the ESP32. Among the others the most used are [MicroPython](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html) and [Arduino](https://github.com/espressif/arduino-esp32). Chose the one you prefer!


## Linux

[**Here**](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html) you can find the official documentation that explains with many more details the installation. For a quick guide read below!  
Additionally you can watch in the video below the full installation procedure explained and executed on a PC.
<iframe
    width="640"
    height="480"
    src="https://www.youtube.com/embed/HRT5CTC8D_4"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>

In addition to following packages, a text editor is required: you can use `VS Code` or `emacs` or wathever you want!

Open a terminal and type the following commands:

``` bash
# Install the essential dependencies
:~$ sudo apt install cmake wget git python3 python3-pip virtualenv
# Create the workspace folder (if it doesn't exist yet), clone the repository of ESP-IDF version 4.4.1 and install it
:~$ mkdir ~/ws/esp
:~$ cd ~/ws/esp
:~/ws/esp$ git clone --recursive https://github.com/espressif/esp-idf.git -b 4.4.1
:~/ws/esp/esp-idf$ cd esp-idf
:~/ws/esp/esp-idf$ bash install.sh esp32

# Before programming the ESP32, a set of environment variables need to be defined in the shell environment
#   Let's create an alias to easily load them and invoke it for each terminal you need
:~/ws/esp/esp-idf$ cd ~
:~$ echo "alias get_idf='. $HOME/ws/esp/esp-idf/export.sh'" >> ~/.bash_aliases
:~$ source $HOME/.bash_aliases
:~$ get_idf
# The environment now is correctly loaded!
```

---

Now it's the moment to create and load on your board the first program that makes blinking te two on-board LEDs!  
Open a terminal and type:

``` bash
# First of all load the needed variables by calling the alias
:~$ get_idf
:~$ cd ~/ws/esp
# Create the project
:~/ws/esp$ idf.py create-project blinker
:~/ws/esp$ cd blinker/main
:~/ws/esp/blinker/main$ 
# Noe paste the content of this file https://example.com on the blinker.c file that you can find in the current folder
#   It is the entry-point of your firmware and contains the instruction to perform the actions we want
```

Now that everything is ready, you can build and flash the program.
As explained in the video at the beginning of this page, you must leave the jumper **JP1** opened to drive the serial communication to ESP microcontroller and then you can connect your board to PC.  
After the connection, a serial port appears on your file system. Its path can be `/dev/ttyUSB0` or `/dev/ttyUSB1` or `/dev/ttyUSB2` and so on, depending if you already have connected serial devices. In the following commands, the port path is referred with `<PORT>` string.  
Finally you have to put the target MCU in flash mode, so close the jumper **JP2** and push the button **SW3** to reset it. The microcontroller can be programmed!

To do that, in a terminal with environment variales already loaded, type the following commands:
``` bash
:~$ cd ~/ws/esp/blinker
:~/ws/esp/blinker$ idf.py -p <PORT> build flash monitor
```

The above command will build the entire project (`build` command), will load the firmware into the ESP flash memory (`flash` command) and will monitor the output produced by the microcontroller and sent via the serial connection (`monitor` command).  
Keep in mind that you can also invoke `buld`, `flash`, and `monitor` commands separately.  
Type the command `idf.py help` to get the full list of available commands.

At this point the board need to be resetted to execute the just flashed firmware.  
Let's open the jumper **JP2** and push the reset button **SW3** to see LEDs in action!

## Windows

For Windows OS installation, Espressif provides an installer which automatically performs everything.  
Firstly download the installer [here](https://dl.espressif.com/dl/esp-idf/?idf=4.4) and launch it.

After the installation, you an open a **ESP-IDF prompt** by searching for **ESP-IDF 4.4 CMD** entry in the Start menu.  
Once launched, a new prompt is executed with the environment already loaded.

Now you can create a project, copy the code and flash the ESP32 in the same way explained for the Linux OS using an **ESP-IDF command prompt**.

---

To obtain more information about the Windows OS, [**here**](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html) you can find the official documentation.  