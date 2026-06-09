# Tulip-monitoring-system
. Environmental Requirements for Rose Growth
Roses (Rosa spp.) are among the most commercially significant flowers in Kenya, particularly in the Rift Valley highlands. Optimal growth requires careful monitoring of several environmental parameters.
1.1 Environmental Parameters Table
#ParameterOptimal Value / RangeNotes1Temperature15°C – 28°C (day) / 10°C – 15°C (night)Above 35°C causes heat stress; below 5°C risks frost damage2Relative Humidity60% – 70%High humidity (>80%) promotes fungal diseases such as powdery mildew3Soil TypeWell-drained loamy soil or sandy loamClay soils should be amended with organic matter to improve drainage4Soil Moisture Content50% – 70% of field capacityAvoid waterlogging; drip irrigation recommended5Soil pH6.0 – 6.5 (slightly acidic)pH outside this range inhibits nutrient uptake6Sunlight Exposure6 – 8 hours of direct sunlight per dayFull sun preferred; partial shade acceptable but reduces bloom count
1.2 Additional Notes

LPG Gas Monitoring: LPG (a mixture of methane, butane, and propane) is monitored as a safety measure in enclosed greenhouse environments where gas heating systems may be in use. Elevated LPG concentrations can be toxic to plants and hazardous to workers. Safe threshold: < 1,000 ppm.
Temperature and humidity are the most critical parameters for disease prevention in rose cultivation.


2. Hardware Components
The following components are required to build the embedded monitoring system:
2.1 Microcontrollers & Communication Modules
#ComponentQuantityPurpose1ESP32S DevKIT WiFi + BLE Module (30-pin)2Main microcontroller with wireless communication for data processing and transmission
2.2 Sensors
#ComponentQuantityPurpose2DHT22 (AM2302) Temperature & Humidity Sensor1Measures ambient temperature and relative humidity3MQ-5 LPG / Natural Gas / Coal Gas Sensor1Detects LPG, methane, propane, and butane concentrations in the air4Capacitive Soil Moisture Sensor (v1.2 or v2.0)1Measures volumetric soil moisture content5pH Sensor / Electrode Module (e.g., SEN0161)1Measures soil pH via solution6LDR (Light Dependent Resistor) / BH1750 Light Sensor1Measures ambient light intensity (lux) as proxy for sunlight hours
2.3 Actuators & Output Devices
#ComponentQuantityPurpose71.3" White IIC 128×64 OLED LCD Display (SH1106)1Displays real-time sensor readings locally85V 1-Channel Low Level Trigger Relay Module1Controls external devices (e.g., irrigation pump, fan, heater) based on sensor thresholds
2.4 Passive Components
#ComponentQuantityPurpose910 kΩ Resistor5Pull-up/pull-down resistors for sensors (DHT22, LDR)104.7 kΩ Resistor2I²C pull-up resistors for SDA/SCL lines111 kΩ Resistor2Current limiting resistors12100 nF (0.1 µF) Ceramic Capacitor4Decoupling capacitors for stable sensor power1310 µF Electrolytic Capacitor2Power supply filtering14Voltage Divider (10 kΩ + 10 kΩ)1Scale MQ-5 analog output to ESP32 ADC input range (0–3.3V)
2.5 Prototyping Tools
#ComponentQuantityPurpose15Breadboard (830-point)2Component prototyping without soldering16Jumper Wires (Male-to-Male, Male-to-Female)40+Circuit connections on breadboard17USB Micro-B Cable2Programming and power supply for ESP32 modules185V DC Power Supply / Power Bank1Power source for the complete circuit19Multimeter1Testing and debugging circuit voltages and continuity
