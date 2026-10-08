# STM32F446RE ADC-Controlled Hardware PWM Generation

This repository contains an embedded C application developed for the **STM32F446RET6** microcontroller using the **STM32 HAL (Hardware Abstraction Layer)** and **STM32CubeIDE**.

The application reads an analog input signal using **ADC1** (Channel 0 on `PA0`) and drives multiple hardware **PWM (Pulse-Width Modulation)** channels using **TIM3**.

---

##  Features

* **Target MCU:** STM32F446RET6 (ARM Cortex-M4)
* **IDE & Toolchain:** STM32CubeIDE / GCC
* **Drivers:** STM32F4xx HAL Driver & CMSIS
* **Analog Input:** ADC1 Regular Conversion on Channel 0 (`PA0`)
* **Timer Peripheral:** TIM3 (PWM Generation)
* **PWM Channels:**
  * **TIM3_CH1:** `PA6`
  * **TIM3_CH2:** `PA7`
  * **TIM3_CH4:** `PB1`
* **GPIO Output:** `PB0` (General Purpose Output)

---

##  Pinout Configuration

| Pin | Function | Configuration / Peripheral |
| :--- | :--- | :--- |
| **PA0** | `ADC1_IN0` | Analog Input (e.g., Potentiometer) |
| **PA6** | `TIM3_CH1` | PWM Output Channel 1 |
| **PA7** | `TIM3_CH2` | PWM Output Channel 2 |
| **PB1** | `TIM3_CH4` | PWM Output Channel 4 |
| **PB0** | `GPIO_Output` | Digital Output Pin |

---

##  Building and Running

1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/embedded_hw4.2.git
