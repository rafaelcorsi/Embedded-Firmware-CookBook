# Digital Output

Digital output is the most simple way to **control** the external world. This signal can assume only two states: On/OFF, `1`/`0`, `High`/ `Low`.

!!! info "most common uses"
    - LED
    - DC Motor
    - Buzzer
    - ...

The peripheral that allows us to read a digital value is common named:

- :arrow_right: Parallel I/O - PIO
- General-Purpose I/O - GPIO

!!! note "Peripheral"
    Read more about this peripheral on [Peripheral-PIO]().


## Hardware

> This examples shows how to control a LED, but can be apply to others digital components.

This example shows on how to control a LED with a microcontroller, the series resistor limits the electric current.

=== "Drive in"
    ![](/misc/figs/digital-output/digital-output-vcc.png){width=350}

    :star: Best solution (reduces the risk of burning as normally input accept electric current is higher than output current)
    
    - Connect LED to resistor to VCC
    
    Write `0` to pin light up LED, `1` turn off.
    
=== "Drive out"
    ![](/misc/figs/digital-output/digital-output-gnd.png){width=350}

!!! warning 
    - You must respect the VCC of your system.
    - You must check the resistor value to your system.

## Firmware 

Steps to simple control a PIO pin:

1. Enable system clock/ board configs.
1. Enable the peripheral
1. Configure the Pin as output
1. Control pin (High/ Low)

### Example 

``` c
#define LED_PIO      PIOC
#define LED_PIO_ID   ID_PIOC
#define LED_IDX      8
#define LED_IDX_MASK (1 << LED_IDX)
#define LED_CONFIG PIO_DEFAULT

int main (void){
	sysclk_init();

    pmc_enable_periph_clk(LED_PIO_ID);
    
	while (1){
        // drive pin low - turns on led
        pio_clear(LED_PIO, LED_IDX_MASK);  
        delay_ms(100);  
        
        // drive pin high - turns off led 
        pio_set(LED_PIO, LED_IDX_MASK);  
        delay_ms(100);                      
    }

```
