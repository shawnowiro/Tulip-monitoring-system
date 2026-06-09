# ICS 4111: Embedded Systems & IoT
## Semester Project — Deliverable 1
**Flower Assigned:** Rose (*Rosa* spp.)
**Course:** ICS 4111 — Embedded Systems & IoT
**Semester:** April–July 2026

---

## Table of Contents

1. [Environmental Requirements for Rose Growth](#1-environmental-requirements-for-rose-growth)
2. [Hardware Components](#2-hardware-components)
3. [Component Datasheets](#3-component-datasheets)
4. [Schematic Diagrams](#4-schematic-diagrams)
5. [References](#5-references)

---

## 1. Environmental Requirements for Rose Growth

Roses (*Rosa* spp.) are among the most commercially significant flowers in Kenya, particularly in the Rift Valley highlands. Optimal growth requires careful monitoring of several environmental parameters.

### 1.1 Environmental Parameters Table

| # | Parameter | Optimal Value / Range | Notes |
|---|-----------|----------------------|-------|
| 1 | **Temperature** | 15°C – 28°C (day) / 10°C – 15°C (night) | Above 35°C causes heat stress; below 5°C risks frost damage |
| 2 | **Relative Humidity** | 60% – 70% | High humidity (>80%) promotes fungal diseases such as powdery mildew |
| 3 | **Soil Type** | Well-drained loamy soil or sandy loam | Clay soils should be amended with organic matter to improve drainage |
| 4 | **Soil Moisture Content** | 50% – 70% of field capacity | Avoid waterlogging; drip irrigation recommended |
| 5 | **Soil pH** | 6.0 – 6.5 (slightly acidic) | pH outside this range inhibits nutrient uptake |
| 6 | **Sunlight Exposure** | 6 – 8 hours of direct sunlight per day | Full sun preferred; partial shade acceptable but reduces bloom count |

### 1.2 Additional Notes

- **LPG Gas Monitoring:** LPG (a mixture of methane, butane, and propane) is monitored as a safety measure in enclosed greenhouse environments where gas heating systems may be in use. Elevated LPG concentrations can be toxic to plants and hazardous to workers. Safe threshold: **< 1,000 ppm**.
- Temperature and humidity are the most critical parameters for disease prevention in rose cultivation.

---

## 2. Hardware Components

The following components are required to build the embedded monitoring system:

### 2.1 Microcontrollers & Communication Modules

| # | Component | Quantity | Purpose |
|---|-----------|----------|---------|
| 1 | ESP32S DevKIT WiFi + BLE Module (30-pin) | 2 | Main microcontroller with wireless communication for data processing and transmission |

### 2.2 Sensors

| # | Component | Quantity | Purpose |
|---|-----------|----------|---------|
| 2 | DHT22 (AM2302) Temperature & Humidity Sensor | 1 | Measures ambient temperature and relative humidity |
| 3 | MQ-5 LPG / Natural Gas / Coal Gas Sensor | 1 | Detects LPG, methane, propane, and butane concentrations in the air |
| 4 | Capacitive Soil Moisture Sensor (v1.2 or v2.0) | 1 | Measures volumetric soil moisture content |
| 5 | pH Sensor / Electrode Module (e.g., SEN0161) | 1 | Measures soil pH via solution |
| 6 | LDR (Light Dependent Resistor) / BH1750 Light Sensor | 1 | Measures ambient light intensity (lux) as proxy for sunlight hours |

### 2.3 Actuators & Output Devices

| # | Component | Quantity | Purpose |
|---|-----------|----------|---------|
| 7 | 1.3" White IIC 128×64 OLED LCD Display (SH1106) | 1 | Displays real-time sensor readings locally |
| 8 | 5V 1-Channel Low Level Trigger Relay Module | 1 | Controls external devices (e.g., irrigation pump, fan, heater) based on sensor thresholds |

### 2.4 Passive Components

| # | Component | Quantity | Purpose |
|---|-----------|----------|---------|
| 9 | 10 kΩ Resistor | 5 | Pull-up/pull-down resistors for sensors (DHT22, LDR) |
| 10 | 4.7 kΩ Resistor | 2 | I²C pull-up resistors for SDA/SCL lines |
| 11 | 1 kΩ Resistor | 2 | Current limiting resistors |
| 12 | 100 nF (0.1 µF) Ceramic Capacitor | 4 | Decoupling capacitors for stable sensor power |
| 13 | 10 µF Electrolytic Capacitor | 2 | Power supply filtering |
| 14 | Voltage Divider (10 kΩ + 10 kΩ) | 1 | Scale MQ-5 analog output to ESP32 ADC input range (0–3.3V) |

### 2.5 Prototyping Tools

| # | Component | Quantity | Purpose |
|---|-----------|----------|---------|
| 15 | Breadboard (830-point) | 2 | Component prototyping without soldering |
| 16 | Jumper Wires (Male-to-Male, Male-to-Female) | 40+ | Circuit connections on breadboard |
| 17 | USB Micro-B Cable | 2 | Programming and power supply for ESP32 modules |
| 18 | 5V DC Power Supply / Power Bank | 1 | Power source for the complete circuit |
| 19 | Multimeter | 1 | Testing and debugging circuit voltages and continuity |

---

## 3. Component Datasheets

### 3.1 1.3" White IIC 128×64 OLED LCD (SH1106 Driver)

- **Datasheet / Product Page:** [SH1106 OLED Datasheet — Sino Wealth](https://www.velleman.eu/downloads/29/infosheets/sh1106_datasheet.pdf)
- **Key Specs:**
  - Resolution: 128 × 64 pixels
  - Interface: I²C (address 0x3C or 0x3D)
  - Operating Voltage: 3.3V – 5V
  - Display Color: White on Black
  - Driver IC: SH1106

### 3.2 ESP32S DevKIT WiFi + BLE Module (30-Pin)

- **Datasheet / Product Page:** [ESP32 Series Datasheet — Espressif Systems](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf)
- **Technical Reference Manual:** [ESP32 Technical Reference Manual](https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf)
- **Key Specs:**
  - CPU: Xtensa dual-core LX6 @ up to 240 MHz
  - RAM: 520 KB SRAM
  - Wi-Fi: 802.11 b/g/n
  - Bluetooth: v4.2 BR/EDR + BLE
  - GPIO Pins: 30 (on this variant)
  - ADC: 12-bit, 18 channels
  - Operating Voltage: 3.3V (logic) / 5V via USB

### 3.3 DHT22 AM2302 Temperature and Humidity Sensor

- **Datasheet:** [DHT22 AM2302 Datasheet — Aosong Electronics](https://cdn-shop.adafruit.com/datasheets/DHT22.pdf)
- **Key Specs:**
  - Temperature Range: -40°C to +80°C (±0.5°C accuracy)
  - Humidity Range: 0% – 100% RH (±2% accuracy)
  - Interface: Single-wire digital (1-Wire like)
  - Operating Voltage: 3.3V – 5V
  - Sampling Rate: Once every 2 seconds

### 3.4 MQ-5 LPG / Natural Gas / Coal Gas Sensor

- **Datasheet:** [MQ-5 Datasheet — Zhengzhou Winsen Electronics](https://www.winsen-sensor.com/d/files/PDF/Semiconductor%20Gas%20Sensor/MQ-5%20(Ver1.4)%20-%20Manual.pdf)
- **Product Page:** [MQ-5 at Winsen Sensor](https://www.winsen-sensor.com/sensors/combustible-gas-sensor/mq-5.html)
- **Key Specs:**
  - Target Gases: LPG, natural gas (methane), coal gas, butane, propane
  - Detection Range: 200 – 10,000 ppm
  - Heater Voltage: 5V AC/DC
  - Output: Analog voltage (AO) and digital threshold (DO)
  - Preheat Time: ≥ 48 hours (first use); 20 minutes (subsequent use)
  - Operating Voltage: 5V

### 3.5 5V 1-Channel Low Level Trigger Relay Module

- **Product Page / Description:** [5V 1-Channel Relay Module — Components101](https://components101.com/switches/5v-single-channel-relay-module-pinout-features-applications-working-datasheet)
- **Key Specs:**
  - Trigger Type: Low Level (active LOW signal triggers the relay)
  - Control Signal Voltage: 3.3V – 5V (compatible with ESP32)
  - Load Capacity: Up to 10A @ 250V AC / 10A @ 30V DC
  - Relay Type: SPDT (Single Pole Double Throw)
  - Pins: VCC, GND, IN (signal), COM, NO (Normally Open), NC (Normally Closed)

##  References

1. **Rose Cultivation Guide** — Kenya Flower Council: https://kenyaflowercouncil.org
2. **SH1106 OLED Datasheet** — Sino Wealth Semiconductor: https://www.velleman.eu/downloads/29/infosheets/sh1106_datasheet.pdf
3. **ESP32 Series Datasheet** — Espressif Systems: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
4. **DHT22 AM2302 Datasheet** — Aosong Electronics (via Adafruit): https://cdn-shop.adafruit.com/datasheets/DHT22.pdf
5. **MQ-5 Gas Sensor Datasheet** — Winsen Electronics: https://www.winsen-sensor.com/d/files/PDF/Semiconductor%20Gas%20Sensor/MQ-5%20(Ver1.4)%20-%20Manual.pdf
6. **5V Relay Module — Components101**: https://components101.com/switches/5v-single-channel-relay-module-pinout-features-applications-working-datasheet
7. **ESP-NOW Protocol Guide** — Espressif: https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/network/esp_now.html
8. Shafer, M., & Luo, L. (2020). *IoT-Based Environmental Monitoring Systems for Smart Greenhouses*. IEEE Access. (Reference for circuit diagram standards at figure 7 level of detail)

---

*Document prepared for ICS 4111 — Embedded Systems & IoT, April–July 2026 Semester.*
*Submitted via GitHub repository as required.*
