# Vision-Based Gesture-Controlled Pneumatic System

## Project Overview

This project implements a **vision-based, touch-free pneumatic control system** using real-time hand gesture recognition. A webcam captures hand movements, and computer vision algorithms identify the number of raised fingers to control LED indicators and a pneumatic cylinder through an Arduino Uno.

The system integrates computer vision, embedded systems, relay-based switching, and pneumatic actuation to demonstrate a human–machine interface for industrial automation.

## Features

- Real-time hand detection and tracking using a webcam.
- Finger counting using OpenCV and CVZone.
- Five LED indicators corresponding to the number of raised fingers.
- Gesture-based pneumatic cylinder actuation.
- Arduino Uno communication using PyFirmata.
- Touch-free control for pneumatic automation.

## Hardware Requirements

- Arduino Uno
- Webcam
- 5 LEDs with suitable current-limiting resistors
- Relay module
- Pneumatic solenoid valve with spring-return mechanism
- Pneumatic cylinder
- Pneumatic air supply and tubing
- Connecting wires and power supply

## Software Requirements

- Python 3.x
- OpenCV
- CVZone
- PyFirmata
- Arduino IDE
- Arduino StandardFirmata firmware

## System Architecture

```text
Webcam
   |
   v
Hand Detection and Tracking
(OpenCV + CVZone)
   |
   v
Finger Count Recognition
   |
   v
Python Control Program
   |
   v
PyFirmata Communication
   |
   v
Arduino Uno
   |
   +----> LED Indicators (Pins 8–12)
   |
   +----> Relay Module (Pin 7)
                 |
                 v
          Solenoid Valve
                 |
                 v
          Pneumatic Cylinder
```

## Working Principle

1. The webcam captures live video of the user's hand.
2. CVZone detects and tracks the hand, identifying which fingers are raised.
3. Python calculates the total number of raised fingers.
4. The Arduino controls five LEDs according to the detected finger count.
5. When all five fingers are raised, the relay is activated to command pneumatic cylinder extension.
6. When a closed fist is detected, the relay is deactivated, allowing the spring-return valve to command cylinder retraction.

**LED indication:**

| Raised fingers | LED indication | Pneumatic control |
|---|---|---|
| 0 | All LEDs OFF | Relay OFF |
| 1 | LED 1 ON | No change |
| 2 | LEDs 1–2 ON | No change |
| 3 | LEDs 1–3 ON | No change |
| 4 | LEDs 1–4 ON | No change |
| 5 | All LEDs ON | Relay ON |

*Note: When no hand is detected, the program turns all LEDs OFF and sets the relay OFF.*

## Pin Configuration

| Arduino digital pin | Connected component |
|---|---|
| D7 | Relay module |
| D8 | LED 1 |
| D9 | LED 2 |
| D10 | LED 3 |
| D11 | LED 4 |
| D12 | LED 5 |

## Installation and Setup

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

### 2. Install Python Dependencies

```bash
pip install opencv-python cvzone pyfirmata
```

### 3. Configure Arduino

1. Connect the Arduino Uno to your computer.
2. Open the Arduino IDE.
3. Navigate to **File → Examples → Firmata → StandardFirmata**.
4. Upload the StandardFirmata sketch to the Arduino Uno.
5. Identify the correct serial port from the Arduino IDE.

### 4. Configure the COM Port

In `controller.py`, update the serial port to match your Arduino connection.

```python
comport = 'COM8'
```

Replace `COM8` with your actual port if different.

### 5. Run the Application

Run the main Python script:

```bash
python main.py
```

Ensure the webcam is connected and the Arduino is powered before starting the application.

### 6. Stop the Application

Press **K** while the camera window is active to stop the program and close the camera.

## Project Structure

```text
Vision-Based-Gesture-Controlled-Pneumatic-System/
│
├── main.py
├── controller.py
├── README.md
└── requirements.txt
```

- `main.py` — Captures webcam frames, detects hand gestures, and sends commands to the controller.
- `controller.py` — Controls the LED indicators and relay through Arduino using PyFirmata.
- `requirements.txt` — Lists the required Python libraries.
- `README.md` — Documents the project and setup instructions.

## Applications

- Touch-free industrial machine control.
- Pneumatic pick-and-place systems.
- Human–machine interfaces.
- Educational demonstrations of computer vision and automation.
- Gesture-based control of electromechanical systems.

## Future Improvements

- Add additional gestures for different pneumatic operations.
- Integrate multiple cylinders for sequential actuation.
- Improve reliability under varying lighting conditions.
- Add emergency-stop and fault-detection mechanisms.
- Implement a more robust communication and safety-monitoring system.

## Safety Considerations

Use an appropriately rated relay or driver for the solenoid valve. Verify the valve's normal state, relay logic, and pneumatic connections before operation. Provide suitable pressure regulation, mechanical guarding, and an independent emergency-stop system. A closed-fist gesture or loss of camera detection should not be treated as a safety-rated emergency stop.

## Author

**Albert**

Mechatronics Engineering | Robotics and Automation

