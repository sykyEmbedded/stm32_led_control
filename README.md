# STM32 LED Control

Goal: send uart commands to the target via python/minicom, which changes the LED flashing rate. Use of the push button to enable/disable the LED. 

This repository demostrates the set up of 3 different freeRTOS tasks & UART parsing which can be tested off-target. 

## Board
Nucleo-G474RE. Reference manual for pinouts etc is [UM2505](https://www.st.com/resource/en/user_manual/um2505-stm32g4-nucleo64-boards-mb1367-stmicroelectronics.pdf)

## Requirements

### Thread 1: UART
- Ring buffer for listening for commands, and parsing them, and editing a shared variable - i.e the frequency of the LED
- Ring buffer + parsing should be able to be unit tested
- Frequency in Hz, finished via `\r\n` - need to handle unknown inputs and return that its unknown

### Thread 2: LED
- Pulses the LED at the specified frequency
  
### Thread 3: Push Button
- Push button, needs to handle debouncing
- Press change state
- START STATE: **ON**