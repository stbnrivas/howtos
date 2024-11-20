# Espressif 32



## ESP-WROOM-32

- successor of ESP8266 released september 2016
- dual core, 32-bit microcontroller modudel
- cpu cores can bee individually controlled
- clock frequency up to 240MHz
- multiple power modules
- integrated wifi, bluetooth and BLE (bluetooth low energy)
- multiple digital and anaglo I/O pins

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
sudo dnf install git wget flex bison gperf python3 python3-pip python3-setuptools cmake ninja-build ccache dfu-util libusbx

sudo dnf install

sudo apt-get install git wget libncurses-dev flex bison gperf python python-pip python-setuptools cmake ninja-build ccache libffi-dev libssl-dev




sudo usermod -a -G dialout $USER




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

```
- check variables



