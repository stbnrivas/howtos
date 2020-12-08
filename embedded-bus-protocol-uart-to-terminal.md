# UART terminal 

- search your UART interface in linux

```bash
sudo dmesg | egrep --color 'serial|ttyS|ttyUSB'
# [ 2808.766754] usbcore: registered new interface driver usbserial_generic
# [ 2808.766762] usbserial: USB Serial support registered for generic
# [ 2808.769653] usbserial: USB Serial support registered for cp210x
# [ 2808.771432] usb 2-3: cp210x converter now attached to ttyUSB0


ls /dev/tty{S*,USB*}
#/ dev/ttyS0  /dev/ttyS1  /dev/ttyS2  /dev/ttyS3  /dev/ttyUSB0
```


- report your serial

```bash
# sudo apt install setserial
setserial -g /dev/ttyS[0123]

# /dev/ttyS0, UART: unknown, Port: 0x03f8, IRQ: 4
# /dev/ttyS1, UART: unknown, Port: 0x02f8, IRQ: 3
# /dev/ttyS2, UART: unknown, Port: 0x03e8, IRQ: 4
# /dev/ttyS3, UART: unknown, Port: 0x02e8, IRQ: 3
```

## connect using cu

```bash
# sudo apt install cu
# Call Up otehr sistem
# cu -l /dev/device -s baud-rate-speed
cu -l /dev/ttyS0 -s 19200
```

## connect using screen


```bash
# sudo apt install screen
screen /dev/ttyS0 <speed>

# to detach session
# `CTRL+A` `D` or `CTRL+A` `CTRL+D`

# to exit and kill session
# `CTRL+A` `K`

# resume again with
screen -r
```



## connect using tio


```bash
# sudo apt install tio
# tio --help

# Usage: tio [<options>] <tty-device>
# Options:
#   -b, --baudrate <bps>        Baud rate (default: 115200)
#   -d, --databits 5|6|7|8      Data bits (default: 8)
#   -f, --flow hard|soft|none   Flow control (default: none)
#   -s, --stopbits 1|2          Stop bits (default: 1)
#   -p, --parity odd|even|none  Parity (default: none)
#   -o, --output-delay <ms>     Output delay (default: 0)
#   -n, --no-autoconnect        Disable automatic connect
#   -e, --local-echo            Do local echo
#   -t, --timestamp             Prefix each new line with a timestamp
#   -l, --log <filename>        Log to file
#   -m, --map <flags>           Map special characters
#   -v, --version               Display version
#   -h, --help                  Display help

tio -b 19200 /dev/ttyS0 
```

exit with `CTRL+T` `q`


```bash
# default options:

tio -b 115200 -d 8 -s 1 -p none -m /dev/ttyUSB0

```



```bash
-m, --map <flags>

          Map (replace, translate) special characters on input or output. The following mapping flags are supported:

          INLCR   Translate NL to CR on input.

          IGNCR   Ignore carriage return on input.

          ICRNL   Translate carriage return to newline on input (unless IGNCR is set).

          ONLCR   Map NL to CR-NL on output.

          OCRNL   Map CR to NL on output.

          If defining more than one flag, the flags must be comma separated.
```