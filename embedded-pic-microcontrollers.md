# parts of microcontroller


## internal

- program flash memory (store our program)

- RAM

- timing generation (has multiples generators)

  + High frecuency interruption oscilator `HFINTOSC`
  + Medium frecuency interruption oscilator `MFINTOSC`
  + Low frecuency interruption oscilator `MFINTOSC`

- !MCLR (used to reset the PIC)

- Ports

	+ PORT{A,B,C,D,E} used to interface the microcontroller to the outside world

- WDT (WatchDog Timer)

  automatically reset the processor after a given period as defined by the user extremelly important to exit from endless loop.

- Brown-Out Reset

it reset the circuitry holds untle the power supply return to an acceptable level

- `_XTAL_FREQ` define to compiler frequency of oscilator


## periphericals

- ADC (Analog to digital converter)
- DAC (Digital to Analog converter)
- CCP Module (Capture Compare Pulse)

  used to measure a particular number of falling or rising edges of a timer, allows the timing of an event

- PWM Module (Pulse Width Modulation)

  pulses are use to operate stuff like motors or thing that need a pulse to start

- Timers or Timerx block

- Comparators

  compare two voltages and gives a digital output to indicate which is larger

- FVR (Fixed voltage Reference)

	used to provide a stable reference voltage to the comparator DAC or ADC 

- Temperature Indicator

- EUSART (Enhanced Universal Synchronous Asynchornous Receiver Transmitter) 

  used for serial communications and a lot of external modules require this interface to communicate with microcontroller

- CLC (Configurable Logic Cell)

  provide a bit of onboard sequential an combinational login functions

- MSSP (Master Synchronous Serial Port) provides two modes of operation to be configured for use

  + SPI (Serial Peripheral Interface)
  + I2C (Inter Integrated Circuit)

- NCO (Numerically Controlled Oscillator)

  used to provide a very precise and fine resolution frequency at a duty cycle

- ZCD (Zero Cross Detection)

  detects the point when there is no voltage on the AC waveform

- GOG (Complementary Output Generator)

  it takes one PWM signal and convert into two complentary signals

- Operational Amplifiers

- HEF (high endurance flash block)

  is designed to be a replacemente for EEPROM 


## Input-Output

- TRIS register (TRIState)

his name comes from three states, it can be configured for:
  
  + output hight
  + output low
  + input

is used to make a port either an input or an output.

for instance:
 - to set PORTB as an output port, we do TRISB = 0
 - to set PORTB as an input  port, we do TRISB = 1

```c
TRISBbits.TRISB0 = 0; // set to output
TRISBbits.TRISB1 = 1; // set to input
```

it is imperative to remember that data will not move from the port register to the microcontroller until you give the rigth behaviour setting as input or output


- PORT Register

in general a pic hast a range of ports like PORTA-PORTX, each one of these has 8-bits 16-bit depending of the architecture. The port register essentially reads the voltage levels of the pins on the device


- Output Latch Registers (LAT)

the Latch register are an improvement on the PORT registers for writing data to output. Only the 18F contain LAT registers. It improves on problems associated with the PORT register for writing data to the pins. The problem occurs while simply using the PORT register as output and it read the actual voltage level on the pin

```c
/*
In General you should always
CONFIGURE using TRIS_X to set 0 as output 1 as input
WRITE using LAT_X
READ using PORT_X
*/
TRISBbits.TRISB2=0
LATBbits.LATB2=1;       // Write RB2
// or
TRISBbits.TRISB2=1
Data=PORTBbits.RB2;     // Read RB2

LATBbits.LATB2=~LATBbits.LATB2;       // Read/Write RB2
```

- ANSEL (Analog Select Register)

used to enable or disable analog input functions on an particular pin. 
  + Not needed when use I/O pin for output.
  + If you use pin I/O as input you need to set previusly corresponding ANSEL register

- Weak Pull-Up

the ports on pic have internal pull-up resistors, used to reduce the need of add external components like add resistance

```c
OPTION_REGbits.nWPUEN = 0; // global enable weak pull-ups resistor option
WPUBbits.WPUB0 = 1; // configure individual pin PINB0
```

- Peripheral Pin Select (PPS)

In previous PICs, the I/O ports had fixed functions with respect to which peripherals were accessed through which pins. In newer PPS was introduced to avoid this problem. A pin can be configured to access specific function

- OPTION_REG

The Option_Reg Register
is a Readable and Writable register that is used to control some modules of the PIC. This register is only available from bank 1 and bank 3.


|  Bit   |    7    |    6     |   5  |   4  |  3  |  2  |  1  | 0   |
|--------|---------|----------|------|------|-----|-----|-----|-----|
|  name  | -RBPU   |  INTEDG  |	TOCS | TOSE | PSA | PS2 | PS1 |	PS0 |


- PS0, PS1, PS2: (prescaler rate selection)

Those bits are Readable and Writable and after a reset they will get the value '1'. They are used to set the Prescaller rate. The values it can get are:

- PSA (Prescaller Assignment)

This bit is Readable and Writable and after a reset it will get the value 1. This bit is used to assign the prescaller to to the Watchdog timer or the Timer 0 module. The values it can get are:

  + 0: The prescaller is assigned to the Timer 0 module (TMR0)
  + 1: The prescaller is assigned to the Watchdog timer (WDT)

- TOSE (Timer 0 Sourde Edge select)

This bit is Readable and Writable and after a reset it will get the value 1. It is used to select the RA4/TOCKI pin clock edge (High to Low or Low to High) on which the Timer 0 will count. The values it can get are:

  + 0: Increment on Low to High
  + 1: Increment on High to Low

- INTEDG (RB0/INT pin interrupt edge select)

This bit is Readable and Writable and after a reset it will get the value 1. By altering this bit, you can select the RB0/INT pin pulse edge that the RB0/INT interrupt will occur. The values it can get are:

  + 0: The RB0/INT interrupt will occur on the falling edge of the RB0/INT pin
  + 1: The RB0/INT interrupt will occur on the rising edge of the RB0/INT pin

- -RBPU (PORTB Pull-up enable)

This bit is Readable and Writable and after a reset it will get the value 1. The RB ports have an internal programmable pull-up resistor to minimize the use of external pull-up resistors when needed. This bit will enable or disable those resistors. The values it can get are:

  + 0: The RB pull-up resistors are enabled
  + 1: The RB pull-up resistors are disabled


## interfacing actuators

use input and output microcontrollers to operate, DC motor, steeper motor and the servo motor.


## interrupts, timers, counters and PWM

polling versus interrupts method (and mask interrupts)

The interrupt service routine, aka interrupt handler, is essentially the piece of code that the microcontroller executes when an interrupt is invoked, it takes three to five instruction cycles (aka interrupt latency). The interrupt comes from many sources timers onboard peripherals even an external pin.

The microcontroler assings priorities to each interrupt. An interrupt with a higher priority takes precedence over a lower priority one. In addition the microcontroller can also mask an interrupt, which is like ignore it when the call for service happen.

IMPORTANT TO CONFIRM: into a PIC only exist one unique route of service to handle interruption, the same code should attend multiples interrupts.

IVT - (interrupt vector table)


Into PIC18 the interruption vector table ar into ROM location

```
Power-on reset            0x0000
High priority interrupt   0x0008
Low  priority interrupt   0x0018
```

- sources of interrupts in the PIC18

  + Timers 0, 1, 2, 3
  + Pins RB0, RB1, RB2 for external hardware INT0, INT1, INT2
  + PORTB-Change
  + Serial Communication's USART Interrupts receive and transmit
  + ADC (analog to digital converter)
  + CCP (Compare caputre pulse-width-modulation)

- INTCON (interrupt control register) used to enable or disable 

```
|  7  |   6  |    5   |   4    |   3  |   2    |   1    |   0   |
-----------------------------------------------------------------
| GIE | PEIE | TMR0IE | INT0IE | RBIE | TMR0IF | INT0IF | RB0IF |

GIE (Global interrupt Enable) 
  GIE = 0 => disable all interrupt, even if they are enabled individually
  GIE = 1 => interrupt are allowed, each interrupt source is enabled by setting his enable bit

TMR0IE (timer 0 interrupt enable)
  TMR0IE = 0 disable Timer 0 overflow as interrupt
  TMR1IE = 1 disable Timer 0 overflow as interrupt

INT0IE (enables or disables external interrupt)
  INT0IE = 0 => disable external interrupt 0
  INT0IE = 1 => enable external interrupt 0

PEIE (PEripheral Interrupt Enable)
```

The GIE must be set 0 bit is cleared by the PIC18 itself to make sure anoyter interrupt cannot interrupt while are servicing the current and at the end of teh ISR should restore the GIE to 1 

- PIR1 (interrupt control register 1) for peripheral interrupts
- PIE1 (interrupt enable register 1) for peripheral interrupts


TODO: where i can find the interrupt code
TODO: mask an interrupt
TODO: set a function as routine of interruption


- Most baseline PIC® devices do not implement interrupts at all; check the datasheet

- PIC mid-range devices utilize a single interrupt vector,

- PIC18 devices implement two separate interrupt vector locations and use a simple priority scheme 

In MPLAB® C18 with PIC18

There are 2 interrupt vector in PIC18, the high priority and low priority interrupt. Interrupt is settings are configured with INTCON register. IPEN bit in RCON need to be set to enable the interrupt priority levels.

```c
// timeout
T0CON = 0x85;
TMR0H = 0x85;
TMR0L = 0xEE;
// interrupt
INTCON = 0x20;                
INTCON2 = 0x04;               //TMR0 high priority
RCONbits.IPEN = 1;            //enable priority levels

// Since that C18 does not create ISR (Interrupt Service Routine) automatically...
// we need a goto instruction must be created at the vector to redirect the interrupt to the appropriate ISR. 

// In this example only the high priority ISR is used.
// the code below shows the setting for the ISR. 
// A code section is created at 0x08 which is the high interrupt vector to redirect the interrupt to the ISR. 
// Inside the ISR the timer period is reloaded back to 34286 
// so that 1s interrupt can be achieved. check is set in the ISR 
// to tell the main program to update the LCD. 

void high_isr(void);
/*****************High priority interrupt vector **************************/
#pragma code high_vector=0x08
void interrupt_at_high_vector(void)
{
  _asm GOTO high_isr _endasm
}

#pragma code
/*****************High priority ISR **************************/

#pragma interrupt high_isr
void high_isr (void){
 if (INTCONbits.TMR0IF){  // Interrupt Check   
   INTCONbits.TMR0IF = 0;                 
   TMR0H = 0x85;        //Timer Reload to count 1s
   TMR0L = 0xEE;                    
   second++;
   if (second == 200){
   	second = 0;
   } 
   check = 1;
 }
}
```


In MPLAB® XC8 C source code, a function can be written to act as the interrupt service routine by using the interrupt qualifier. Declare a function qualified with the "interrupt" keyword and the compiler will place it in the right place, and take care of saving any used registers and its restoration.

```c
/*****************************
Dependencies:   xc.h
Processor:      PIC16f1829
Complier:       XC8 v1.00 or higher 
*****************************/
#include <xc.h>        
void main(void)
{       
 
    TRISB = 0x3F;              // Port B bits 7 and 6 are output
    OPTION_REGbits.T0CS = 0;   // Timer increments on instruction clock
    INTCONbits.T0IE = 1;       // Enable interrupt on TMR0 overflow
    OPTION_REGbits.INTEDG = 0; // falling edge trigger the interrupt
    INTCONbits.INTE = 1;       // enable the external interrupt
    INTCONbits. GIE = 1;       // Global interrupt enable
    for(;;)
        CLRWDT();       // Idly kick the dog
    while (1);
}        
 
void interrupt   tc_int  (void)        // interrupt function 
{
    if(INTCONbits.T0IF && INTCONbits.T0IE) 
    {                                     // if timer flag is set & interrupt enabled
            TMR0 -= 250;             // reload the timer - 250uS per interrupt
            INTCONbits.T0IF = 0;     // clear the interrupt flag 
            PORTB = 0x40;            // toggle a bit to say we're alive
    }
 
}
```

For an enhanced 8-bit MCU that uses interrupts (Using High and Low priority):

```c
/*****************************
Dependencies:   xc.h
Processor:      PIC18f4520
Complier:       XC8 v1.00 or higher 
*****************************/
#include <xc.h>
 
int tick_count=0x0;
 
void main(void)
{
    T1CON = 0x01;               //Configure Timer1 interrupt
    PIE1bits.TMR1IE = 1;           
    INTCONbits.PEIE = 1;
    RCONbits.IPEN=0x01;
    IPR1bits.TMR1IP=0x01;       // TMR1 high priority ,TMR1 Overflow Interrupt Priority bit
    INTCONbits.GIE = 1;
    PIR1bits.TMR1IF = 0;
    T0CON=0X00;
    INTCONbits.T0IE = 1;        // Enable interrupt on TMR0 overflow
    INTCON2bits.TMR0IP=0x00;        
    T0CONbits.TMR0ON = 1;
    while (1);
}
 
void interrupt tc_int(void)             // High priority interrupt
{
    if (TMR1IE && TMR1IF)
    {
        TMR1IF=0;
        ++tick_count;
        TRISC=1;
        LATCbits.LATC4 = 0x01;
    }
}
 
void interrupt low_priority   LowIsr(void)    //Low priority interrupt
{
    if(INTCONbits.T0IF && INTCONbits.T0IE)  // If Timer flag is set & Interrupt is enabled
    {                               
        TMR0 -= 250;                    // Reload the timer - 250uS per interrupt
        INTCONbits.T0IF = 0;            // Clear the interrupt flag 
        ADCON1=0x0F;
        TRISB=0x0CF;
        LATBbits.LATB5 = 0x01;          // Toggle a bit 
    }
    if (TMR1IE && TMR1IF)
    {
        TMR1IF=0;
        ++tick_count;
        TRISC=0;
        LATCbits.LATC3 = 0x01;
    }
}
```

### Timers

a timer on a microcontroller can c
- count either regular clock pulses (thus making it is a timer)  
- count irregular clock pulses (thus making it is a counter)

check the datasheet to know how many timers have your PIC.

The timer needs a clock pulse to tick. This clock source can either be internal or external to the microcontroller. 

A timer 0 will increment every instruction cycle unless a prescaler is used. The prescaller is responsible flor slowing down the rate at which Timer 0 counts, the timer has 8 values which provide from 2-256 escale


## USART, SPI and I2C (serial communication protocols)

The protocols are different in the way they transmit and receive information on teh data bus lines, the data bus lines, polarity and teh clock, more significan bits meanings


| protocol |     nº wires                    | clock | synch strategy |  bit order |         communication mode    |
| -------- | --------------------------------|-------|----------------|------------|-------------------------------|
| UART     | 3/4 data, RX/TX                   | n/a   |                | LSB        | one-to-one or one-to-many PTP |
| SPI      | 4 SCLK, MOSI, MISO, SS          | SCLK  |                | MSB or LSB | one-to-many, single master multiple slave with more slave lines|
| I2C      | 2 data, clock                   | SCL   |                | MSB first  | one-to-many address for master slaves |
| USB      | 2 (D+/D-) |||||


### USART (universal synchronous asynchronous receiver transmitter)

4 wires?

Sometime see USART written as UART, thing USART is just an enhanced UART protocol without S of Synchronous that require a clock to be synchronous. The USART module onboard the PIC can be used synch o asynch

An important consideration for USART is the baud rate (transmission speed). A baud rate specify the rate of transfer data: A baud rate 2400 => transfer a maximum 240bits.

For example if you send signal to a LCD module that has selectable baud rates of 2400, 9600 you should check the datasheet.

when you need to communicate with a pc you can use a serial to usb converter


### SPI (Serial Peripheral Interface)

In SPI the clock is present because SPI communication use synchronous data transfer. In SPI always has only one mster device and althoug there can be many slaves.

SPI has several lines:
- Serial Clock (SCK)
- Master Out Slave In (MOSI)
- Master in Slave Out (MISO)
- Slave select (SS)

The disadvantages is that it use a lot of I/O lines.
The advantage of SPI is tha it can transfer million of bytes of data per seconds, useful to interactuate with SD cards


### I2C (inter integrated circuit)

I2C protocol is widely used and use only two lines but the communicatoin occurs at a slower rate and it is a very complex protocol.

I2C is unique when compared to the other protocols already shown, only one line is used for data flow. On 
the I2C bus, the device known as the master is used to communicate with another device known as teh slave
and the master can communicate with the slave because each device on the slave has its own address.

The lines used SCL (Serial Clock Line) and SDA (Serial Data Line) and the lines must be connected to VCC using pull-up resistors.

The speed most I2C devices use is either 10kHz or 400Khz. The protocol transmit information via frames and there are two types of frames:
- an address frame (which informw the bus which slave dvide will receive the message) followed by data frames 8-bit data
- an data frame

every frame has 9th bite called acknowledge (ACK) or not (NACK) bit, which is used to indicate whether teh slave device reads teh transmission.

Every I2C communication from tehe master starts with the master pulling the SDA line low an leaving the SCL line high. This is konon as teh start condition. Similarly, there is a stop condition, where there is a low-to-hight transition on SDA after a low-to-high transition on SCL with SCL being high.

into PICs SSPADD register value is used to determine teh clock rate for I2C

```
Frequency Clock = Fosc / [(SSPADD+1)*4]
```

## ADC and DAC

many times when you're working with microcontrollers, you might need to use analog to digital and digital to analog converters. These converters are crucial to operate modern devices, read battery status, read a sensor, read signal from potentiometer, increase the speed of a turbine...

- ADC  analog digital converter, converts analog voltages into a digital representation, ADC has a specific number of bits of resolution. Example 10 bits can read voltage in steps from 0 to 1023

- DAC  digital analog converter


## PIC Modules: NCO, Comparator, FVR

- CLC (Configurable Logic Cell) a module which provide a configurable logic for microcontrollers, you can configure from MCC into the MPLab IDE

- NCO (Numerically Controlled Oscillator) the output of NCO is a sqare wave that's dependet on the input clock and the valuegiven for the incremente postscaller, operate independent from the cores

- Comparator is a device that compares two analog voltages and outputs the difference between them

- FVR (Fixed Voltage Reference) provide a stable voltage of reference that can be used with comparator


## watchdog timer and low power

The argument has always been that 8-bit microcontrollers are superior to 32-bit ones in relation to low power. The reason is simply the number of transistors PIC microcontrollers offers the technology built-in XLP (Extreme Low Power)

### sleep mode 

the pic can be put into sleep mode by using the SLEEP instructiong. when this happens the pic can be woken up using an external interrupt on some pin

### wathdog (WDT)

is a timer which

# Dudas
