# Digital Output

Digital output is the most simple way to **control** the external world. This signal can assume only two states: On/OFF, `1`/`0`, `High`/ `Low`.

!!! info "most common uses"
    - LED
    - DC Motor
    - Buzzer
    - ...

Normally this peripherals controls more than one pin and each microcontroller has several instances of the same peripheral, to control more pins. Each pin can be configured independent. 

!!! note "Microchip SAM"
    Microchip SAM microcontrollers called this as PIO, each instance of the 
    PIO is called PIO **A**, PIO **B**, PIO **C**, ... each PIO can controll up
    to 32 independents pins.

## Hardware

> This examples shows how to control a LED, but can be apply to others digital componentes.



## Firmware 

Steps to simple control a PIO pin:

1. Enable system clock/ board configs.
1. Enable the peripheral
1. Configure the Pin as output
1. Write to pin

### Example 

``` c

```
