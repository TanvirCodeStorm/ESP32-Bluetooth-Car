<div align="center">🚗 ESP32 BLUETOOTH CAR

⚡ Wireless Control • 🤖 Robotics • 🔧 Embedded Systems

A Bluetooth-controlled robot car built with ESP32, L298N and Dabble GamePad.

<br>""ESP32" (https://img.shields.io/badge/ESP32-Microcontroller-E7352C?style=for-the-badge&logo=espressif&logoColor=white)" (https://www.espressif.com/)
""C++" (https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)" (https://isocpp.org/)
""Bluetooth" (https://img.shields.io/badge/Control-Bluetooth-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white)" (https://github.com/)
""Driver" (https://img.shields.io/badge/Driver-L298N-orange?style=for-the-badge)" (https://www.st.com/)

<br>⬆️ Forward   ⬇️ Reverse   ⬅️ Left   ➡️ Right

<br>From smartphone commands to real-world motion. 🚀

</div>---

📑・Table of Contents

#| Section
01| ✨ "Project Highlights" (#-project-highlights)
02| 🧰 "Components Required" (#-components-required)
03| 🏗️ "System Architecture" (#️-system-architecture)
04| 🔌 "Wiring Connections" (#-wiring-connections)
05| 🗺️ "Text Wiring Diagram" (#️-text-wiring-diagram)
06| 🎮 "Control System" (#-control-system)
07| 💻 "Installation Guide" (#-installation-guide)
08| 🖼️ "Project Gallery" (#️-project-gallery)
09| 🛠️ "Troubleshooting" (#️-troubleshooting)
10| ⚠️ "Power & Safety" (#️-power--safety)
11| 👨‍💻 "Developer" (#-developer)

---

✨ Project Highlights

«A compact robotics project that combines wireless communication, embedded programming and motor control.»

- 📱 Wireless Control — Drive the car using the Dabble mobile application.
- 🧠 ESP32 Controller — Process commands and control both motors.
- ⚙️ Dual Motor Driver — Use the L298N to control motor direction.
- ⚡ PWM Speed Control — Adjust motor drive duty using 8-bit PWM.
- 🔄 Four Directions — Move forward, reverse, left and right.
- 🔧 Beginner-Friendly Hardware — Built from common robotics components.

---

🧰 Components Required

🔢| Component| Qty.
1️⃣| ESP32 development board with compatible Bluetooth| 1
2️⃣| L298N dual H-bridge motor driver| 1
3️⃣| DC geared motors| 2
4️⃣| Robot chassis and wheels| 1 set
5️⃣| Suitable motor battery| 1
6️⃣| Jumper wires| As needed
7️⃣| USB cable| 1

---

🏗️ System Architecture

<div align="center">       📱 SMARTPHONE
       ┌───────────────┐
       │  Dabble App   │
       │   GamePad     │
       └───────┬───────┘
               │
          📶 Bluetooth
               │
               ▼
       ┌───────────────┐
       │     ESP32     │
       │               │
       │ Command Logic │
       │ Direction PWM│
       └───────┬───────┘
               │
          🔌 GPIO Signals
               │
               ▼
       ┌───────────────┐
       │     L298N     │
       │ Motor Driver  │
       └───────┬───────┘
               │
          ┌────┴────┐
          ▼         ▼
      ⚙️ RIGHT   ⚙️ LEFT
       MOTOR      MOTOR

</div>🔄 How It Works

1. 📱 The user presses a directional button in Dabble.
2. 📶 The ESP32 receives the Bluetooth command.
3. 🧠 The program determines each motor's direction.
4. ⚡ GPIO 22 and GPIO 23 provide PWM speed control.
5. ⚙️ The L298N drives the two DC motors.

---

🔌 Wiring Connections

🟦 ESP32 → L298N

ESP32 Pin| L298N Pin| Function
"GPIO 22"| "ENA"| ⚡ Right motor PWM
"GPIO 16"| "IN1"| 🔄 Right motor direction
"GPIO 17"| "IN2"| 🔄 Right motor direction
"GPIO 23"| "ENB"| ⚡ Left motor PWM
"GPIO 18"| "IN3"| 🔄 Left motor direction
"GPIO 19"| "IN4"| 🔄 Left motor direction
"GND"| "GND"| 🔗 Common ground

🟥 L298N → Motors

L298N Terminal| Connection
"OUT1" + "OUT2"| ⚙️ Right DC motor
"OUT3" + "OUT4"| ⚙️ Left DC motor
"VS / +12V"| 🔋 Motor supply positive
"GND"| 🔋 Motor supply negative and ESP32 GND

«💡 Remember: The L298N terminal marked "+12V" is the motor supply input. You do not necessarily need a 12 V battery; use a voltage suitable for your motors and driver.»

⚠️ PWM Jumper Configuration

- Remove the ENA and ENB jumpers to use GPIO 22 and GPIO 23 for PWM.
- Connect ESP32 GND to L298N GND.
- Check the module's onboard 5 V regulator configuration before powering it.
- Never connect the motor battery directly to the ESP32 3.3 V pin.

---

🗺️ Text Wiring Diagram

        ESP32 DEVKIT V1                L298N DRIVER
      ┌─────────────────┐          ┌─────────────────┐
      │                 │          │                 │
      │ GPIO 22 ────────┼─────────►│ ENA             │
      │ GPIO 16 ────────┼─────────►│ IN1             │
      │ GPIO 17 ────────┼─────────►│ IN2             │
      │                 │          │                 │
      │ GPIO 23 ────────┼─────────►│ ENB             │
      │ GPIO 18 ────────┼─────────►│ IN3             │
      │ GPIO 19 ────────┼─────────►│ IN4             │
      │                 │          │                 │
      │ GND ────────────┼──────────┤ GND             │
      └─────────────────┘          │                 │
                                   │ OUT1 ──┐        │
                                   │        ├─ RIGHT │
                                   │ OUT2 ──┘  MOTOR │
                                   │                 │
                                   │ OUT3 ──┐        │
                                   │        ├─ LEFT  │
                                   │ OUT4 ──┘  MOTOR │
                                   │                 │
 Battery (+) ─────────────────────►│ VS / +12V       │
 Battery (-) ─────────────────────►│ GND             │
                                   └─────────────────┘

---

🎮 Control System

🎮 Dabble Button| ⚙️ Right Motor| ⚙️ Left Motor| 🚗 Action
⬆️ UP| Forward| Forward| Move forward
⬇️ DOWN| Reverse| Reverse| Move backward
⬅️ LEFT| Forward| Reverse| Turn left
➡️ RIGHT| Reverse| Forward| Turn right
⏹️ No direction| Stop command| Stop command| Stop driving

⚡ PWM Configuration

Parameter| Value
PWM frequency| "1000 Hz"
PWM resolution| "8-bit"
Maximum duty value| "255"
Right motor enable| "GPIO 22"
Left motor enable| "GPIO 23"

Note: The sketch uses "ledcAttach()" and "ledcWrite(pin, duty)", compatible with the Arduino-ESP32 Core 3.x LEDC API.

---

💻 Installation Guide

1️⃣ Clone the Repository

git clone https://github.com/TanvirCodeStorm/YOUR_REPOSITORY.git

2️⃣ Open the Arduino Sketch

Open your ".ino" file using Arduino IDE.

3️⃣ Install the Required Library

Install the "DabbleESP32" library and its dependencies.

4️⃣ Configure Your ESP32

- Select the correct ESP32 board.
- Select the correct serial port.
- Ensure your board package supports the code's LEDC functions.

5️⃣ Upload the Firmware

Upload the sketch to your ESP32.

6️⃣ Connect Your Phone 📱

1. Power the ESP32 and motor driver.
2. Open the Dabble application.
3. Select the GamePad module.
4. Connect to "MyBluetoothCar".
5. Test the directional controls with the wheels raised.

«📌 Bluetooth compatibility depends on the exact ESP32 variant and the Bluetooth mode supported by your Dabble library.»

---

🖼️ Project Gallery

<div align="center">🔌 Wiring Diagram

<img src="https://raw.githubusercontent.com/TanvirCodeStorm/YOUR_REPOSITORY/main/images/wiring-diagram.png" alt="ESP32 and L298N wiring diagram" width="90%">ESP32 GPIO connections to the L298N motor driver.

<br>🚘 Robot Prototype

<img src="https://raw.githubusercontent.com/TanvirCodeStorm/YOUR_REPOSITORY/main/images/car-prototype.png" alt="ESP32 Bluetooth car prototype" width="90%">The assembled Bluetooth-controlled robot car.

</div>📷 
---

🛠️ Troubleshooting

❌ Problem| 🔍 Possible Cause| ✅ Solution
Car does not move| Power or wiring issue| Check motor supply and common ground
Only one motor works| Loose connection| Check the motor and driver terminals
Motor spins backward| Reversed polarity| Swap the motor's two output wires
PWM does not work| ENA/ENB jumpers installed| Remove the jumpers
ESP32 keeps restarting| Power drop or motor interference| Improve power stability and wiring
Bluetooth will not connect| Unsupported Bluetooth mode| Verify ESP32 and Dabble compatibility
Compilation fails| Incorrect ESP32 core| Use a compatible Core 3.x release

---

⚠️ Power & Safety

- 🔋 Use a suitable motor supply for your motor voltage and current.
- 🔌 Never power motors directly from ESP32 GPIO pins.
- 🔗 Keep ESP32 and L298N grounds connected.
- 🚫 Never feed motor battery voltage into the ESP32 3.3 V pin.
- 🛑 Disconnect power before changing connections.
- 🧪 Test the car with its wheels raised before driving it on the ground.
- ⚡ Check the L298N regulator and jumper configuration before applying power.

---

📂 Repository Structure

ESP32-Bluetooth-Car/
│
├── 📄 README.md
├── 📁 src/
│   └── 📄 BluetoothCar.ino
│
├── 📁 images/
    ├── 🖼️ wiring-diagram.png
    └── 🖼️ car-prototype

---

👨‍💻 Developer

<div align="center">🚀 TANVIR HUSSAIN

Robotics • Electronics • Embedded Programming

""GitHub" (https://img.shields.io/badge/GitHub-TanvirCodeStorm-181717?style=for-the-badge&logo=github)" (https://github.com/TanvirCodeStorm)

Building ideas into real-world projects, one line of code at a time. ⚡

</div>---

⭐ Support the Project

If this project helps you learn robotics:

- ⭐ Star the repository.
- 🍴 Fork it and experiment.
- 🛠️ Improve the design.
- 📢 Share your build with other makers.

---

<div align="center">⚡ CODE. CONNECT. DRIVE. ⚡

ESP32 × L298N × Dabble

Made with curiosity and a passion for robotics. 🤖

</div>