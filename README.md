🚗 ESP32 Bluetooth Car — Dabble GamePad

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white" alt="ESP32">
  <img src="https://img.shields.io/badge/Driver-L298N-blue?style=for-the-badge" alt="L298N">
  <img src="https://img.shields.io/badge/Control-Bluetooth-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white" alt="Bluetooth">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++">
</p><p align="center">
  <b>Control a two-motor robot car wirelessly using an ESP32, an L298N motor driver, and the Dabble GamePad app.</b>
</p>---

📑 Table of Contents

- "✨ Features" (#-features)
- "🧰 Components Required" (#-components-required)
- "🏗️ System Architecture" (#️-system-architecture)
- "🔌 Wiring Connections" (#-wiring-connections)
- "🗺️ Text Wiring Diagram" (#️-text-wiring-diagram)
- "📱 Bluetooth Setup" (#-bluetooth-setup)
- "🎮 Controls" (#-controls)
- "💻 Software Requirements" (#-software-requirements)
- "⚙️ Installation" (#️-installation)
- "🔋 Power and Safety" (#-power-and-safety)
- "🛠️ Troubleshooting" (#️-troubleshooting)
- "📂 Repository Structure" (#-repository-structure)
- "👨‍💻 Developer" (#-developer)
- "📜 License" (#-license)

---

✨ Features

- 📱 Wireless control using Bluetooth.
- 🎮 Directional control through Dabble GamePad.
- ⚡ PWM-based motor speed control.
- ↔️ Forward, reverse, left, and right movement.
- 🔧 Two DC motors controlled independently.
- 🧠 ESP32-based control system.
- 🔌 L298N dual H-bridge motor driver.

🧰 Components Required

No.| Component| Quantity
1| ESP32 development board with Bluetooth support| 1
2| L298N dual motor driver module| 1
3| DC geared motors| 2
4| Robot car chassis and wheels| 1 set
5| Suitable motor battery or power supply| 1
6| Jumper wires| As required
7| USB cable for programming| 1

🏗️ System Architecture

┌────────────────────┐
│   Dabble GamePad   │
│   Smartphone App   │
└─────────┬──────────┘
          │ Bluetooth
          ▼
┌────────────────────┐
│        ESP32       │
│ Direction + PWM    │
└─────────┬──────────┘
          │ GPIO Signals
          ▼
┌────────────────────┐
│   L298N Driver     │
│   Dual H-Bridge     │
└──────┬───────┬─────┘
       │       │
       ▼       ▼
  Right Motor  Left Motor

🔌 Wiring Connections

ESP32 → L298N

ESP32 GPIO| L298N Pin| Function
GPIO 22| ENA| Right motor speed (PWM)
GPIO 16| IN1| Right motor direction
GPIO 17| IN2| Right motor direction
GPIO 23| ENB| Left motor speed (PWM)
GPIO 18| IN3| Left motor direction
GPIO 19| IN4| Left motor direction
GND| GND| Common ground

L298N → Motors and Power

L298N Terminal| Connection
OUT1| Right motor wire 1
OUT2| Right motor wire 2
OUT3| Left motor wire 1
OUT4| Left motor wire 2
"+12V" / "VS"| Motor supply positive
GND| Motor supply negative and ESP32 GND

«Important: The L298N terminal marked "+12V" is the motor supply input; it does not mean you must use a 12 V battery. Select a suitable supply for your motors and driver.»

🗺️ Text Wiring Diagram

           ESP32                         L298N
     ┌────────────────┐           ┌─────────────────┐
     │                │           │                 │
     │ GPIO 22 ───────┼──────────►│ ENA             │
     │ GPIO 16 ───────┼──────────►│ IN1             │
     │ GPIO 17 ───────┼──────────►│ IN2             │
     │                │           │                 │
     │ GPIO 23 ───────┼──────────►│ ENB             │
     │ GPIO 18 ───────┼──────────►│ IN3             │
     │ GPIO 19 ───────┼──────────►│ IN4             │
     │                │           │                 │
     │ GND ───────────┼───────────┤ GND             │
     └────────────────┘           │                 │
                                  │ OUT1 ──┐        │
                                  │        ├── Right Motor
                                  │ OUT2 ──┘        │
                                  │                 │
                                  │ OUT3 ──┐        │
                                  │        ├── Left Motor
                                  │ OUT4 ──┘        │
                                  │                 │
 Motor Battery (+) ───────────────►│ +12V / VS       │
 Motor Battery (-) ───────────────►│ GND             │
                                  └─────────────────┘

⚠️ PWM Jumper Configuration

- Remove the ENA and ENB jumpers before connecting GPIO 22 and GPIO 23 to the enable pins.
- Keep ESP32 GND and L298N GND connected.
- Do not feed motor battery voltage into the ESP32 3.3 V pin.
- Check the module's 5 V regulator arrangement before powering it.

📱 Bluetooth Setup

1. Install the Dabble mobile app.

2. Upload the Arduino sketch to your ESP32.

3. Power on the ESP32 and motor driver.

4. Open Dabble and select the GamePad module.

5. Connect to the Bluetooth device named:
   
   "MyBluetoothCar"

6. Use the directional controls to move the car.

«Bluetooth discovery and connection options may differ depending on the Dabble app version and the ESP32 board package.»

🎮 Controls

GamePad Button| Right Motor| Left Motor| Movement
⬆️ Up| Forward| Forward| Move forward
⬇️ Down| Reverse| Reverse| Move backward
⬅️ Left| Forward| Reverse| Turn left
➡️ Right| Reverse| Forward| Turn right
No direction pressed| Stop command| Stop command| Stop driving

Note: The actual left/right turning direction depends on the physical motor mounting and wiring. Swap a motor's output wires if its direction is reversed.

💻 Software Requirements

- Arduino IDE
- ESP32 board package compatible with Arduino-ESP32 Core 3.x
- DabbleESP32 library
- Dabble mobile app

PWM Configuration

This project uses:

Setting| Value
PWM frequency| 1000 Hz
PWM resolution| 8-bit
Maximum PWM duty| 255
Right motor enable| GPIO 22
Left motor enable| GPIO 23

The sketch uses the Arduino-ESP32 Core 3.x functions "ledcAttach()" and "ledcWrite(pin, duty)".

⚙️ Installation

Step 1 — Clone the Repository

git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git

Step 2 — Open the Sketch

Open the ".ino" file in Arduino IDE.

Step 3 — Install the Library

Install the DabbleESP32 library and its required dependencies.

Step 4 — Select the Board

Choose your ESP32 board and the correct serial port in Arduino IDE.

Step 5 — Upload

Upload the code and open Serial Monitor at 115200 baud if you need to inspect startup messages.

Step 6 — Test

Connect through Dabble and test each direction with the car's wheels safely lifted off the ground first.

🔋 Power and Safety

- Use a motor supply that matches your DC motors' voltage and current requirements.
- Never power DC motors directly from ESP32 GPIO pins.
- Ensure all grounds are common.
- Check motor stall current against the L298N driver's capabilities.
- Disconnect power before changing wiring.
- Keep wheels off the ground during initial testing.
- Do not connect two power-source outputs together.
- Verify the L298N onboard 5 V regulator and jumper configuration for your specific module.

🛠️ Troubleshooting

Problem| Possible Cause| Solution
ESP32 does not appear in Dabble| Bluetooth mode or pairing issue| Verify the board supports Bluetooth Classic and check Dabble compatibility
Motors do not move| Missing motor supply or loose wiring| Check battery voltage, grounds, and output connections
Only one motor works| Wiring or driver channel issue| Check ENA/ENB and the corresponding IN/OUT pins
Motor direction is reversed| Motor wires or chassis orientation| Swap the two wires on that motor's output
PWM does not work| ENA/ENB jumpers still installed| Remove both jumpers and verify GPIO connections
ESP32 restarts when motors start| Voltage drop or electrical noise| Use a suitable motor supply and stable ESP32 power
Compilation fails on LEDC functions| Incompatible ESP32 core version| Select an Arduino-ESP32 Core 3.x-compatible installation

📂 Repository Structure

YOUR_REPOSITORY/
│
├── README.md
├── src/
│   └── BluetoothCar.ino
│
└── images/
    ├── wiring-diagram.png
    └── car-prototype.png

🖼️ Add Your Own Images Using GitHub Raw URLs

Upload an image to your repository, then use its raw URL:

![Wiring Diagram](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY/main/images/wiring-diagram.png)

For a project prototype:

![Bluetooth Car Prototype](https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY/main/images/car-prototype.png)

Tip: The file path, branch name, and letter case must match your repository exactly. GitHub's "main" branch is assumed in these examples.

👨‍💻 Developer

Tanvir Hussain

- GitHub: "@TanvirCodeStorm" (https://github.com/TanvirCodeStorm)
- Project: ESP32 Bluetooth Car
- Technology: ESP32 · L298N · Dabble · Arduino C++

If you find this project useful, consider giving the repository a ⭐ star!

---

<p align="center">
  <b>Built with curiosity, code, and electronics. 🚀</b>
</p>
