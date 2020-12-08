# Espressif 32


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





- create enviroment variables (for vscode)

```
"${IDF_PATH}",
"${IDF_TOOLS}"
```

- check variables



