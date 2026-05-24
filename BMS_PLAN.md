# 12V BMS Development Guide (Step 1 to Advanced)

# Introduction

This project is for building a 12V Battery Management System (BMS) for lithium batteries.

Battery Type:

* 3S Li-ion Battery Pack
* 11.1V nominal
* 12.6V full charge

Goal:

* Start from very basic protection BMS
* Improve step-by-step into smart industrial BMS

---

# STEP 1 — BASIC PROTECTION BMS

## Mandatory Functions

1. Overcharge protection
2. Overdischarge protection
3. Overcurrent protection
4. Short-circuit protection
5. MOSFET cutoff switching
6. Battery connection terminals

---

# 1. OVERCHARGE PROTECTION

## Purpose

Stop charging when cell voltage becomes too high.

---

## Different Ways To Implement

| Method                  | Complexity  | Notes            |
| ----------------------- | ----------- | ---------------- |
| Dedicated BMS IC        | Easy        | Most common      |
| Zener diode cutoff      | Very simple | Low accuracy     |
| Comparator circuit      | Medium      | Good learning    |
| Op-amp comparator       | Medium      | Adjustable       |
| MCU ADC monitoring      | Medium      | Needs software   |
| MCU + relay             | Easy        | Slow             |
| MCU + MOSFET            | Better      | Common smart BMS |
| TL431 reference circuit | Medium      | Cheap precision  |
| Analog supervisor IC    | Easy        | Reliable         |
| Battery monitor IC      | Advanced    | Professional     |

---

## Components Used

| Method              | Components               |
| ------------------- | ------------------------ |
| BMS IC              | HX-3S-01, CM1041         |
| Zener               | Zener diode + transistor |
| Comparator          | LM393                    |
| Op-amp              | LM358                    |
| MCU                 | STM32F103CBT6            |
| Supervisor IC       | TLV803                   |
| Precision reference | TL431                    |

---

# 2. OVERDISCHARGE PROTECTION

## Purpose

Disconnect load when voltage becomes too low.

---

## Different Ways To Implement

| Method                       | Complexity |
| ---------------------------- | ---------- |
| Dedicated BMS IC             | Easy       |
| Comparator cutoff            | Medium     |
| Op-amp undervoltage detector | Medium     |
| MCU ADC monitoring           | Medium     |
| Relay cutoff                 | Easy       |
| MOSFET cutoff                | Better     |
| Voltage supervisor IC        | Easy       |
| TL431 undervoltage circuit   | Medium     |

---

## Components Used

| Method        | Components    |
| ------------- | ------------- |
| Comparator    | LM393         |
| Op-amp        | LM358         |
| MCU           | STM32F103CBT6 |
| MOSFET        | IRF3205       |
| Relay         | 12V relay     |
| Supervisor IC | TLV3012       |

---

# 3. OVERCURRENT PROTECTION

## Purpose

Stop excessive current.

---

## Different Ways To Implement

| Method                      | Complexity |
| --------------------------- | ---------- |
| Shunt resistor + comparator | Easy       |
| Shunt + op-amp              | Medium     |
| Shunt + MCU ADC             | Medium     |
| Hall sensor                 | Medium     |
| Current sensor IC           | Easy       |
| Resettable fuse (PTC)       | Very easy  |
| Fast electronic fuse        | Advanced   |

---

## Components Used

| Method         | Components |
| -------------- | ---------- |
| Shunt resistor | 0.01Ω      |
| Comparator     | LM393      |
| Op-amp         | INA180     |
| Hall sensor    | ACS712     |
| Sensor IC      | INA219     |
| Fuse           | PTC fuse   |

---

# 4. SHORT-CIRCUIT PROTECTION

## Purpose

Instant shutdown during short circuit.

---

## Different Ways To Implement

| Method                             | Complexity |
| ---------------------------------- | ---------- |
| BMS IC internal protection         | Easy       |
| Comparator current spike detection | Medium     |
| Fast MOSFET cutoff                 | Medium     |
| Electronic fuse                    | Advanced   |
| Physical fuse                      | Very easy  |
| Polyfuse/PTC                       | Easy       |
| Relay cutoff                       | Slow       |

---

## Components Used

| Method     | Components      |
| ---------- | --------------- |
| MOSFET     | IRF3205         |
| Fuse       | Blade fuse      |
| Comparator | LM393           |
| eFuse IC   | TPS25940        |
| PTC        | Resettable fuse |

---

# 5. MOSFET CUTOFF SWITCHING

## Purpose

Disconnect battery electronically.

---

## Different Ways To Implement

| Method                     | Complexity |
| -------------------------- | ---------- |
| N-channel MOSFET low-side  | Easy       |
| P-channel MOSFET high-side | Medium     |
| Back-to-back MOSFETs       | Common BMS |
| Relay switching            | Easy       |
| Contactor switching        | Heavy duty |
| Solid-state relay          | Advanced   |

---

## Components Used

| Method      | Components        |
| ----------- | ----------------- |
| N-MOSFET    | IRF3205           |
| P-MOSFET    | IRF9540           |
| Relay       | 12V relay         |
| SSR         | Solid-state relay |
| Gate driver | TC4420            |

---

# 6. BASIC CURRENT LIMITING

## Purpose

Limit maximum output current.

---

## Different Ways To Implement

| Method                   | Complexity |
| ------------------------ | ---------- |
| Fuse                     | Very easy  |
| PTC resettable fuse      | Easy       |
| Shunt + comparator       | Medium     |
| MCU controlled limiting  | Medium     |
| PWM current limiting     | Advanced   |
| Constant current circuit | Medium     |

---

## Components Used

| Method     | Components    |
| ---------- | ------------- |
| Fuse       | Blade fuse    |
| PTC        | Polyfuse      |
| Comparator | LM393         |
| MCU        | STM32F103CBT6 |
| MOSFET     | IRF3205       |

---

# 7. BATTERY CONNECTION TERMINALS

## Purpose

Connect cells safely.

---

## Different Ways To Implement

| Method                    | Notes            |
| ------------------------- | ---------------- |
| Spot welded nickel strips | Best             |
| Spring holders            | Easy             |
| Screw terminals           | Prototype        |
| XT60 connectors           | High current     |
| JST-XH balance connector  | Common balancing |
| Busbars                   | Heavy current    |

---

# COMPLETE COMPONENT LIST FOR FIRST STEP

## Main Components

| Component            | Quantity  |
| -------------------- | --------- |
| HX-3S-01 BMS IC      | 1         |
| IRF3205 MOSFET       | 2         |
| LM393 comparator     | 1         |
| LM358 op-amp         | 1         |
| 0.01Ω shunt resistor | 1         |
| Blade fuse           | 1         |
| PTC fuse             | 1         |
| JST-XH connector     | 1         |
| Screw terminal       | 4         |
| Capacitor 0.1uF      | 4         |
| Capacitor 10uF       | 2         |
| 100Ω resistor        | 4         |
| 1kΩ resistor         | 4         |
| 10kΩ resistor        | 6         |
| 100kΩ resistor       | 3         |
| Heatsink             | 2         |
| Perfboard/PCB        | 1         |
| Thick battery wires  | As needed |

---

# BATTERY REQUIRED

| Component           | Quantity |
| ------------------- | -------- |
| 18650 lithium cells | 3        |

Use:

* Same brand
* Same capacity
* Same age

---

# TOOLS REQUIRED

| Tool               | Mandatory   |
| ------------------ | ----------- |
| Multimeter         | Yes         |
| Soldering iron     | Yes         |
| Flux               | Recommended |
| Bench power supply | Recommended |
| Wire cutter        | Yes         |
| Insulation tape    | Yes         |

---

# WHAT STEP 1 WILL DO

After building:

* Battery protected from overcharge
* Battery protected from overdischarge
* Short-circuit shutdown
* Basic current limiting
* Automatic MOSFET cutoff

---

# WHAT STEP 1 WILL NOT DO

* Bluetooth
* LCD display
* Mobile app
* Wi-Fi
* Smart balancing
* Battery percentage
* STM32 monitoring
* Data logging

---

# STEP 2 — CELL BALANCING

## Functions

* Balance cell voltages
* Improve battery life

## Methods

| Method                     | Complexity |
| -------------------------- | ---------- |
| Passive resistor balancing | Easy       |
| MOSFET balancing           | Easy       |
| Capacitor balancing        | Medium     |
| Inductor balancing         | Hard       |
| Transformer balancing      | Very hard  |

---

# STEP 3 — VOLTAGE & CURRENT MONITORING

## Functions

* Measure pack voltage
* Measure current
* Measure individual cells

## Methods

| Method                 | Complexity |
| ---------------------- | ---------- |
| Voltage divider + ADC  | Easy       |
| Shunt resistor sensing | Medium     |
| Hall sensor            | Medium     |
| Current sensor IC      | Easy       |

---

# STEP 4 — STM32 SMART CONTROL

## Functions

* Smart protection
* Data processing
* ADC measurements
* Sensor management

## MCU Used

* STM32F103CBT6

## Communication Methods

| Method | Difficulty |
| ------ | ---------- |
| UART   | Easy       |
| I2C    | Easy       |
| SPI    | Medium     |
| CAN    | Advanced   |

---

# STEP 5 — SMART FEATURES

## Functions

* Bluetooth
* OLED display
* Data logging
* Mobile app

## Modules

| Module         | Usage        |
| -------------- | ------------ |
| HC-05          | Bluetooth    |
| ESP32          | Wi-Fi + BLE  |
| OLED SSD1306   | Display      |
| SD card module | Data logging |

---

# STEP 6 — ADVANCED INDUSTRIAL BMS

## Functions

* Active balancing
* CAN bus
* OTA firmware updates
* Industrial protection
* AI prediction
* EV integration

## Advanced ICs

| IC       | Usage                      |
| -------- | -------------------------- |
| LTC6811  | Industrial battery monitor |
| MAX17853 | Automotive BMS             |
| BQ40Z50  | Fuel gauge                 |

---

# RECOMMENDED LEARNING ORDER

1. Learn battery wiring
2. Learn MOSFET switching
3. Build simple protection BMS
4. Add balancing
5. Add STM32 monitoring
6. Add displays
7. Add Bluetooth
8. Add industrial features

---

# SAFETY NOTES

Lithium batteries can:

* Catch fire
* Explode
* Overheat

Always:

* Use fuse
* Avoid short circuits
* Use insulated tools
* Never reverse polarity
* Test with small loads first
* Check voltages carefully

---

# RECOMMENDED BEGINNER PATH

| Step           | Recommended Method |
| -------------- | ------------------ |
| Overcharge     | Dedicated BMS IC   |
| Overdischarge  | Dedicated BMS IC   |
| Overcurrent    | Shunt + comparator |
| Short-circuit  | MOSFET + fuse      |
| Monitoring     | STM32 ADC          |
| Smart features | ESP32 Bluetooth    |

---

# COMPLETE BMS FUNCTIONALITIES LIST

## Basic Protection Functions

1. Overcharge protection
2. Overdischarge protection
3. Overcurrent protection
4. Short-circuit protection
5. Reverse polarity protection
6. Overvoltage protection
7. Undervoltage protection
8. MOSFET cutoff switching
9. Fuse protection
10. Current limiting

---

## Cell Management Functions

11. Cell voltage monitoring
12. Cell balancing
13. Passive balancing
14. Active balancing
15. Cell mismatch detection
16. Weak cell detection
17. Cell failure detection
18. Open wire detection
19. Cell internal resistance monitoring
20. Cell temperature monitoring

---

## Battery Monitoring Functions

21. Pack voltage monitoring
22. Pack current monitoring
23. Power monitoring
24. Energy monitoring
25. Capacity estimation
26. Remaining runtime estimation
27. Coulomb counting
28. State of Charge (SOC) estimation
29. State of Health (SOH) estimation
30. Battery aging analysis

---

## Thermal Management Functions

31. Overtemperature protection
32. Undertemperature protection
33. Thermal runaway detection
34. Cooling fan control
35. Heater control
36. Multi-point temperature sensing
37. Thermal balancing

---

## Charging Functions

38. Charger enable/disable
39. Charge current limiting
40. Fast charging support
41. Smart charging control
42. Precharge control
43. Inrush current limiting
44. Charger communication

---

## Load Control Functions

45. Load enable/disable
46. Smart load distribution
47. Sleep mode
48. Wake-up detection
49. Idle shutdown
50. Auto recovery after fault

---

## Communication Functions

51. UART communication
52. I2C communication
53. SPI communication
54. CAN bus communication
55. RS485 communication
56. SMBus communication
57. USB communication
58. Bluetooth communication
59. Wi-Fi communication
60. Modbus communication

---

## Smart Functions

61. OLED/LCD display support
62. LED status indicators
63. Buzzer/alarm indication
64. Mobile app integration
65. Cloud monitoring
66. Remote diagnostics
67. OTA firmware updates
68. Password/authentication system
69. Battery ID recognition
70. Real-time telemetry

---

## Data Logging Functions

71. Event logging
72. Fault logging
73. Charge/discharge history
74. Cycle counting
75. EEPROM/flash storage
76. SD card logging
77. Usage analytics
78. Runtime statistics

---

## Industrial/Advanced Functions

79. Multi-pack synchronization
80. Master-slave architecture
81. Parallel pack management
82. Series stack management
83. Isolation monitoring
84. Ground fault detection
85. Leakage current detection
86. Arc fault detection
87. Fire risk detection
88. Emergency shutdown system
89. Redundant protection systems
90. Predictive maintenance

---

## EV / Smart Energy Functions

91. Regenerative braking support
92. EV motor controller communication
93. Solar charging integration
94. UPS integration
95. Smart inverter integration
96. Peak load management
97. Dynamic power limiting
98. Grid storage support
99. Vehicle telemetry integration
100. AI-based fault prediction

---

# END OF README
