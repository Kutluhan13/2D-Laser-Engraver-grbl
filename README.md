# 2D Laser Engraver (GRBL-Based)

A compact and functional 2D laser engraver built using GRBL firmware, Arduino Nano, and CD/DVD stepper mechanisms. It is also suitable for CNC drawing or lightweight milling applications.

---

## ⚠️ Safety Notes

- Never connect/disconnect components while the system is powered.
- Disconnect all peripherals from the Arduino during the initial GRBL upload.
- Avoid touching electronics or motors during operation; use ESD precautions when handling components.

---

## 🔒 Laser Safety

- This project uses a **Class 4 laser module (405 nm)** which poses risks of eye damage and skin burns. Always wear protective eyewear rated for 405 nm.
- Use a proper **constant-current driver with ESD protection** for the laser diode.
- Ensure cooling is in place; powerful diodes heat up quickly and require heatsinks.
- Adjust the laser focus according to the material height for optimal engraving.

---

## 🧰 Components Required

- 0.5W 405nm TTL Laser + Driver (12V)
- Arduino Nano (ATmega328P, 5V/16MHz)
- 2× Easydriver Stepper Motor Drivers
- 2× CD/DVD Drive Stepper Mechanisms
- Frame (3D-printable, design files included)
- Step-down Buck Converter (Min. 15V input)

---

## 🛠️ Physical Setup

- Mount motors and electronics on the frame.
- Wire each stepper's 4 pins to the drivers (reverse if axis direction is incorrect).
- Power: 5V for drivers and motors, 12V for laser.
- Common GND must be shared across all components.

---

## 🔌 Signal Wiring

| Signal       | Arduino Pin | Description               |
| ------------ | ----------- | ------------------------- |
| Stepper Cut  | D8          | Easydriver EN pin         |
| Laser Enable | D12         | TTL input of laser driver |
| X Step / Dir | D2 / D3     | Base axis                 |
| Y Step / Dir | D4 / D5     | Top axis                  |

---

## 💻 Software Setup

- Use **ATmega328P** (not ATmega168).
- Copy the `grbl` folder inside `grbl-K13` to Arduino’s libraries directory.
- Open Arduino IDE → File → Examples → grbl → grblUpload and upload to Nano.
- Use **115200 baud rate** in Serial Monitor and type `$RST=*` to reset settings.
- Test movement:
  ```
  G91 G28 X0 Y0
  X10 Y10
  ```
  If movement is inverted, reverse the stepper connections.

---

## ⚙️ GRBL Tuning

Default GRBL settings are adjusted for this hardware. For new builds, tune parameters like `steps/mm`, `acceleration`, and `max travel` experimentally or via GRBL documentation:

- [https://github.com/grbl/grbl/wiki](https://github.com/grbl/grbl/wiki)

---

## 📟 Usage

Send any 2D G-code design to the device using **Universal G-code Sender**:

- [https://github.com/winder/Universal-G-Code-Sender](https://github.com/winder/Universal-G-Code-Sender)