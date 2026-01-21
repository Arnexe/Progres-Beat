<p align="center">
  <img src="logo.png" width="400" alt="PROGRES:BEAT // UNIT_11">
</p>

# PROGRES:BEAT // UNIT_11
### INDUSTRIAL CYBERDECK CONTROL INTERFACE // REV 3.0

![Status](https://img.shields.io/badge/STATUS-OPERATIONAL-green?style=for-the-badge)
![Hardware](https://img.shields.io/badge/HARDWARE-ARDUINO_UNO-blue?style=for-the-badge)
![Interface](https://img.shields.io/badge/INTERFACE-WEB_BLUETOOTH-red?style=for-the-badge)

> **PROGRES:BEAT** is a specialized hardware-software artifact designed for "Deep Work" environments. It functions as a standalone industrial-grade visualizer and processing indicator, driven by a low-latency Web Bluetooth protocol to an 11-pixel LED ring array.

---

## 1. TECHNICAL SPECIFICATIONS

### 1.1 Hardware Architecture
| Component | Specification | Description |
| :--- | :--- | :--- |
| **Microcontroller** | ATmega328P | Arduino Uno R3 Core |
| **Connectivity** | Bluetooth 2.0/4.0 | HC-05 / HM-10 Module |
| **Visual Output** | WS2812B RGB Ring | 11 Addressable Pixels |
| **Audio Feedback**| Active Buzzer | 5V TTL Logic |
| **Power Logic** | USB 5V | 500mA Bus Powered |

### 1.2 Wiring Interface (PINOUT)
**Strict adherence to this configuration is mandatory for Firmware V3 compatibility:**

| Peripheral | Signal | Arduino Pin |
| :--- | :--- | :--- |
| **BUZZER** | I/O SIGNAL | **D2** |
| **LED RING** | DATA LINE | **D3** |
| **BT MODULE** | STATE | **D4** |
| **BT MODULE** | TXD (Transmit) | **D9** |
| **BT MODULE** | RXD (Receive) | **D10** |

---

## 2. OPERATIONAL LOGIC

The system operates on a dual-mode communication protocol via Bluetooth UART at 9600 baud.

* **SYNC MODE (Command: 'V'):** Real-time frequency-to-pixel mapping. Accepts integer values (0-11) to represent signal amplitude.
* **LOADING MODE (Command: 'L'):** Triggers an autonomous "Comet" animation stored in the MCU firmware.

---

## 3. DESIGN SYSTEM & IDENTITY

### 3.1 Industrial Color Palette
The artifact utilizes a specific color-coding system for data representation:
* **CRIMSON RED (`#C70039`):** High-intensity signals, peaks, and system alerts.
* **CYBER BLUE (`#2196F3`):** Connectivity status, idle data flow, and UI elements.
* **TERMINAL WHITE (`#E0E0E0`):** Default state, secondary visualization, and typography.

---

## 4. FIRMWARE SOURCE CODE (V3.0)

[Image of Arduino Uno with WS2812B LED ring and Bluetooth module wiring diagram]

```cpp
/*
 * PROGRES:BEAT // UNIT_11 FIRMWARE
 * REV: 3.0.0 // 2026-01-21
 */

#include <Adafruit_NeoPixel.h>
#include <SoftwareSerial.h>

#define LED_PIN    3
#define BUZZER_PIN 2
#define BT_RX      10
#define BT_TX      9
#define NUMPIXELS  11

Adafruit_NeoPixel pixels(NUMPIXELS, LED_PIN, NEO_GRB + NEO_KHZ800);
SoftwareSerial BTSerial(BT_RX, BT_TX
