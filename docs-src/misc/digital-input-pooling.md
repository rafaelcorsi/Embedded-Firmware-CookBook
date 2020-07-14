# Digital Input - Pooling

Digital input output (I/O) is the most simple way to **read** from external world. This signal can assume only two states: On/OFF, `1`/`0`, `High`/ `Low`.

!!! tip "most common uses"
    - Buttons (push/ slider/ dip switch)
    - Signal pulse (encoder)
    - ...
    
The peripheral that allows us to read a digital value is common named:

- :arrow_right: Parallel I/O - PIO
- General-Purpose I/O - GPIO

Normally this peripherals controls more than one pin and each microcontroller has several instances of the same peripheral, to control more pins. Each pin can be configured independent. 

!!! note "Microchip SAM"
    Microchip SAM microcontrollers called this as PIO, each instance of the 
    PIO is called PIO **A**, PIO **B**, PIO **C**, ... each PIO can controll up
    to 32 independents pins.

## Hardware

> This examples shows how to read a button, but can be apply to others digital componentes.

There is two way to use a button: with Pull-Up or Pull-Down. Most peripherals allow to enable a internal Pull-UP/Pull-Down resistor, with no need to connet resistores to the uC.

=== "Internal Pull-Up"

    ![](/misc/figs/digital-input/internal-pullup.svg.png){width=350}
    
    :star: Best solution (reduces the risk of burning, uses fewer components)
    
    Setup:
    
    - Connect button to pin and to gnd
    - Need to configure **Pull-Up** on the peripheral.
    - **No need to external resistor**
    
    Read `1` when not pressed and `0` when pressed.
    
=== "External Pull-Up"

    ![](/misc/figs/digital-input/external-pullup.svg.png){width=350}
    
    Setup:
    
    - Connect button to pin and to gnd
    - Add a parallel resistor to VCC 
        - must respect max pin voltage
    
    Read `1` when not pressed and `0` when pressed.

## Firmware 

Steps to read a simple digital data:

1. Enable system clock/ board configs.
1. Enable the peripheral
1. Configure on the peripheral:
    - Pin as input
    - As need: Pull-Up/ Pull-Down
1. Read the data

### Code

Firmware example for SAME70, with internal Pull-Up

``` c
#define BUT_PIO      PIOA
#define BUT_PIO_ID   ID_PIOA
#define BUT_IDX      11
#define BUT_IDX_MASK (1 << BUT_IDX)
#define BUT_SETTINGS PIO_PULLUP

int main (void){
    // init system 
    sysclk_init();

    // enable and configure peripheral
    pmc_enable_periph_clk (BUT_PIO_ID);
    pio_configure (BUT_PIO, PIO_INPUT, BUT_IDX_MASK, BUT_SETTINGS);

    while (1){
        if (pio_get (BUT_PIO, PIO_INPUT, BUT_IDX_MASK)){
            // button not pressed
        } else {
            // button pressed
        }
    }
}
```
