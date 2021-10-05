
# Lab 2: Martin Knob

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/xknobm00/Digital-electronics-2](https://github.com/xknobm00/Digital-electronics-2)


 [Calculate LED resistor value](https://electronicsclub.info/leds.htm) for typical red and blue LEDs.

&nbsp;
![ohms law](Images/ohms_law.png)  (5-2)/0,02 = 150 Ω
&nbsp;

&nbsp;
![ohms law](Images/ohms_law.png)  (5-3)/0,02 = 100 Ω
&nbsp;

| **LED color** | **Supply voltage** | **LED current** | **LED voltage** | **Resistor value** |
| :-: | :-: | :-: | :-: | :-: |
| red | 5&nbsp;V | 20&nbsp;mA | 2&nbsp;V | 150&nbsp;Ω |
| blue | 5&nbsp;V | 20&nbsp;mA | 3&nbsp;V | 100&nbsp;Ω |


### Active-low and active-high LEDs

1. Complete tables according to the AVR manual.

| **DDRB** | **Description** |
| :-: | :-- |
| 0 | Input pin |
| 1 | Output pin |

| **PORTB** | **Description** |
| :-: | :-- |
| 0 | Output low value |
| 1 | Output high value |

| **DDRB** | **PORTB** | **Direction** | **Internal pull-up resistor** | **Description** |
| :-: | :-: | :-: | :-: | :-- |
| 0 | 0 | input | no | Tri-state, high-impedance |
| 0 | 1 | input | yes | Pxn will source current if ext. pulled low |
| 1 | 0 | output | no | output low |
| 1 | 1 | output | no | output high |


| **Port** | **Pin** | **Input/output usage?** |
| :-: | :-: | :-- |
| A | x | Microcontroller ATmega328P does not contain port A |
| B | 0 | Yes (Arduino pin 8) |
|   | 1 | yes, pin 9 |
|   | 2 | yes, pin 10 |
|   | 3 | yes, pin 11 |
|   | 4 | yes, pin 12 |
|   | 5 | yes, pin 13 |
|   | 6 | no |
|   | 7 | no |
| C | 0 | Yes (Arduino pin A0) |
|   | 1 | yes, pin A1 |
|   | 2 | yes, pin A2 |
|   | 3 | yes, pin A3 |
|   | 4 | yes, pin A4, SDA |
|   | 5 | yes, pin A5, SCL |
|   | 6 | no |
|   | 7 | no |
| D | 0 | Yes (Arduino pin RX<-0) |
|   | 1 | yes, pin X->1 |
|   | 2 | yes, pin 2 |
|   | 3 | yes, pin -3 |
|   | 4 | yes, pin 4 |
|   | 5 | yes, pin -5 |
|   | 6 | yes, pin -6 |
|   | 7 | yes, pin 7 |


2. Part of the C code listing with syntax highlighting, which blinks alternately with a pair of LEDs; let one LED is connected to port B and the other to port C:

```c
/* Defines -----------------------------------------------------------*/
#define LED_GREEN   PB5     // AVR pin where green LED is connected
#define LED_RED   PC0
#define BLINK_DELAY 500
#ifndef F_CPU
# define F_CPU 16000000     // CPU frequency in Hz required for delay
#endif

/* Includes ----------------------------------------------------------*/
#include <util/delay.h>     // Functions for busy-wait delay loops
#include <avr/io.h>         // AVR device-specific IO definitions

/* Functions ---------------------------------------------------------*/
/**********************************************************************
 * Function: Main function where the program execution begins
 * Purpose:  Toggle two LEDs when a push button is pressed.
 * Returns:  none
 **********************************************************************/
int main(void)
{
    // Green LED at port B
    // Set pin as output in Data Direction Register...
    DDRB = DDRB | (1<<LED_GREEN);
    // ...and turn LED off in Data Register
    PORTB = PORTB & ~(1<<LED_GREEN);
    
    DDRC = DDRC | (1<<LED_RED);    
    PORTC = PORTC & ~(1<<LED_RED);
    

    // Configure the second LED at port C


    // Configure Push button at port D and enable internal pull-up resistor


    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        PORTB = PORTB ^ (1<<LED_GREEN);
        _delay_ms(BLINK_DELAY);
        PORTB = PORTB & ~(1<<LED_GREEN);
        PORTC = PORTC ^ (1<<LED_RED);
        _delay_ms(BLINK_DELAY);
        PORTC = PORTC & ~(1<<LED_RED);       
        // WRITE YOUR CODE HERE
        

    }

    // Will never reach this
    return 0;
}
```


### Push button

1. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Let the push button is connected to port D:

```c
#define LED_GREEN   PB5     // AVR pin where green LED is connected
#define LED_RED   PC0
#define BUTTON   PD0
#define BLINK_DELAY 500
#ifndef F_CPU
# define F_CPU 16000000     // CPU frequency in Hz required for delay
#endif

/* Includes ----------------------------------------------------------*/
#include <util/delay.h>     // Functions for busy-wait delay loops
#include <avr/io.h>         // AVR device-specific IO definitions

/* Functions ---------------------------------------------------------*/
/**********************************************************************
 * Function: Main function where the program execution begins
 * Purpose:  Toggle two LEDs when a push button is pressed.
 * Returns:  none
 **********************************************************************/
int main(void)
{
    // Green LED at port B
    // Set pin as output in Data Direction Register...
    DDRB = DDRB | (1<<LED_GREEN);
    DDRC = DDRC | (1<<LED_RED); 
	
    DDRD = DDRD | (1<<BUTTON);
    PORTD = PORTD & ~(1<<BUTTON);

    // Infinite loop
    while (1)
    {

        if (bit_is_clear(PIND, PD0))
        {
           PORTC = PORTC ^ (1<<LED_RED);
		   PORTB = PORTB ^ (1<<LED_GREEN); 
        }
        
    }

    // Will never reach this
    return 0;
}
```


### Knight Rider

1. Scheme of Knight Rider application, i.e. connection of AVR device, five LEDs, resistors, one push button, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

   ![your figure]()
