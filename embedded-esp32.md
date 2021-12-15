# Espressif 32


https://socialcompare.com/es/comparison/esp8266-vs-esp32-vs-esp32-s2

ESP3266  - year 2014
ESP8285  - year 2016
ESP32    - year 2016
ESP32    - year 2016
ESP32-S2 - year 2019
ESP32-C3 - year 2020

- successor of ESP8266 released september 2016
- dual core, 32-bit microcontroller modudel
- cpu cores can bee individually controlled
- clock frequency up to 240MHz
- multiple power modules
- integrated wifi, bluetooth and BLE (bluetooth low energy)
- multiple digital and anaglo I/O pins
https://socialcompare.com/es/comparison/esp8266-vs-esp32-vs-esp32-s2


- up to 18 12-bit ADC
- 2 8-bits DAC
- 10 capacitive touch sensors inputs
- 4 SPI bus channel
- 2 I2C bus connections
- 2 I2S bus connections (audio)
- 3 UART

- SD card host controller
- IR remote controller, up to eight channels
- motor PWN
- led PWM, up to sixteen channels
- real time clocks



WARNING: most pints have multiple functions, some function conflicts, not all can be used simultaneously
WARNING: not all development boards expose all pins
WARNING: some pins not recommended for use



Node MCu EsP-32S board has an ESP-WROOM-32







## installation

```
sudo apt-get install git wget libncurses-dev flex bison gperf python python-pip python-setuptools cmake ninja-build ccache libffi-dev libssl-dev



mkdir esp
cd esp
git clone -b v4.0.1 --recursive https://github.com/espressif/esp-idf.git
cd esp-idf/
./install.sh
source ./export.sh


```


in linux CTR+] don't stop monitor you can use CTR+ALT+5



```
# into ~/.bashrc

alias get_idf='. $HOME/esp/esp-idf/export.sh'
```





- create enviroment variables (for vscode) "${IDF_PATH}", "${IDF_TOOLS}"

```bash
IDF_PATH=~/esp/esp-idf
IDF_TOOLS_PATH=$HOME/.espressif
alias get_idf='. $HOME/esp/esp-idf/export.sh'
- create enviroment variables (for vscode)

```
"${IDF_PATH}",
"${IDF_TOOLS}"
```

- check variables







## problem don't recognize libraries for windows



### FIX 1

[https://github.com/abobija/esp-idf-vscode-boilerplate](https://github.com/abobija/esp-idf-vscode-boilerplate)

add to path
create .vs/c_cpp_properties.json

```json
{
    "env": {
        "defaultIncludePath": [
            "${env:IDF_PATH}/components/**",
            "${workspaceFolder}/main/**",
            "${workspaceFolder}/components/**",
            "${workspaceFolder}/build/config/*",
            "${env:IDF_PATH}/examples/common_components/protocol_examples_common/**"
        ],
        "defaultBrowsePath": [
            "${env:IDF_PATH}/components",
            "${workspaceFolder}/main",
            "${workspaceFolder}/components",
            "${workspaceFolder}/build/config",
            "${env:IDF_PATH}/examples/common_components/protocol_examples_common"
        ]
    },
    "configurations": [
        {
            "name": "ESP32",
            "includePath": [
                "${defaultIncludePath}"
            ],
            "browse": {
                "path": [
                    "${defaultBrowsePath}"
                ],
                "limitSymbolsToIncludedHeaders": false
            },
            "compilerPath": "xtensa-esp32-elf-gcc",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "compileCommands": "${workspaceFolder}/build/compile_commands.json"
        },
        {
            "name": "ESP8266",
            "includePath": [
                "${defaultIncludePath}"
            ],
            "browse": {
                "path": [
                    "${defaultBrowsePath}"
                ],
                "limitSymbolsToIncludedHeaders": false
            },
            "compilerPath": "xtensa-lx106-elf-gcc",
            "cStandard": "c11",
            "cppStandard": "c++11",
            "compileCommands": "${workspaceFolder}/build/compile_commands.json"
        }
    ],
    "version": 4
}

```
