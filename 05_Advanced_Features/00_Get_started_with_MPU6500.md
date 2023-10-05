
# Get starte with MPU6500 IC

Those of you who purchased the UDOO KEY PRO will be eager to try the on-board sensors as soon as possible!  
In this guide we'll show you how to easily test the on-board accelerometer, MPU-6500, with the [esp-idf v5.0.2](https://docs.espressif.com/projects/esp-idf/en/v5.0.2/esp32/get-started) framework.

Install it on your PC and let's start coding!

## MPU tester project

The code we are going to see in this little guide has been already pushed on [this](FIXME) repository: those of you who want to quickly test and integrate the accelerometer driver on their project can clone, check and use it.

Instead, if you want an explanation about the wrote code, simply continue reading below.

## Step-by-step guide

First of all you have to install the esp-idf version 5.0.2 on your develoment PC: if you already haven't, install it following the instructions on the [offical Espressif page](https://docs.espressif.com/projects/esp-idf/en/v5.0.2/esp32/get-started/#installation).  
The developed project has been tested on Ubuntu 20.04 OS but. thanks to the esp-idf support, it can be compiled on each supported OS.

To communicate with the accelerometer and get sensed values we need the driver https://github.com/natanaeljr/esp32-MPU-driver.git developed by [natanalejr](https://github.com/natanaeljr).  
The project above depends on a wrapper around the esp-idf libraries to communicate over the ESP32 I²C bus: https://github.com/natanaeljr/esp32-I2Cbus.git.

Both of them will be added later as managed components using the [IDF Component Manager tool](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-component-manager.html).



### Project creation and setup

In this first step we will create the project.

Thanks to the `esp-idf` support it it a simple operation.  
You have to move to the workspace folder and type:

```SHELL
$ idf.py create-project mpu6500-tester
```

Then create the `idf_component.yml` file inside the main component folder and paste the following text:

```YAML
## IDF Component Manager Manifest File
dependencies:
  ## Required IDF version
  idf:
    version: ">=5.0.2"
```



### `accelerometer-driver` implementation

Firstly you have to create the new component by moving to the root project folder and creating the component `acclerometer-driver` typing:

```SHELL
$ cd mpu6500-tester
mpu6500-tester$ idf.py create-component accelerometer-driver -C components
```

Since the `esp32-MPU-driver` and `esp32-I2Cbus` components are written in C++, you can include them in your C++ project or, if your project is ocmposed by C sources, you need to create a wrapper around C++ classes in order to use them.  
Here we illustrate you the second way since the first one is a fairly simple operation and don't necessarily need a wrapper component.

So let's create the `MPU-driver-wrapper.cpp` file in the same directory of `accelerometer-driver.c` file: it will contain a set of functions that can be used to invoke C++ methods.  
Then update the `CMakeLists.txt` file content to include the just created file in the compilation process. The new content can be as follow:

```CMAKE
idf_component_register(
    SRCS "accelerometer-driver.c" "MPU-driver-wrapper.cpp"
    INCLUDE_DIRS "include")
```

To add required dependencies to `accelerometer-driver` component, create the `idf_component.yml` file in the root directory of the target component and paste the following text:

```YAML
## IDF Component Manager Manifest File
dependencies:
  ## Required IDF version
  idf:
    version: ">=5.0.2"

  MPU-driver:
    version: "master"
    git: https://github.com/natanaeljr/esp32-MPU-driver.git
  I2Cbus:
    version: "master"
    git: https://github.com/natanaeljr/esp32-I2Cbus.git
```

Finally, to clone locally the dependencies, go to the root folder of project and type:

```SHELL
idf.py reconfigure
```

Noe it's time to add the `acclerometer-driver` implementation!

---

First of all, define the data structures and functions inside the `accelerometer-driver.h` file: you need a sensor descriptor structure, an initializer for the component and two functions to read the accelerometer and gyroscope data.  
Since you cannot refer to a C++ classes inside a C source file, the `mpu6500_sensor_t` contains a `void *` reference which will point to the actual driver class.

The header file content can be as follow:

```C
#pragma once

#include <esp_err.h>

typedef struct
{
    void *driver_object;
} mpu6500_sensor_t;

esp_err_t mpu6500_sensor_init(mpu6500_sensor_t **target_sensor);
esp_err_t accelerometer_read(mpu6500_sensor_t *sensor, float *ax, float *ay, float *az);
esp_err_t gyroscope_read(mpu6500_sensor_t *sensor, float *gx, float *gy, float *gz);

```

The implementation of such functions, contained in `accelerometer-driver.c` file, can be:
```C
#include <esp_err.h>
#include <esp_log.h>

#include <string.h>

#include <accelerometer-driver.h>

const char *TAG = "accelerometer-driver";

extern void *mpu_get_new_driver_object();
extern esp_err_t mpu_accelerometer_read(void *, float *, float *, float *);
extern esp_err_t mpu_gyroscope_read(void *, float *, float *, float *);

esp_err_t mpu6500_sensor_init(mpu6500_sensor_t **target_sensor)
{
    if (*target_sensor != NULL) {
        ESP_LOGE(TAG, "Target sensor structure alreeady existing!");
        return ESP_ERR_INVALID_ARG;
    }

    *target_sensor = (mpu6500_sensor_t *) malloc(sizeof(mpu6500_sensor_t));
    memset(*target_sensor, '\0', sizeof(mpu6500_sensor_t));

    (*target_sensor)->driver_object = mpu_get_new_driver_object();

    return ESP_OK;
}

esp_err_t accelerometer_read(mpu6500_sensor_t *sensor, float *ax, float *ay, float *az)
{
    return mpu_accelerometer_read(sensor->driver_object, ax, ay, az);
}

esp_err_t gyroscope_read(mpu6500_sensor_t *sensor, float *gx, float *gy, float *gz)
{
    return mpu_gyroscope_read(sensor->driver_object, gx, gy, gz);
}
```

Such functions simply calls extern functions, that will be defined and implemented in `MPU-driver-wrapper.cpp` file, which contain the relevant business logic.

So the content of such file can be:

```C++
#include <esp_log.h>
#include <esp_err.h>

#include <MPU.hpp>
#include <I2Cbus.hpp>
#include <mpu/math.hpp>


static const char *TAG = "MPU-driver-wrapper";



extern "C" MPU_t *mpu_get_new_driver_object() {
    MPU_t *sensor = NULL;
    esp_err_t res = ESP_OK;
    
    i2c0.begin(GPIO_NUM_18, GPIO_NUM_21, 400000);

    sensor   = new MPU_t();
    sensor->setBus(i2c0);
    sensor->setAddr(mpud::MPU_I2CADDRESS_AD0_HIGH);

    if ((res = sensor->testConnection()) != ESP_OK) {
        ESP_LOGE(TAG, "Failed to connect to the MPU, error=%#X (%s)", res, esp_err_to_name(res));
        vTaskDelay(pdMS_TO_TICKS(100));
    }

    ESP_ERROR_CHECK(sensor->initialize());

    return sensor;
}




extern "C" esp_err_t mpu_accelerometer_read(MPU_t *MPU_driver, float *x, float *y, float *z) {
    mpud::raw_axes_t accelRaw;
    mpud::float_axes_t accelG;
    
    // Reading
    MPU_driver->acceleration(&accelRaw);
    // Converting
    accelG = mpud::accelGravity(accelRaw, mpud::ACCEL_FS_4G);

    *x = accelG.x;
    *y = accelG.y;
    *z = accelG.z;

    return ESP_OK;
}




extern "C" esp_err_t mpu_gyroscope_read(MPU_t *MPU_driver, float *x, float *y, float *z) {
    mpud::raw_axes_t gyroRaw;
    mpud::float_axes_t gyroDPS;
    
    // Reading
    MPU_driver->rotation(&gyroRaw);
    // Converting
    gyroDPS = mpud::gyroDegPerSec(gyroRaw, mpud::GYRO_FS_500DPS);

    *x = gyroDPS[0];
    *y = gyroDPS[1];
    *z = gyroDPS[2];

    return ESP_OK;
}
```

Now that we have the MPU driver implementation, let's dive into the main component implementation!



### Main component implementation

The main component is in charge of initializing the sensor and periodically print sensed values on the screen.  
The content of `mpu65000-tester.c` could be:

```C
#include <accelerometer-driver.h>
#include <esp_log.h>
#include <esp_err.h>
#include <freertos/FreeRTOS.h>
#include <freertos/task.h>

static const char* TAG = "mpu6500-tester";


void app_main() {
    mpu6500_sensor_t *sensor = NULL;

    ESP_ERROR_CHECK(mpu6500_sensor_init(&sensor));

    while (1) {
        float a_x, a_y, a_z, g_x, g_y, g_z;
        ESP_ERROR_CHECK(accelerometer_read(sensor, &a_x, &a_y, &a_z));
        ESP_LOGI(TAG, "A (x, y, z) : (%+6.2f, %+6.2f, %+6.2f)", a_x, a_y, a_z);
        ESP_ERROR_CHECK(gyroscope_read(sensor, &g_x, &g_y, &g_z));
        ESP_LOGI(TAG, "G (x, y, z) : (%+6.2f, %+6.2f, %+6.2f)", g_x, g_y, g_z);

        vTaskDelay(pdMS_TO_TICKS(4000));
    }
}
```



### Build and flash

Before build and flash the project, you have to select the correct MPU model. To configure the project, open the `menuconfig` tool typing in the rott folder project:
```BASH
$ idf.py menuconfig
```

Go to `Component config/MPU driver/MPU chip model` and select the `MPU6500` entry.

Then close saving the changed configuration and compile the project with:

```BASH 
$ idf.py build
```

To flash and monitor the execution type on the terminal:

```BASH
$ idf.py -p <serial_port> flash monitor
```

replacing `<serial_port>` with the actual port (generally `/dev/ttyUSB0` or similar on linux).

When the flash operation finished, press the reset button.  
If everything goes well, you will see on the terminal something like

```BASH
I (0) cpu_start: App cpu up.
I (217) cpu_start: Pro cpu start user code
I (217) cpu_start: cpu freq: 160000000 Hz
I (217) cpu_start: Application information:
I (222) cpu_start: Project name:     mpu6500-tester
I (227) cpu_start: App version:      1
I (232) cpu_start: Compile time:     Oct  4 2023 09:15:44
I (238) cpu_start: ELF file SHA256:  291a143921ded781...
I (244) cpu_start: ESP-IDF:          v5.0.2
I (248) cpu_start: Min chip rev:     v0.0
I (253) cpu_start: Max chip rev:     v3.99 
I (258) cpu_start: Chip rev:         v3.0
I (263) heap_init: Initializing. RAM available for dynamic allocation:
I (270) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (276) heap_init: At 3FFB2848 len 0002D7B8 (181 KiB): DRAM
I (282) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (289) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (295) heap_init: At 4008D0F8 len 00012F08 (75 KiB): IRAM
I (303) spi_flash: detected chip: generic
I (306) spi_flash: flash io: dio
I (311) cpu_start: Starting scheduler on PRO CPU.
I (0) cpu_start: Starting scheduler on APP CPU.
I (515) MPU6500: Reset!
I (515) MPU6500: Sample rate set to 100 Hz
I (515) MPU6500: Initialization complete
I (515) mpu6500-tester: A (x, y, z) : ( -0.00,  +0.03,  +0.99)
I (525) mpu6500-tester: G (x, y, z) : ( +0.20,  -0.24,  -0.21)
I (4525) mpu6500-tester: A (x, y, z) : ( -0.01,  +0.03,  +0.99)
I (4525) mpu6500-tester: G (x, y, z) : ( +0.56,  -0.61,  -0.40)
I (8525) mpu6500-tester: A (x, y, z) : ( -0.01,  +0.03,  +0.99)
I (8525) mpu6500-tester: G (x, y, z) : ( +0.52,  -0.56,  -0.46)
I (12525) mpu6500-tester: A (x, y, z) : ( -0.01,  +0.03,  +0.99)
```