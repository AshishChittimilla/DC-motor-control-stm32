# DC Motor Control Project — STM32 Nucleo-F446RE

## Overview

This project demonstrates a simplified embedded firmware solution to control a DC motor using **STM32 Nucleo-F446RE**.  
The motor speed is controlled dynamically via **UART serial input** by adjusting the **PWM duty cycle**.

The solution covers:
- ✅ Motor Control based on external condition (UART input)
- ✅ Speed Control at multiple discrete steps (Stop, Low, Medium, High)
- ✅ Well-commented and modular C code
- ✅ Prepared for real hardware, though this demonstration is code-only

## System Requirements / Tools Used

- **Microcontroller**: STM32 Nucleo-F446RE
- **IDE**: STM32CubeIDE
- **UART Terminal**: Tera Term / PuTTY / STM32CubeMonitor UART
- **Firmware Framework**: STM32 HAL drivers
- **Baud Rate**: 115200
- **Host OS**: Windows / macOS / Linux

## Project Structure

| File | Description |
|------|-------------|
| `main.c` | Core application logic: PWM setup, UART handling, motor control functions |
| `stm32f4xx_hal_msp.c` | Hardware abstraction layer MSP functions, pin configurations |
| `README.md` | Project description and execution guide |

## How the Code Works

1. **PWM Generation**
   - TIM3 is configured to generate PWM signal at ~20 kHz.
   - PWM output is mapped to **Pin PB4** (TIM3_CH1).

2. **UART Control**
   - USART2 is configured for serial communication at **115200 baud**.
   - The MCU listens for single-character commands from a terminal.

3. **Motor Speed Control**
   - Enter one of the following characters in your serial terminal:
     - `'0'` → Motor Stop
     - `'1'` → Low Speed (approx. 25% duty cycle)
     - `'2'` → Medium Speed (approx. 50% duty cycle)
     - `'3'` → High Speed (approx. 75% duty cycle)
   - MCU updates PWM duty cycle based on user input.

4. **Feedback**
   - The MCU responds via UART by printing the current speed level.

## How to Execute the Code

1. **Open the project in STM32CubeIDE.**
2. **Connect STM32 Nucleo-F446RE to your computer via USB.**
3. **Build and flash the code to the MCU.**
4. **Open a serial terminal (e.g., Tera Term, PuTTY, STM32CubeMonitor UART):**
   - Port: STM32 Virtual COM Port
   - Baud Rate: `115200`
   - Data bits: `8`
   - Parity: `None`
   - Stop bits: `1`
   - Flow control: `None`

5. **Test:**
   - Type `'1'`, `'2'`, `'3'`, or `'0'` in the terminal.
   - Observe UART feedback indicating the selected motor speed.

6. *(Optional for real hardware)*:
   - Connect the PWM output pin (**PB4**) to a motor driver input.
   - Power the motor driver and motor circuit.

## Expected Output

- On terminal input:
  ```bash
  Current Speed Level: 1
  Current Speed Level: 2
  Current Speed Level: 3
  Current Speed Level: 0

- PWM duty cycle adjusts dynamically based on user input.
- Motor speed (if hardware connected) changes accordingly.

## Future Improvements

✅ Add potentiometer (ADC input) for analog speed control.
✅ Add closed-loop control using a speed sensor for feedback regulation.
✅ Add status LED indication for motor states (Stop/Run).
✅ Integrate UART command parsing for advanced features (e.g., acceleration ramps).
✅ Optionally extend to BLE or Wi-Fi control (ESP32 or STM32WB).

## Notes for Reviewers

- The code is designed to run independently and does not require external hardware for demonstration.
- UART-based control simulates a real-time control interface, making the logic hardware-agnostic for testing purposes.
- If connected to real hardware, PWM signal on PB4 will control motor speed levels.

## Author

Ashish Chittimilla

## License

This project is provided as a technical demonstration for Voltair.ai assignment and is free for evaluation and educational use.

