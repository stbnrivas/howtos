# ESP32


ESP32-WROOM-32D existen opciones de flash de 4 8 y 16MB

un modulo de ESP32 como el ESP-WROOM-32 contiene en su interior
- el esp32 que contiene el procesador y la memoria SRAM 520Kb en el caso de ESP32 y 320Kb en el caso del ESP32-S2
- un modulo memoria flash de 4Mb donde se guardan el codigo, ficheros y otras cosas



la SRAM esta dividida en:

- DRAM, mantiene las variables, el heap y los stack de las tareas
- IRAM, mantiene el codigo (intrucciones) y las interrupciones



la DRAM está a su vez dividida entre
- la memoria asignada en tiempo de compilacion (staticamente)
- la memoria asignada de forma dinamica usando malloc en ejecucion



```c
int heap = xPortGetFreeHeapSize();
int dram = heap_caps_get_free_size(MALLOC_CAP_8BIT);
int iram = heap_caps_get_free_size(MALLOC_CAP_32BIT) - heap_caps_get_free_size(MALLOC_CAP_8BIT);

```



```bash
```




BSS (from Block Started by Symbol) In C, statically-allocated objects without an explicit initializer are initialized to zero (for arithmetic types) or a null pointer (for pointer types). I