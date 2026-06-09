## Semester Project — Deliverable 1
**Group Name:** Wantam
**Group Members:**
* 152066 - Owiro Shawn Ochieng
* 168323 - Wambari Michael Rimu
* 167074 - Jaafar Latifah Jepchirchir
* 166152 - Precious Mwende Waweru
* 157769 - Kariuki Darrel Kanyugo
---

## Table of Contents

1. [Environmental Requirements for Tulip Growth](#1-environmental-requirements-for-tulip-growth)
2. [Hardware Components](#2-hardware-components)
3. [Component Datasheets](#3-component-datasheets)
5. [References](#5-references)
---

## 1. Environmental Requirements for Tulip Growth
 
### 1.1 Overview
 
Tulips  are cool-season spring-blooming bulbous perennials belonging to the family *Liliaceae*. Native to Central Asia and cultivated worldwide since the 16th century, tulips are prized for their vivid cup-shaped blooms and seasonal beauty. They are highly sensitive to temperature and require a well-defined cold vernalisation period — typically 12 to 14 weeks at 2 °C – 9 °C — for successful bulb development and bloom initiation.
 
In controlled greenhouse environments, which are increasingly standard in commercial tulip production, continuous environmental monitoring is critical. Deviations in temperature, humidity, soil moisture, or gas composition can rapidly lead to crop loss through fungal disease, heat stress, root rot, or oxygen displacement at the root zone. The embedded monitoring system described in this deliverable is designed to track and respond to the six key parameters documented below.
 
---
 
### 1.2 Environmental Parameters Reference Table
 
| # | Parameter | Optimal Value / Range | Unit | Notes |
|---|-----------|----------------------|------|-------|
| 1 | **Temperature** | 10 – 15 °C (night) / 20 – 26 °C (day) | °C | Vernalisation (bulb cold period): 2 – 9 °C for 12–14 weeks. Above 30 °C causes bloom damage and drooping. Below −1 °C risks bulb frost damage |
| 2 | **Relative Humidity** | 50 % – 70 % | % RH | Humidity above 80 % promotes *Botrytis tulipae* (fire disease) and other fungal pathogens. Indoor/greenhouse target: 50 – 60 % for maximum flower lifespan [8][9] |
| 3 | **Soil Type** | Light sandy loam, well-drained | — | Raised beds recommended. Sandy loam amended with organic matter is ideal. Heavy clay soils must be supplemented with decomposed compost or peat moss. Tulips are highly susceptible to root rot in waterlogged conditions [10][11] |
| 4 | **Soil Moisture Content** | 40 % – 60 % of field capacity | % | Maintain consistent moisture without saturation. Drip irrigation preferred. Bulbs rot rapidly in soggy soils [8] |
| 5 | **Soil pH** | 6.0 – 7.0 (slightly acidic to neutral) | pH | Optimal is 6.0 – 6.5. pH extremes outside this range inhibit bulb root growth and block nutrient uptake. Acidic or alkaline soils should be amended before planting [9][10] |
| 6 | **Sunlight Exposure** | 6 – 8 hours of direct sunlight | h/day | Full sun preferred in temperate climates. Partial or dappled shade advisable in warmer environments to prevent heat stress. No artificial supplemental light is required for established bulbs [8][11] |
| 7 | **LPG Concentration (Safety)** | < 1,000 ppm (alarm threshold) | ppm | Gas-fired heating systems used in greenhouses to maintain cold vernalisation temperatures may leak LPG (methane, butane, propane). Concentrations above 1,000 ppm are hazardous to personnel and displace oxygen critical to root respiration [1] |
 
> **Note on LPG Monitoring:** In enclosed greenhouse environments where gas-fired heaters maintain the cool temperatures necessary for tulip vernalisation, monitoring for LPG leakage is a mandatory safety measure. Undetected leaks present fire and explosion hazards, and elevated gas concentrations can create anaerobic soil conditions that are fatal to tulip bulbs. The MQ-5 sensor in this design provides both analog concentration readings and a configurable digital threshold alarm output.
 
---
 
## 2. Hardware Components
 
The following bill of materials (BOM) lists all hardware required to build the embedded environmental monitoring device. Components are grouped by functional category.
 
### 2.1 Microcontrollers
 
| # | Component | Qty | Function |
|---|-----------|-----|----------|
| 1 | ESP32S DevKIT WiFi + BLE Module (30-pin) | 2 | Central processing unit for all designs. Handles sensor data acquisition, threshold evaluation, display output, and wireless data transmission via Wi-Fi (802.11 b/g/n) or Bluetooth 4.2 BLE |
 
### 2.2 Sensors
 
| # | Component | Qty | Function |
|---|-----------|-----|----------|
| 2 | DHT22 AM2302 Temperature & Humidity Sensor | 1 | Measures ambient air temperature (−40 °C to +80 °C, ±0.5 °C) and relative humidity (0–100 % RH, ±2 %) via single-wire digital protocol. Sampling interval: minimum 2 seconds |
| 3 | MQ-5 LPG / Natural Gas / Coal Gas Sensor | 1 | Electrochemical sensor detecting LPG, methane (CH₄), propane (C₃H₈), and butane (C₄H₁₀) in the range 200–10,000 ppm. Outputs analog voltage (AO) and digital threshold (DO) |
| 4 | Capacitive Soil Moisture Sensor v2.0 | 1 | Measures volumetric soil water content using capacitance principles. Corrosion-resistant compared to resistive-type sensors |
| 5 | Analog pH Sensor / Electrode Module (DFRobot SEN0161) | 1 | Measures soil pH via buffer solution probe (range: pH 0–14, accuracy ±0.1 pH) |
| 6 | BH1750 Digital Ambient Light Intensity Sensor | 1 | Measures illuminance in lux over I²C; used to log cumulative daily sunlight exposure hours |
 
### 2.3 Output Devices & Actuators
 
| # | Component | Qty | Function |
|---|-----------|-----|----------|
| 7 | 1.3" White IIC 128×64 OLED LCD Display (SH1106) | 1 | Displays real-time sensor readings locally. I²C interface; operates at 3.3 V |
| 8 | 5V 1-Channel Low Level Trigger Relay Module | 1 | Switches external loads (irrigation pump, exhaust fan, or heater) based on threshold events. Controlled by ESP32 GPIO |
 
### 2.4 Passive Electronic Components
 
| # | Component | Qty | Function |
|---|-----------|-----|----------|
| 9 | 10 kΩ Resistor (¼ W, ±5 %) | 5 | Pull-up for DHT22 DATA line (×1); voltage divider for MQ-5 AO line (×2); signal conditioning (×2) |
| 10 | 4.7 kΩ Resistor (¼ W, ±5 %) | 2 | I²C bus pull-up resistors on SDA and SCL lines (OLED + BH1750) |
| 11 | 1 kΩ Resistor (¼ W, ±5 %) | 2 | Current-limiting for status LED indicators |
| 12 | 100 nF (0.1 µF) Ceramic Capacitor | 4 | High-frequency decoupling capacitors placed close to sensor VCC pins to suppress power rail noise |
| 13 | 10 µF Electrolytic Capacitor (16 V rated) | 2 | Bulk power supply filtering at 5 V and 3.3 V rails |
 
### 2.5 Prototyping Tools
 
| # | Component | Qty | Function |
|---|-----------|-----|----------|
| 14 | Full-size Breadboard (830-point) | 2 | Solderless prototyping platform for circuit assembly |
| 15 | Jumper Wires — Male-to-Male | 20 | Breadboard-to-breadboard internal connections |
| 16 | Jumper Wires — Male-to-Female | 20 | Breadboard-to-sensor module connections |
| 17 | USB Micro-B Cable | 2 | ESP32 programming and 5 V power delivery |
| 18 | 5 V DC Power Supply (minimum 2 A) | 1 | Primary power source for the complete assembled circuit |
| 19 | Digital Multimeter | 1 | Voltage, resistance, and continuity verification during assembly and debugging |
 
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

## 5. References

[1] A. A. Umar, "Automatic Gas Leakage Monitoring System Using MQ-5 Sensor," *Review of Computer Engineering Research*, vol. 8, no. 2, pp. 64–75, 2021. https://doi.org/10.18488/JOURNAL.76.2021.82.64.75
[2] Espressif Systems, *ESP32 Series Datasheet*, v4.6. Espressif Systems, 2024. [Online]. Available: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
[3] Espressif Systems, *ESP32 Technical Reference Manual*, v5.3. Espressif Systems, 2024. [Online]. Available: https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf
[4] Aosong Electronics Co., Ltd., *DHT22 AM2302 Digital-output Relative Humidity and Temperature Sensor — Product Manual*. Aosong, 2021. [Online]. Available: https://cdn-shop.adafruit.com/datasheets/DHT22.pdf
[5] Zhengzhou Winsen Electronics Technology Co., Ltd., *MQ-5 Semiconductor Sensor for Combustible Gas — Product Manual v1.4*. Winsen, 2014. [Online]. Available: https://www.winsen-sensor.com/d/files/PDF/Semiconductor%20Gas%20Sensor/MQ-5%20(Ver1.4)%20-%20Manual.pdf
[6] Sino Wealth Semiconductor Ltd., *SH1106 128×64 OLED Driver with Controller — Datasheet*. Sino Wealth, 2011. [Online]. Available: https://www.velleman.eu/downloads/29/infosheets/sh1106_datasheet.pdf
[7] Components101, "5V Single Channel Relay Module — Pinout, Features & Datasheet," 2023. [Online]. Available: https://components101.com/switches/5v-single-channel-relay-module-pinout-features-applications-working-datasheet
[8] Neroli Blume, "How to Take Care of Tulips: A Comprehensive Guide," *Neroli Blume Blog*, Feb. 2025. [Online]. Available: https://neroliblume.com/blogs/flower-facts/how-to-take-care-of-tulips
[9] DryGair, "What are the Ideal Conditions for Greenhouse Tulips?" *DryGair Blog*, Apr. 2023. [Online]. Available: https://drygair.com/blog/greenhouse-tulips/ 
[10] Kellogg Garden Organics, "Gardener's Guide to Planting Tulips," Dec. 2022. [Online]. Available: https://kellogggarden.com/blog/gardening/gardeners-guide-to-planting-tulips/
[11] White Flower Farm, "Planting & Growing Tulips," 2026. [Online]. Available: https://www.whiteflowerfarm.com/how-to-grow-tulips
[12] Espressif Systems, "ESP-NOW — ESP-IDF Programming Guide," 2024. [Online]. Available: https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/network/esp_now.html
---
