The UDOO BLU BLE Firmware can be updated wireless Over-The-Air.

This procedure is called **OAD (Over-The-Air Donwload)** by Texas Instruments.

Since the flash memory size of the TI CC2650 micro-controller is 128KiB not all the features(services) can be contained in a single Firmware.  
We provide more than one Firmware to cover all the features of the UDOO BLU board.

You can upload the Firmware of the UDOO BLU using the OAD procedure in the [UDOO BLU Manager Android App](!BLE_Libraries_and_Tools/UDOO_BLU_Manager_Android_App) via BLE.

Inside the **OAD** section of the App you can find the available BLE Firmwares(with description) you can upload on the UDOO BLU.

The **UDOO BLU Manager** App use the [UDOOBluLib](!BLE_Libraries_and_Tools/BLE_Libraries) and the [Connection Control and OAD services](!BLE_Firmware/Profile_and_Services/Connection_Control_and_OAD_Services) to upload the Firmware on the UDOO BLU board.


<img src="../img/blu_app_screen_oad.png" alt="UDOO BLU Manager OAD" class="img-responsive" width="350px" >
