Consulting the [BLE Firmware](!BLE_Firmware/BLE_Overview) section you can develop your BLE software to communicate with the UDOO BLU using the programming language you prefer.  
Usually every programming language provides standard BLE libraries to manage BLE communication with a BLE peripheral like UDOO BLU.

In this section you can find some useful high-level libraries to communicate with the UDOO BLU easily.

# Android Library - UDOOBluLib

**UDOOBluLib** is the Official Android library to communicate with the UDOO BLU via BLE.

You can find all the source code and info about the library in the [UDOOBluLib Github page](https://github.com/UDOOboard/UDOOBluLib-android).

The [UDOO BLU Manager](!BLE_Libraries_and_Tools/UDOO_BLU_Manager_Android_App) Android App use this library to manage the UDOO BLUs.

### Installation

Include the library as local library project or add the dependency in your build.gradle.

    repositories { maven { url "http://dl.bintray.com/udooboard/maven" } }
    ...

    dependencies { compile 'org.udoo:udooblulib:0.4.2' }

### Usage

Check the README on the Github page to more info about the usage.


# Nodejs Library - node-udoo-blu

**udoo-blu** is the Official Nodejs library to communicate the the UDOO BLU via BLE.

You can find all the source code and info about the library in the [node-udoo-blu Github page](https://github.com/UDOOboard/node-udoo-blu).

### Installation

Since the package is published on [npm](https://www.npmjs.com/) you can simply install the library:

    npm install udoo-blu

### Usage

Check the all the `test*` files in the main folder to find examples of how to use UDOO BLU features.
