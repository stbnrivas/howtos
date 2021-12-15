
# ESP32 ADC

https://github.com/espressif/esp-idf/blob/master/docs/en/api-reference/peripherals/adc.rst



```
.. only:: esp32

        Reading the internal hall effect sensor::

            #include <driver/adc.h>

            ...

                adc1_config_width(ADC_WIDTH_BIT_12);
                int val = hall_sensor_read();


    .. only:: esp32

        The value read in both these examples is 12 bits wide (range 0-4095).

    .. only:: esp32s2

        The value read in both these examples is 13 bits wide (range 0-8191).

    .. _adc-api-adc-calibration:

```