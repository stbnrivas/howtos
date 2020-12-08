# Buses and Protocols

A bus is a collection of wires which carry electrical signeals. the electrical signals may be defined interm of voltage levels or current values. There are Parallel Buses and Serial Buses but the parallel buses are replacing by serial in the last times, and ever in mcu case becouse mcu have a low number of pins

The bit rate is diferent to baud rate in paralallel comunications, because there are multiples lines.


## serial communications

- Simplex
is a connection in which teh data flows in oly one direction, from the transmitter to the receiver.
- Half-Duplex
is a connection in which data flows in one direction or the other, but not both at the same time.
- Full-Duplex
each end of teh line can thus transmit and receive at the same time, which means that teh bandwidth is divide by two for each derection of data transmission if the same transmission medium is used for both directions.


## Transmission Rate:

for parallel data transfer, the data rate is specidfied in bytes/second but for serial communications, it always bits per seconds (bps), because teh data is sent on bit at a time

in microcontrollers typical examples of busess are

- SPI (Serial Peripheral Interface)
- I2C ()

## Synchronous and Asynchronous buses

The Synchronous bus is time by a clock signal, every device on the bus must run at the same clock rate and teh bus must be short to avoid clock skew problems

The Asynchronous bus is not clocked. It follows a hadshake protocol. It can accommodate a wide variety of devices, and the bus and be lenthended withou worrying about clock-skew or synchronization problems

## Bus Arbitration

When dealing with buses, bus arbitration is very encountered frequently: the activities that occur on a bus re called bus transactions. It amounts to putting up an addres and sendin/receiving data.  The deive that initieates a transaction is called a master and teh device that follows the orders of the master is called the slave

the simplest system is one in which there is one master adn one slave... A more complicated can have multiples master and multiples slaves

- bus arbitration schemes

  + priority: the highest priority module mus be serviced first
  + fairnes: even teh lowest priority module should be able to get service


### bus arbitration schemes

- daisy chaining

for single master and multiples slaves.. have three lines Tx, Rx and "BusBusy"

- parallel arbitration scheme

- distributed arbitration by self-selection


## On-board interface protocols for embedded systems

- USART

- SPI bus

developed by Motorola, (Serial Peripheral Interface) which is synchronous and full duplex, single master and multy and mulsty slave system, in which only one of the slaves is to be enabled at a time

- I2C protocol

developed by Philips, is its synchronous and means Inter-Integrated Circuit two wire and three lines SDA, SCL, CLK

- CAN bus (controller area network bus)





## UART / USART

son acronimos de Universal Asynchronous Receiver-Transmiter y Universal Sinchronous Asinchronous Receiver-Transmiter. Los controladores UART/USART se encargan de controlar la via serie.

En el caso de UART, se tratata se comunicacion asincrona, por lo que no hay señal de reloj: el bit rate debe acordarse previamente, por ejemplo:

-   1200 bps
-   4800 bps
-   9600 bps
-  19200 bps
-  38400 bps
- 115200 bps




En el UART se cuenta con lineas:

- Tx
- Rx
- Gnd
- Vcc


Los UART pueden trabajar con diferentes niveles logicos:
RS-232 opera entre -12v .. 12v
RS-422 opera entre   0v ..  5v
RS-485
RS-232c opera con niveles de voltaje TTL (Transistor Transistor Logic) opera entre   0v ..  5v

RS is for Recomend Standard


|                     |       RS 232    |      RS 422    |      RS 485    |
|---------------------|:---------------:|:--------------:|:--------------:|
| signal              |  single ended   | differential   | differential   |
| number of drivers   |  1              | 1              | 32             |
| number of receivers |  1              | 10             | 32             |
| operation           |  full duplex    | half duplex    | half duplex    |
| network topology    |  point to point | multidrop      | multipoint     |
| max distance        |     15m         | 1200m          | 1200m          |


La comunicacion en el protocolo UART con 8 bits y bit de paridad

- bit de inicio
- transmision de datos (8 bits)
- bit de paridad (paridad par, siempre se envia un nº par de 1 / paridad impar siempre se envia un nº impar de unos-)
- bit de parada (se puede mandar mas de un bit de parada)


si el UART se usan 7 bits  pueden representar por ejemplo 2^7 = 128 el codigo ASCIID https://www.ascii-code.com/
- ASCII control characters (character code 0-31)
- ASCII printable characters (character code 32-127)


si el UART se usan 8 bits puede representar 2^8 = 256 el
- ASCII control characters (character code 0-31)
- ASCII printable characters (character code 32-127)
- The extended ASCII codes (character code 128-255)



### transimsion

0. se configura la velocidad de transmision

los baudios representa el numero de simbolos por segurnod en un medio de transmision digital, cada simbolo puede comprender 1 o mas bits. un baudio equivale a un bit por segundo.


1. se envia el bit de inicio

eso sirve para sincronicar el reloj interno en el receptor para que coincida con el del transmisor

el bit de inicio es poner un 0 en la linea de datos durante un tiempo igual al inverso de la tasa de baudios


2. transmision de la informacion

se envian los bits de datos del caracter (cada bit es enviado en el mismo intervalo de tiempo), el receptor observa justo en la mitad de ese intervalo para evitar errores determinando si el bit es un 0 o un 1




3. bit de paridad
cuando el caracter ha sido enviado se agrega un bit de paridad, para que el receptor compruebe que la recepcion sea interpretada correctamente

4. bit de parada

al menos un bit de parada
ponemos a 1 logico la transmision


despues del bit de inicio 