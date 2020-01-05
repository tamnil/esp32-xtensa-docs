
# Experimental data from esp-idf

## Materials:

- Analog osciloscope 20Mhz
- Esp32 devkit v1 development board
- Example config file: "sdkconfig-test-without-delay"



## Results:

### Test without delay ESP-IDF framework:

```
@ 80Mhz: 1,1 μs => 0.91 Mhz
@ 160Mhz: 0,55 μs => 1.8 Mhz
@ 240Mhz: 0.35 μs => 2.86 Mhz
```

#### Note:

- detected some oscilation on osciloscope near 5 seconds of interval



### Source:
```


#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"
#include "sdkconfig.h"

#define BLINK_GPIO CONFIG_BLINK_GPIO

void app_main()
{
    gpio_pad_select_gpio(BLINK_GPIO);
    gpio_set_direction(BLINK_GPIO, GPIO_MODE_OUTPUT);

    while(1) {
        gpio_set_level(BLINK_GPIO, 0);
        gpio_set_level(BLINK_GPIO, 1);
    }
}

```





