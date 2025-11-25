📡 Arduino Radar System with Processing

A real-time Radar/Sonar visualization system that maps the environment using an Ultrasonic sensor and displays objects on a radar screen via Processing.

📖 Table of Contents

Overview

Components Required

Circuit Diagram

Installation

How it Works

Troubleshooting

🧐 Overview

This project integrates an Arduino UNO with a Processing interface. The Arduino sweeps a servo motor from 15° to 165°, measuring distance at every degree using an HC-SR04 ultrasonic sensor. This data is transmitted serially to a PC, where a Processing sketch renders a classic green radar sweep, plotting objects in red when detected within range (40cm).

📋 Components Required

Component

Quantity

Description

Arduino UNO

1

Main microcontroller

HC-SR04

1

Ultrasonic Distance Sensor

Servo Motor

1

SG90 Micro Servo (or similar)

Breadboard

1

For prototyping

Jumper Wires

~10

Male-to-Male connections

USB Cable

1

Type A to B (for Arduino)

🔌 Circuit Diagram & Connections

1. Servo Motor

Red Wire: +5V

Brown/Black Wire: GND

Orange/Signal Wire: Pin 12

2. HC-SR04 Ultrasonic Sensor

VCC: +5V

GND: GND

Trig: Pin 10

Echo: Pin 11

⚠️ Important: Use the breadboard rails to share the single 5V and GND pins from the Arduino between both the Servo and the Sensor.

🛠️ Installation Step-by-Step

Step 1: Hardware Assembly

Mounting: Secure the Ultrasonic Sensor onto the Servo motor horn using electrical tape, hot glue, or a 3D-printed bracket.

Base: Fix the Servo motor to a stationary base so only the horn (and sensor) rotates.

Wiring: Connect all components according to the Circuit Diagram.

Step 2: Flash the Arduino

Open the Arduino IDE.

Load the file radar_arduino.ino.

Connect your Arduino UNO to the PC.

Select the correct Board and Port in Tools.

Click Upload.

Verify: Open Serial Monitor (9600 baud). You should see data streaming: 15,10., 16,10., etc.

Close the Serial Monitor before proceeding to the next step.

Step 3: Run the Visualization

Download and install Processing 4.

Open the file radar_processing.pde.

Configuring the Port:

The script attempts to use the first available serial port (Serial.list()[0]).

If the app crashes or doesn't show data, edit the setup() function:

// Change the index [0] to [1] or [2], or use the explicit name "COM3"
myPort = new Serial(this, Serial.list()[0], 9600);


Press the Run (Play) button.

🖥️ How it Works

The system operates on a synchronous loop:

Sweep: Arduino rotates the servo 1 degree at a time.

Ping: It triggers the ultrasonic sensor to measure distance.

Transmit: Data is sent over Serial in the format Angle,Distance..

Visualize: Processing reads the string up to the . delimiter, parses the angle and distance, and draws the graphics:

Green Fade: Represents the history/trail of the scan.

Red Lines: Represent detected objects within the alert zone (default < 40cm).

❓ Troubleshooting

Issue: "Error opening serial port..."

Make sure the Arduino Serial Monitor is closed.

Check which COM port your Arduino is connected to in Device Manager and update the index in the Processing code.

Issue: Servo jitters or Arduino resets

This is often a power issue. Try powering the Servo with an external 5V power supply (connect the grounds together) if the USB power isn't sufficient.

Issue: Radar shows "Out of Range" constantly

Check the wiring of the Echo and Trig pins.

Ensure the object is hard/flat enough to reflect sound waves.

Created for the Arduino Radar Project.
