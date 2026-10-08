# STM32F446RE ADC-Triggered RGB Status Indicator & Buzzer Alarm

This repository contains an embedded C application developed for the **STM32F446RET6** microcontroller using the **STM32 HAL (Hardware Abstraction Layer)** and **STM32CubeIDE**.

The firmware continuously samples an analog input voltage (from a sensor or potentiometer) on **ADC1 (Channel 0)**. Depending on predefined threshold ranges, it adjusts the duty cycle of three hardware **PWM channels on TIM3** to change an **RGB LED's** color (Green, Blue, Red) and toggles a **Buzzer** output on `PB0` during hazard states.

---

## Features

- **Target MCU:** STM32F446RET6 (ARM Cortex-M4 @ 16 MHz HSI)
- **IDE & Toolchain:** STM32CubeIDE / GCC
- **Framework:** STM32F4xx HAL Driver & CMSIS
- **Analog Acquisition:** ADC1 Regular Conversion on `PA0` (12-bit resolution)
- **Actuators & Indicators:**
  - **RGB LED via Hardware PWM:** Driven by `TIM3` (Prescaler: 15, Period: 999)
    - **Red:** `TIM3_CH4` (`PB1`)
    - **Green:** `TIM3_CH1` (`PA6`)
    - **Blue:** `TIM3_CH2` (`PA7`)
  - **Acoustic Warning:** Active Buzzer connected to `PB0`

---

## Operating Logic

The analog channel (`PA0`) is sampled inside the main loop every 200 ms:

| ADC Range (12-bit) | LED Color | Active PWM Channels (Duty Cycle) | Buzzer State (`PB0`) | System Status |
| :--- | :--- | :--- | :--- | :--- |
| **< 72** | **Green** | CH1 = 500 (50%), CH2 = 0, CH4 = 0 | `LOW` (Off) | Normal / Safe |
| **72 – 88** | **Blue** | CH2 = 500 (50%), CH1 = 0, CH4 = 0 | `LOW` (Off) | Warning / Intermediate |
| **>= 89** | **Red** | CH4 = 500 (50%), CH1 = 0, CH2 = 0 | `HIGH` (On) | Danger / Alarm |

---

## Pinout Configuration

| Peripheral / Signal | Pin | Mode / Configuration | Description |
| :--- | :--- | :--- | :--- |
| **ADC1_IN0** | `PA0` | Analog Input | Analog input source (Sensor / Potentiometer) |
| **RGB - Green** | `PA6` | Alternate Function Push-Pull (`TIM3_CH1`) | PWM channel for Green LED element |
| **RGB - Blue** | `PA7` | Alternate Function Push-Pull (`TIM3_CH2`) | PWM channel for Blue LED element |
| **RGB - Red** | `PB1` | Alternate Function Push-Pull (`TIM3_CH4`) | PWM channel for Red LED element |
| **Buzzer** | `PB0` | Digital Output Push-Pull | Active buzzer drive pin |

---

## Building and Flashing

1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/embedded_hw4.2.git
