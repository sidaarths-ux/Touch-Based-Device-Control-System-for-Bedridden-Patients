# Touch-Based Device Control System for Bedridden Patients

An embedded assistive-technology system that lets bedridden or mobility-limited patients independently control nearby electrical devices — such as fans, lights, and emergency buzzers — through a simple touchscreen interface, reducing dependency on caregivers for routine tasks.

---

## 📌 Overview

Bedridden patients often rely entirely on caregivers for basic tasks like switching on a fan, turning off a light, or raising an alert — even for the smallest routine needs. This project addresses that dependency with a low-cost embedded control system built around a resistive touchscreen, giving patients a simple, direct way to control their immediate environment without physical switches or verbal requests.

## 🎯 Problem Statement

- Patients confined to bed have limited or no access to conventional switches/appliance controls.
- Constant reliance on caregivers for minor tasks reduces patient independence and increases caregiver workload.
- There is a need for a low-cost, easy-to-use, non-verbal interface for environmental control.

## ✨ Features

- Touch-based control of multiple connected devices (fan, light, buzzer, etc.)
- Zone-based touch mapping — each screen region corresponds to a specific device/function
- Persistent configuration storage using external EEPROM (settings survive power cycles)
- Serial communication support for debugging/external module integration
- Low-cost, low-power hardware suitable for hospital or home-care environments

## 🛠️ System Architecture

**Working principle:**
1. Patient touches a labeled zone on the resistive touchscreen.
2. The analog touch position is sampled by the microcontroller's ADC.
3. The sampled values are converted to digital coordinates and compared against predefined zone boundaries.
4. The matched zone is decoded into a device-control command.
5. The microcontroller drives the relay output stage to switch the corresponding device ON/OFF.
6. Zone mapping and calibration data are read from/written to an external EEPROM over SPI, so settings persist across resets.

```
[Resistive Touchscreen] --(analog)--> [ADC] --> [LPC2148 MCU] --> [Relay Driver] --> [Connected Device]
                                                       |
                                                  [SPI EEPROM]  (config/calibration storage)
                                                       |
                                                    [UART]  (debug / external module)
```

## 🔧 Hardware Components

| Component | Purpose |
|---|---|
| ARM7 LPC2148 Microcontroller | Core processing — touch decoding, control logic |
| Resistive Touchscreen | Patient input interface |
| SPI EEPROM | Persistent storage for zone mapping/calibration |
| Relay Driver Circuit | Switches connected appliances |
| UART Module | Debugging / external device communication |

## 💻 Tools & Technologies

- **MCU:** ARM7 LPC2148
- **IDE/Programmer:** Keil µVision, Flash Magic
- **Language:** Embedded C (register-level programming)
- **Protocols:** SPI, UART, ADC-based touch sensing
- **Simulation (optional):** Proteus

## 📂 Repository Structure

```
├── src/            # Firmware source files
├── inc/            # Header files
├── docs/           # Circuit diagrams, project report, images
└── README.md
```
*(Adjust this section to match your actual folder layout.)*

## 🚀 Getting Started

### Prerequisites
- Keil µVision IDE
- Flash Magic (for flashing the LPC2148)
- LPC2148 development board with resistive touchscreen, SPI EEPROM, and relay module connected

### Setup
1. Clone the repository:
   ```
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
2. Open the project in Keil µVision.
3. Build the project to generate the `.hex` file.
4. Flash the `.hex` file to the LPC2148 using Flash Magic.
5. Power on the board and calibrate the touchscreen if prompted.

## 🔮 Future Scope

- Add wireless control (Bluetooth/Wi-Fi) for remote monitoring by caregivers
- Voice-assist fallback for patients unable to use touch
- Expand to more devices with a scrollable/multi-page touch UI
- Add feedback display (LCD/OLED) to show current device states

## 👤 Author

**Sidaarth Saravana Kumar**
B.Tech ECE, VIT Vellore

## 📄 License

*(Add a license of your choice, e.g., MIT License, if you want others to freely use/modify this project.)*
