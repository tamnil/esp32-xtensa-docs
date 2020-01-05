
# Experimental data from esp-idf

## Materials:

- Analog osciloscope 20Mhz
- Esp32 devkit v1 development board
- Example config file: "sdkconfig-test-without-delay"



## Results:

### Test without delay ESP-IDF framework:


@ 80Mhz: 1,1 μs => 0.91 Mhz
@ 160Mhz: 0,55 μs => 1.8 Mhz
@ 240Mhz: 0.35 μs => 2.86 Mhz

#### Note:

- detected some oscilation on osciloscope near 5 seconds of interval



### Source:
```


/* Blink Example

   This example code is in the Public Domain (or CC0 licensed, at your option.)

   Unless required by applicable law or agreed to in writing, this
   software is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
   CONDITIONS OF ANY KIND, either express or implied.
*/
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"
#include "sdkconfig.h"

/* Can run 'make menuconfig' to choose the GPIO to blink,
   or you can edit the following line and set a number here.
*/
#define BLINK_GPIO CONFIG_BLINK_GPIO

void app_main()
{
    /* Configure the IOMUX register for pad BLINK_GPIO (some pads are
       muxed to GPIO on reset already, but some default to other
       functions and need to be switched to GPIO. Consult the
       Technical Reference for a list of pads and their default
       functions.)
    */
    gpio_pad_select_gpio(BLINK_GPIO);
    /* Set the GPIO as a push/pull output */
    gpio_set_direction(BLINK_GPIO, GPIO_MODE_OUTPUT);
    while(1) {
        /* Blink off (output low) */
	/* printf("Turning off the LED\n"); */
        gpio_set_level(BLINK_GPIO, 0);
        /* vTaskDelay(1 / portTICK_PERIOD_MS); */
        /* Blink on (output high) */
	/* printf("Turning on the LED\n"); */
        gpio_set_level(BLINK_GPIO, 1);
        /* vTaskDelay(1 / portTICK_PERIOD_MS); */
    }
}

```





