<div align="center">🚗 ESP32-Bluetooth-Car

⚡ Wireless Robotics • Smart Control • Embedded Systems

A Bluetooth-controlled robotic car powered by ESP32, L298N and Dabble GamePad.

<br>""ESP32" (https://img.shields.io/badge/ESP32-Controller-E7352C?style=for-the-badge&logo=espressif&logoColor=white)" (https://www.espressif.com/)
""C++" (https://img.shields.io/badge/C%2B%2B-Firmware-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)" (https://isocpp.org/)
""Bluetooth" (https://img.shields.io/badge/Bluetooth-Wireless-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white)" (https://github.com/)
""L298N" (https://img.shields.io/badge/L298N-Motor_Driver-FF6F00?style=for-the-badge)" (https://www.st.com/)

<br>⬆️ Forward　 ⬇️ Reverse　 ⬅️ Left　 ➡️ Right

</div>---

📌 Overview

Turn a standard two-motor robot chassis into a wireless robotic vehicle.

This project uses an ESP32 to receive GamePad commands through Bluetooth and control two DC motors through an L298N dual H-bridge motor driver.

✨ Highlights

- 📱 Wireless control through the Dabble GamePad.
- ⚙️ Independent direction control for two DC motors.
- ⚡ PWM motor control with 8-bit resolution.
- 🔄 Forward, reverse and differential turning.
- 🧠 ESP32-based embedded control.
- 🔧 Simple, clearly mapped GPIO connections.

---

🧭 Contents

- "🏗️ System Architecture" (#️-system-architecture)
- "🧰 Hardware Requirements" (#-hardware-requirements)
- "🔌 Pin Connections" (#-pin-connections)
- "🗺️ Wiring Diagram" (#️-wiring-diagram)
- "🎮 Controls" (#-controls)
- "💻 Software Setup" (#-software-setup)
- "🔋 Power and Safety" (#-power-and-safety)
- "🛠️ Troubleshooting" (#️-troubleshooting)
- "📂 Project Structure" (#-project-structure)
- "👨‍💻 Developer" (#-developer)

---

🏗️ System Architecture

┌─────────────────────────┐
│      📱 Smartphone      │
│     Dabble GamePad      │
└────────────┬────────────┘
             │
        Bluetooth
             │
             ▼
┌─────────────────────────┐
│         ESP32           │
│                         │
│  Command Processing     │
│  Direction Control      │
│  PWM Generation         │
└────────────┬────────────┘
             │
         GPIO Signals
             │
             ▼
┌─────────────────────────┐
│      L298N DRIVER       │
│      Dual H-Bridge      │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
 ┌──────────┐ ┌──────────┐
 │  RIGHT   │ │   LEFT   │
 │  MOTOR   │ │  MOTOR   │
 └──────────┘ └──────────┘

🔄 Operating Principle

1. The user presses a direction in Dabble GamePad.
2. The ESP32 processes the command.
3. GPIO outputs determine each motor's direction.
4. PWM signals control the motor driver's enable inputs.
5. The L298N drives the motors according to the commands.

---

🧰 Hardware Requirements

Component| Quantity
ESP32 development board| 1
L298N dual motor driver| 1
DC geared motors| 2
Robot chassis and wheels| 1 set
Suitable motor power supply| 1
Jumper wires| As required
USB cable| 1

---

🔌 Pin Connections

ESP32 → L298N

ESP32 GPIO| L298N Pin| Function
"GPIO 22"| "ENA"| Right motor PWM
"GPIO 16"| "IN1"| Right motor direction
"GPIO 17"| "IN2"| Right motor direction
"GPIO 23"| "ENB"| Left motor PWM
"GPIO 18"| "IN3"| Left motor direction
"GPIO 19"| "IN4"| Left motor direction
"GND"| "GND"| Common ground

L298N → Motors and Power

L298N Terminal| Connection
"OUT1" and "OUT2"| Right DC motor
"OUT3" and "OUT4"| Left DC motor
"VS / +12V"| Motor supply positive
"GND"| Motor supply negative and ESP32 ground

«PWM configuration: Remove the ENA and ENB jumpers before using GPIO 22 and GPIO 23 for PWM speed control.»

---

🗺️ Wiring Diagram

       ESP32 DEVKIT                  L298N MODULE
     ┌────────────────┐           ┌────────────────┐
     │                │           │                │
     │ GPIO 22 ───────┼──────────►│ ENA            │
     │ GPIO 16 ───────┼──────────►│ IN1            │
     │ GPIO 17 ───────┼──────────►│ IN2            │
     │                │           │                │
     │ GPIO 23 ───────┼──────────►│ ENB            │
     │ GPIO 18 ───────┼──────────►│ IN3            │
     │ GPIO 19 ───────┼──────────►│ IN4            │
     │                │           │                │
     │ GND ───────────┼───────────┤ GND            │
     └────────────────┘           │                │
                                  │ OUT1 ──┐       │
                                  │        ├─ RIGHT│
                                  │ OUT2 ──┘ MOTOR │
                                  │                │
                                  │ OUT3 ──┐       │
                                  │        ├─ LEFT │
                                  │ OUT4 ──┘ MOTOR │
                                  │                │
 Motor Supply (+) ───────────────►│ VS / +12V      │
 Motor Supply (-) ───────────────►│ GND            │
                                  └────────────────┘

Grounding requirement: The ESP32 ground, L298N ground and motor supply negative must share a common ground.

---

🎮 Controls

GamePad Button| Right Motor| Left Motor| Movement
⬆️ UP| Forward| Forward| Forward
⬇️ DOWN| Reverse| Reverse| Reverse
⬅️ LEFT| Forward| Reverse| Turn left
➡️ RIGHT| Reverse| Forward| Turn right
⏹️ No direction| Stop command| Stop command| Stop

Actual turning direction depends on motor mounting and wiring.

⚡ PWM Configuration

Parameter| Value
PWM frequency| "1000 Hz"
PWM resolution| "8-bit"
Maximum duty value| "255"
Right motor enable| "GPIO 22"
Left motor enable| "GPIO 23"

The firmware uses "ledcAttach()" and "ledcWrite(pin, duty)", as supported by the Arduino-ESP32 Core 3.x LEDC API.

---

💻 Software Setup

Requirements

- Arduino IDE
- Compatible ESP32 board package, Core 3.x
- "DabbleESP32" library
- Dabble mobile application
- ESP32 board compatible with the Bluetooth mode required by the library

Firmware Configuration

The Bluetooth device name is:

Dabble.begin("MyBluetoothCar");

The sketch configures the motor pins, initializes PWM and processes GamePad inputs continuously.

Run the Project

1. Open the Arduino sketch.
2. Select the correct ESP32 board and serial port.
3. Install the required Dabble library.
4. Upload the firmware.
5. Power the motor driver with a suitable motor supply.
6. Open Dabble, select GamePad and connect to "MyBluetoothCar".
7. Test movement with the wheels raised before driving.

---

🔋 Power and Safety

- 🔌 Never connect motors directly to ESP32 GPIO pins.
- 🔋 Match the motor supply to the motors' voltage and current requirements.
- 🔗 Keep ESP32 and L298N grounds connected.
- ⚠️ Never connect motor battery voltage directly to the ESP32 3.3 V pin.
- ⚡ Check the L298N onboard regulator and jumper configuration.
- 🛑 Disconnect power before modifying connections.
- 🧪 Test the system with the wheels raised first.

---

🛠️ Troubleshooting

Problem| Check
Motors do not move| Motor supply, ground and output wiring
Only one motor works| Motor terminals and driver channel
Motor direction is reversed| Swap that motor's output wires
PWM speed control fails| ENA/ENB jumpers and LEDC configuration
ESP32 restarts under load| Supply voltage drop and motor interference
Bluetooth connection fails| ESP32 Bluetooth capability and library compatibility
Firmware fails to compile| ESP32 board package and Dabble library

---

📂 Project Structure

ESP32-Bluetooth-Car/
├── README.md
├── src/
│   └── BluetoothCar.ino
└── images/
    ├── wiring-diagram.png
    └── car-prototype.png

---

👨‍💻 Developer

<div align="center">Tanvir Hussain

Robotics · Electronics · Embedded Programming

""GitHub" (https://img.shields.io/badge/GitHub-TanvirCodeStorm-181717?style=for-the-badge&logo=github)" (https://github.com/TanvirCodeStorm)

Turning code into motion. One project at a time. ⚡

</div>---

<div align="center">🚗 ESP32 × L298N × Dabble

CONNECT · CONTROL · DRIVE

</div>