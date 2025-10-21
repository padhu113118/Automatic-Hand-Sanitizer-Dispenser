# Automatic Hand Sanitizer Dispenser 🤖🧴

A touchless, automatic hand sanitizer dispenser built using an Arduino Uno, an ultrasonic sensor, and a servo motor. This project is perfect for promoting hygiene and serves as a great introduction to Arduino-based automation.

![Automatic Hand Sanitizer Dispenser](https://img.youtube.com/vi/Ax6P93r32KU/0.jpg)


---

## 📋 Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
- [Components Required](#components-required)
- [Circuit Diagram / Wiring](#circuit-diagram--wiring)
- [Installation & Setup](#installation--setup)
- [Code Explanation](#code-explanation)
- [Enclosure & Assembly](#enclosure--assembly)
- [Troubleshooting](#troubleshooting)
- [Future Improvements](#future-improvements)
- [License](#license)

---

## 🧠 Overview

This project automates a standard liquid hand sanitizer bottle by using an ultrasonic sensor to detect the presence of a hand. When a hand is detected within a specific range, the Arduino commands a servo motor to press the pump lever, dispensing a precise amount of sanitizer without any physical contact.

**Key Features:**
- **Touchless Operation:** Enhances hygiene by eliminating surface contact.
- **Adjustable Sensitivity:** Easily change the detection range in the code.
- **Low Power Consumption:** Can be powered by a 9V battery or USB adapter.
- **Customizable:** Code and mechanism can be adapted for different dispensers.

---

## ⚙️ How It Works

1.  The HC-SR04 Ultrasonic Sensor continuously emits ultrasonic waves and listens for their echo.
2.  The Arduino calculates the distance to the nearest object based on the time it takes for the echo to return.
3.  If the calculated distance is less than a predefined threshold (e.g., 10 cm), the Arduino interprets this as a hand being present.
4.  The Arduino then sends a signal to the SG90 Servo Motor, making it rotate to a specific angle to press down the sanitizer pump.
5.  After a short delay (to allow the sanitizer to be dispensed), the servo returns to its original position, ready for the next use.

---

## 📦 Components Required

| Component | Quantity | Description |
| :--- | :--- | :--- |
| **Arduino Uno** | 1 | The brain of the project. |
| **HC-SR04** | 1 | Ultrasonic Distance Sensor for hand detection. |
| **SG90 Micro Servo** | 1 | Motor to actuate the pump lever. |
| **Jumper Wires** | Several | For making connections. |
| **Breadboard** | 1 | For prototyping the circuit. |
| **USB Cable** | 1 | To upload code and power the Arduino. |
| **Hand Sanitizer Bottle** | 1 | Standard pump-action bottle. |
| **Enclosure** | 1 | A box or 3D-printed case to house the components. |

---

## 🔌 Circuit Diagram / Wiring

Connect the components as follows:

| Arduino Uno Pin | HC-SR04 | SG90 Servo |
| :--- | :--- | :--- |
| `5V` | `VCC` | `RED (VCC)` |
| `GND` | `GND` | `BROWN (GND)` |
| `Digital Pin 9` | `Trig` | -- |
| `Digital Pin 10` | `Echo` | -- |
| `Digital Pin 6` | -- | `ORANGE (Signal)` |

*(A visual diagram can be created using Fritzing or similar software and uploaded to your repository as `wiring_diagram.png`)*

---

## 🛠️ Installation & Setup

1.  **Assemble the Circuit:** Connect all the components as per the wiring table above.
2.  **Connect to Computer:** Plug the Arduino into your computer using the USB cable.
3.  **Upload the Code:**
    - Open the Arduino IDE.
    - Copy the code from the `automatic_sanitizer.ino` file (below) into a new sketch.
    - Select the correct board (**Tools > Board > Arduino Uno**) and port (**Tools > Port**).
    - Click the **Upload** button.

---

## 💻 Code Explanation

Here is the core Arduino code for the project:

```cpp
// Automatic Hand Sanitizer Dispenser Code
#include <Servo.h> // Include the Servo library

// Define pin connections
const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 6;

// Define variables and constants
long duration;
int distance;
int sanitizeDistance = 10; // Detection range in cm

Servo myServo; // Create a servo object

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin); // Attaches the servo on pin 6 to the servo object
  myServo.write(0); // Ensure servo starts at 0 degrees
  delay(1000); // Give the servo time to reach the position
}

void loop() {
  // Clear the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  // Set the trigPin HIGH for 10 microseconds to send the pulse
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance (in cm)
  distance = duration * 0.034 / 2;

  // Check if the distance is within the sanitizing range
  if (distance <= sanitizeDistance) {
    dispenseSanitizer();
  }
}

void dispenseSanitizer() {
  myServo.write(90); // Rotate servo to 90 degrees to press the pump
  delay(500);        // Hold it down for 0.5 seconds
  myServo.write(0);  // Return servo to original position
  delay(3000);       // Wait 3 seconds before next detection to avoid multiple triggers
}
