# grbl
An open source, embedded, high performance g-code-parser and CNC milling controller written in optimized C that will run on a straight Arduino

This version is a rather hacky but "working" attempt at adding a 4th axis C, some serious pin re-arrangement requried to acheive this and not undergone serious testing so use at your own risk.
Based on 0.9j and with changes suggested by ashelly (https://github.com/grbl/grbl/pull/703) with a series of things disabled. 

Using a nano for testing as it is easier, will probably move onto bare ATMEGA328 when dev is done.

Build results in - 30616byte hex and 1495bytes of ram usage.

```
                        +-----+
           +------------| USB |------------+
           |            +-----+            |
           | [ ]D13  PB5       PB4  D12[ ] |   Spindle Enable  
           | [ ]3.3V           PB3  D11[ ]~|   Spindle PWM active low (sinking current)
           | [ ]V.ref     ___  PB2  D10[ ]~|   Z Limit  
RESET      | [ ]A0  PC0  / N \ PB1   D9[ ]~|   Y Limit  
X Direction| [ ]A1  PC1 /  A  \PB0   D8[ ] |   X Limit
Y Direction| [ ]A2  PC2 \  N  /PD7   D7[ ] |   
Z Direction| [ ]A3  PC3  \_0_/ PD6   D6[ ]~|   
C Direction| [ ]A4  PC4        PD5   D5[ ]~|   C Step
Probe      | [ ]A5  PC5        PD4   D4[ ] |   Z Step
           | [ ]A6  ADC6    PD3/INT1/D3[ ]~|   Y Step
           | [ ]A7  ADC7    PD2/INT0/D2[ ] |   X Step
           | [ ]5V                  GND[ ] |     
           | [ ]RST PC6        PC6  RST[ ] |  
           | [ ]GND   5V MOSI GND   TX1[ ] |  PD0
           | [ ]Vin   [ ] [ ] [ ]   RX1[ ] |  PD1
           |          [ ] [ ] [ ]          |
           |          MISO SCK RST         |
           | NANO-V3                       |
           +-------------------------------+
```        
TODO: </br>
  1.Double check functionality of reset and ensure system is disabled properly maybe move to port D/B?</br>
  2.Check PWM output of spindle enable</br>
  3.Check limits.c for issues with N_AXIS == 4</br>
  4.Look at stepper output on scope vs stock version while moving in 3/4 axis</br>
  5.Check to see if ashelly's change to stepper.c ( st.counter_z changed to st.counter[Z_AXIS] ) has any noticible negative effects as part of step 3</br>
  6.List things that have been disabled in the readme/re-enable things where possible</br>