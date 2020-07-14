# Digital Input - IRQ

!!! note "read before"
    This complements [Digital Input - Pooling](/misc/digital-input-pooling/). General information and hardware is describe there.
    
The use of interruption makes the code react to event on the pin (High -> Low/ Low -> High/ High/ Low). The advance

- avoid losing information
- priorization of events
- entering in low power modes
- 

## Firmware 

Steps to read a simple digital data from PIO pin for the 

1. Enable system clock/ board configs.
1. Enable the peripheral
1. Configure on the peripheral:
    - Pin as input
    - As need: Pull-Up/ Pull-Down
1. Read the data

## Example for internal Pull-Up

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
    pmc_enable_periph_clk (BUT_PRO_ID);
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
