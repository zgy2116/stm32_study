# GPIO LED Blinking

## Purpose

Configure a GPIO output with STM32CubeMX and blink the onboard LED on an STM32F103C8T6 development board.

## Hardware

- MCU: STM32F103C8T6
- Debug/programmer: ST-Link via SWD
- LED: PC13, active low (low turns the LED on)
- Button: PA0, configured as a pull-up GPIO input but not yet used by the application

## CubeMX Configuration

- Toolchain: CMake
- Debug interface: Serial Wire on PA13/PA14
- System clock: 8 MHz HSE with PLL x9, SYSCLK = 72 MHz
- PC13: push-pull GPIO output, initial state high
- PA0: pull-up GPIO input

## Program Behavior

`main.c` toggles PC13 every 500 ms with `HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_13)`. Since the LED is active low, it blinks once per second.

## Build and Flash

Build the Debug preset from the project directory:

```bash
cmake --preset Debug
cmake --build --preset Debug
```

Flash the resulting ELF file with the VSCode debug configuration or STM32CubeProgrammer through ST-Link.

## Result

The board LED flashes successfully after programming.
