# Touch-Based Device Control System for Bedridden Patients

A password-protected, touch-based device control system built on the ARM7 LPC2148 microcontroller, designed to help bedridden or mobility-limited patients operate essential appliances with minimal physical effort — with a password authentication layer to prevent unauthorized or accidental use.

---

## 🎯 Aim

Patients confined to bed often depend entirely on caregivers to control basic devices like lights or alerts. This project addresses that dependency using a resistive touchscreen interface that lets patients control connected devices directly, while a keypad-based password mechanism ensures only authorized users (patient/admin) can operate or reconfigure the system.

## 🖼️ Block Diagram

![image alt](https://github.com/sidaarths-ux/Touch-Based-Device-Control-System-for-Bedridden-Patients/blob/348ad77f96f71a03e2abee9670fcbc91b59dcd86/diagram-export-8-13-2026-1_30_15-AM.png)

## 🔁 System Flow

![image alt](https://github.com/sidaarths-ux/Touch-Based-Device-Control-System-for-Bedridden-Patients/blob/ef2ea312f402eada412d258f0e28ffc57296f709/touch%2C%20flowchart.jpeg)

## ⚙️ How It Works

1. On startup, the system waits for a password, entered via the 4x4 matrix keypad.
2. The entered password is validated against the value stored in the AT25LC512 SPI EEPROM.
3. Once authenticated, the touchscreen module is activated for device control.
4. The patient touches predefined zones on the touchscreen to turn **Device 1 (LED1)** and **Device 2 (LED2)** ON/OFF.
5. A dedicated touch zone allows the patient to trigger the **buzzer** for emergency alerts.
6. The touchscreen can be disabled after use to prevent accidental device control.
7. The admin/user can update the password via the keypad; the new password is written back to the EEPROM.

> **Note:** The AT25LC512 SPI EEPROM must be operated at **3.3V**.

## 🔧 Hardware Requirements

| Component | Role |
|---|---|
| LPC2148 (ARM7) | Core microcontroller — control logic, peripheral interfacing |
| Resistive Touch Screen Module | Patient touch input for device control |
| 16x2 LCD | Status/prompt display |
| 4x4 Matrix Keypad | Password entry and system configuration |
| Device 1 (LED1) | Simulated controllable appliance |
| Device 2 (LED2) | Simulated controllable appliance |
| Buzzer | Emergency alert output |
| AT25LC512 (SPI EEPROM) | Persistent password and configuration storage (3.3V) |

## 💻 Software Requirements

- Embedded C
- Keil µVision (Keil-C Compiler)
- Flash Magic (for flashing the LPC2148)

## 🛠️ Implementation Sequence

The system was built and validated module-by-module before final integration:

1. **LCD check** — display character, string, and integer constants.
2. **Keypad check** — read and display key values on the LCD.
3. **UART check** — verify UART interrupt-based communication on hardware.
4. **EEPROM check** — write and read N bytes to/from the AT25LC512 using Byte Write/Byte Read functions, display on LCD.
5. **Touchscreen check (PC-side)** — verify touchscreen module output via MAX232 interfacing with a PC.
6. **Touchscreen check (MCU-side)** — read touchscreen data using UART interrupt logic.
7. **Integration** — combine all peripheral drivers into `projectmain.c`, initialize peripherals, and implement the main application logic:
   - Prompt for password → validate against EEPROM
   - On success, activate touchscreen control of Device 1 / Device 2
   - Support buzzer-based emergency alert via touch
   - Support password change, with the updated password saved back to EEPROM



## 🚀 Getting Started

### Prerequisites
- Keil µVision IDE
- Flash Magic
- LPC2148 board wired to: resistive touchscreen, 16x2 LCD, 4x4 keypad, AT25LC512 EEPROM (3.3V), 2x LED (devices), buzzer

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
2. Open the project in Keil µVision and build to generate the `.hex` file.
3. Flash the `.hex` file to the LPC2148 using Flash Magic.
4. Power on the hardware, enter the default password via the keypad, and use the touchscreen to control the devices.

## 🔮 Future Scope

- Wireless (Bluetooth/Wi-Fi) monitoring for caregivers
- Support for additional controllable devices
- Voice-assist fallback for patients unable to use touch or keypad input
- OLED/graphical display for richer status feedback

## 👤 Author

**Sidaarth.S**
B.Tech ECE, VIT Vellore
