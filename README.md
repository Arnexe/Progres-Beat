<p align="center">
  <img src="logo.png" width="350" alt="PROGRES:BEAT IDENTIFIER">
</p>

# PROGRES:BEAT // UNIT_11
### INDUSTRIAL CYBERDECK CONTROL INTERFACE // REV 3.0

![Status](https://img.shields.io/badge/STATUS-OPERATIONAL-green?style=for-the-badge)
![Hardware](https://img.shields.io/badge/HARDWARE-ARDUINO_UNO-blue?style=for-the-badge)
![Interface](https://img.shields.io/badge/INTERFACE-WEB_BLUETOOTH-red?style=for-the-badge)

> **PROGRES:BEAT** is a specialized hardware-software bridge designed for "Deep Work" environments. It serves as a physical artifact for system telemetry and audio visualization, utilizing a low-latency Web Bluetooth protocol to drive an 11-pixel LED ring array.

---

## 1. SYSTEM SPECIFICATIONS

### 1.1 Hardware Stack
| Component | Specification | ID / Type |
| :--- | :--- | :--- |
| **MCU** | ATmega328P | Arduino Uno R3 |
| **Connectivity** | Bluetooth 2.0/4.0 BLE | HC-05 / HM-10 |
| **Visual Output** | Addressable RGB LED Ring | WS2812B (11-bit) |
| **Audio Output** | Active Piezo Buzzer | 5V Logic |
| **Power Supply** | USB Bus Power | 5V DC / 500mA |

### 1.2 Wiring Diagram (PINOUT)
**CRITICAL:** Strict adherence to this pinout is required for firmware V3.0.0 compatibility.

| Component | Pin Function | Arduino Pin | Note |
| :--- | :--- | :--- | :--- |
| **BUZZER** | SIGNAL | **D2** | Active Low/High |
| **LED RING** | DATA IN | **D3** | 11 Pixels Chain |
| **BLUETOOTH** | STATE | **D4** | Connection Status |
| **BLUETOOTH** | TXD | **D9** | Connect to BT RX |
| **BLUETOOTH** | RXD | **D10** | Connect to BT TX |

---

## 2. SOFTWARE ARCHITECTURE

### 2.1 Communication Protocol
The system uses a custom serial packet structure over Bluetooth UART at 9600 baud.

* **Equalizer Mode (SYNC):**
    * Command: `V` (Velocity)
    * Payload: `0-11` (Integer representing active LEDs)
    * *Latency: < 50ms*

* **Comet Mode (LOADING):**
    * Command: `L` (Loop)
    * Payload: `NULL` (Triggers internal firmware animation)

### 2.2 Web Interface Stack
The client-side application is hosted via GitHub Pages and runs entirely in the browser.
* **Core:** HTML5 / CSS3 (Industrial UI Design)
* **Logic:** Vanilla JavaScript (ES6+)
* **APIs Used:**
    * `navigator.bluetooth` (BLE Connection Management)
    * `AudioContext` (Real-time Frequency Analysis)
    * `getDisplayMedia` (System Audio Stream Capture)

---

## 3. OPERATIONAL MODES

### [MODE A] AUDIO SYNC (Equalizer)
Real-time audio visualization using Fast Fourier Transform (FFT).
* **Function:** Captures system-wide audio via Web Audio API.
* **Logic:** Computes average energy across low and mid frequency bands.
* **Mapping:** Translates amplitude levels directly to the 0-11 LED scale.

### [MODE B] COMET (Idle/Loading)
Autonomous "heartbeat" animation for standby status.
* **Pattern:** Single pixel rotation with sub-pixel interpolation (Anti-aliased tail).
* **Aesthetic:** Minimalist "Processing" indicator.
* **Default Color:** Terminal White / Cyber Cyan.

---

## 4. VISUAL IDENTITY

### 4.1 Color Palette
The interface and hardware LEDs strictly follow this industrial color scheme:

| Color | HEX Code | Usage |
| :--- | :--- | :--- |
| **CRIMSON RED** | `#C70039` | Alerts / Peak Intensity / Bass |
| **CYBER BLUE** | `#2196F3` | Interface / Idle State / Data Streams |
| **VOID BLACK** | `#0a0a0a` | Background / PCB Aesthetic |
| **TERMINAL WHITE**| `#E0E0E0` | Typography / Primary LED Output |

---

## 5. DEPLOYMENT GUIDE

1.  **Firmware:** Flash the provided `.ino` file to the Arduino Uno.
2.  **Hardware Check:** Verify wiring against the **PINOUT** table in section 1.2.
3.  **BT Pairing:** Connect the Bluetooth module to your OS (Default code: 1234 or 0000).
4.  **Launch:** Access the web controller via GitHub Pages URL.
5.  **Initialize:** Click `[01. CONNECT DEVICE]` and select the paired unit.

---

**PROGRES:BEAT // UNIT_11**
*Designed & Engineered by ARNEXE*
