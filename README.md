# Smart Shopping Cart with Color Following and QR-Based Automatic Billing

## Overview
This project implements a **Smart Shopping Cart** that automatically follows a user and performs **automatic billing using QR code scanning**. The cart uses computer vision to track a colored object carried by the user and moves autonomously using DC motors.

Products are scanned using QR codes. The scanned product information is processed, and the total bill is updated in real time and displayed on an LCD screen.

The system integrates **Raspberry Pi, Arduino, computer vision, motor control, and QR code processing** to create an automated retail shopping solution.

---

# System Features

### Autonomous User Following
The cart follows the user using **color-based object tracking** implemented using OpenCV.

### QR Code Product Scanning
Products are scanned using a camera and decoded using a QR detection library.

### Automatic Billing
Scanned items are added to a cart list and the total price is calculated automatically.

### Real-Time Price Display
Item information and total cost are displayed on an LCD connected to Arduino.

### Motor Control
The cart movement is controlled using **two DC motors and an L298N motor driver**.

---

# System Architecture

The system is divided into two major subsystems:

### 1. Navigation System
- Raspberry Pi camera detects the user.
- OpenCV processes the image to track a specific color.
- Based on the object's position in the frame, motor speeds are adjusted.
- The cart maintains a safe distance from the user.

### 2. Billing System
- A camera scans QR codes on products.
- Product name and price are extracted.
- Data is sent to Arduino.
- LCD displays scanned items and total bill.

---

# Hardware Components

| Component | Quantity |
|----------|----------|
| Raspberry Pi | 1 |
| Arduino Uno | 1 |
| ESP32-CAM | 1 |
| L298N Motor Driver | 1 |
| DC Motors | 2 |
| LCD Display (20x4) | 1 |
| Potentiometer | 1 |
| Camera / Webcam | 1 |
| Wheels | 4 |
| Power Bank | 1 |
| External Power Supply | 1 |

---

# Hardware Connections

## ESP32-CAM to Arduino

ESP32-CAM communicates with Arduino through serial communication.

### Connections
| ESP32-CAM | Arduino |
|----------|---------|
| TX | RX |
| RX | TX |
| GND | GND |

---

## LCD Display to Arduino

The LCD display shows scanned products and total bill.

### Connections

| LCD Pin | Arduino |
|-------|-------|
| VSS | GND |
| VDD | 5V |
| VO | Potentiometer |
| RS | Digital Pin |
| E | Digital Pin |
| D4-D7 | Digital Pins |

---

## Motor Driver Connections

The **L298N motor driver** controls two DC motors.

### Connections

| L298N Pin | Raspberry Pi |
|----------|--------------|
| IN1 | GPIO 24 |
| IN2 | GPIO 23 |
| IN3 | GPIO 17 |
| IN4 | GPIO 27 |
| ENA | GPIO 25 |
| ENB | GPIO 22 |

Motors are powered using an **external 11V supply**.

---

# Circuit Diagrams

## ESP32-CAM and Arduino Setup

![ESP32 CAM Setup](ESP32_CAM_SETUP.jpeg)

---

## LCD Display Wiring

![LCD Setup](LCD_DISPLAY_SETUP.jpeg)

---

## Robot Hardware Architecture

![Robot System](colour_following_robot.png)

---

# Software Architecture

The system uses two main Python programs:

### 1. Color Following Robot
This program runs on the Raspberry Pi and controls robot movement.

Main tasks:
- Capture camera frames
- Detect colored object
- Calculate object position
- Control motors based on position

Key libraries used:
- OpenCV
- NumPy
- RPi.GPIO

Motor speed is adjusted based on:
- Object position in frame
- Estimated distance from the object

---

### 2. QR Billing System

The QR billing system scans product QR codes and extracts product information.

Main tasks:
- Capture frames from IP camera
- Decode QR codes
- Extract product name and price
- Update shopping cart
- Send data to Arduino

Libraries used:
- OpenCV
- Pyzbar
- BeautifulSoup
- Serial communication

---

# Installation

## 1. Install Required Packages

```bash
pip install opencv-python
pip install numpy
pip install pyzbar
pip install beautifulsoup4
pip install pillow
pip install pyserial
