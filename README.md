Smart Glove for Sign-to-Speech Conversion

A wearable assistive communication prototype that detects predefined hand gestures using flex sensors and an Arduino Uno, then converts the recognized gestures into spoken words using Python.

Overview

The project was developed to explore a low-cost way of converting hand gestures into audible speech. The implemented prototype uses three flex sensors to detect finger bending, adaptive calibration to account for the user's baseline sensor values, and rule-based gesture recognition.

A key idea behind the project was to go beyond simple gesture-to-speech conversion. We explored the concept of emotion-aware voice modulation, where the tone and delivery of the generated speech could be varied according to the context or emotion associated with a gesture. The current prototype focuses on the base gesture-to-speech system, while emotion-aware modulation remains a proposed extension and future direction.

Key Features

3-flex-sensor gesture recognition

Adaptive user-specific calibration

Sensor averaging for smoother readings

Rule-based recognition of 7 predefined gestures

Arduino-to-Python serial communication

Python text-to-speech output

Duplicate-speech prevention

Proposed emotion-aware voice modulation concept

Gesture Mapping

Finger Pattern

Output

Index

HELLO

Middle

YES

Ring

HELP

Index + Middle

THANK YOU

Index + Ring

FOOD

Middle + Ring

WATER

Index + Middle + Ring

EMERGENCY

System Workflow

Hand Gesture
      ↓
Flex Sensors
      ↓
Voltage Divider Circuit
      ↓
Arduino Analog Inputs
      ↓
Sensor Averaging
      ↓
Adaptive Calibration
      ↓
Rule-Based Gesture Recognition
      ↓
Serial Communication
      ↓
Python
      ↓
Text-to-Speech
      ↓
Spoken Output

How It Works

1. Flex Sensor Input

Flex sensors are placed so that finger bending changes their resistance. Each sensor is connected as part of a voltage-divider circuit.

2. Analog Reading

The Arduino reads the sensors through:

A1 → Index finger
A2 → Middle finger
A3 → Ring finger

3. Sensor Smoothing

The Arduino takes 15 analog readings for each sensor and calculates their average to reduce small fluctuations.

4. Adaptive Calibration

During startup, the user keeps the monitored fingers straight. The Arduino records baseline values and derives individual thresholds:

Index threshold  = Index base  - 25
Middle threshold = Middle base - 18
Ring threshold   = Ring base   - 25

A finger is considered bent when its averaged value falls below its threshold.

5. Gesture Recognition

The combination of bent and straight fingers is matched to one of seven predefined gestures using rule-based conditions.

6. Serial Communication

The Arduino sends recognized gesture labels through serial communication at 9600 baud.

7. Text-to-Speech

Python receives the labels using PySerial and uses pyttsx3 to convert valid gestures into spoken output.

Speech generation runs in a separate thread so the serial-processing loop remains responsive.

Hardware

Arduino Uno

3 Flex Sensors

10kΩ resistors

Breadboard

Glove

Connecting wires

Add your circuit image as:

hardware/circuit_diagram.png

Then the README will display it with:



Software

Arduino IDE

Embedded C/C++

Python

PySerial

pyttsx3

Project Structure

Smart-Glove-Sign-to-Speech/
│
├── README.md
├── requirements.txt
│
├── arduino/
│   └── smart_glove.ino
│
├── python/
│   └── speech_output.py
│
├── hardware/
│   └── circuit_diagram.png
│
└── demo/
    └── demo_video.mp4

Setup

Arduino

Open arduino/smart_glove.ino in Arduino IDE.

Connect the flex sensors according to the circuit.

Connect the Arduino Uno.

Select the correct board and COM port.

Upload the code.

Open Serial Monitor at 9600 baud.

During startup calibration, keep the monitored fingers straight and still.

Python

Install the required packages:

pip install -r requirements.txt

Change the COM port in python/speech_output.py if required:

arduino = serial.Serial("COM3", 9600)

Run:

python python/speech_output.py

Demo

Add your demonstration video as:

demo/demo_video.mp4

The demo shows the prototype recognizing predefined gestures and converting them into spoken output.

Innovation: Emotion-Aware Voice Modulation

The main innovative direction of the project was to move beyond simple gesture-to-word conversion.

The proposed extension is:

Recognized Gesture
        ↓
Context / Emotion
        ↓
Emotion Mapping
        ↓
Tone / Pitch / Rate Selection
        ↓
More Expressive Speech

For example:

Normal communication → Neutral delivery
Positive interaction → Happier delivery
Emergency → Urgent delivery

The current prototype does not claim a complete emotion-recognition or voice-modulation implementation. This remains the main proposed extension and future direction of the project.

Results

The implemented prototype demonstrates:

Adaptive calibration of flex-sensor readings

Detection of predefined finger-bending patterns

Recognition of 7 gesture outputs

Real-time Arduino-to-Python communication

Text-to-speech conversion of recognized gestures

Future Scope

Expand the gesture vocabulary

Support complete sign-language phrases

Add more flex sensors

Integrate hand-orientation sensing

Add wireless communication

Explore machine-learning-based gesture recognition

Implement emotion-aware voice modulation

Support multiple languages

Develop a more compact standalone wearable system

Learning Outcomes

This project provided practical experience with:

Flex sensors

Voltage-divider circuits

Analog sensor readings

ADC-based data acquisition

Adaptive thresholding

Sensor smoothing

Rule-based classification

Embedded programming

Serial communication

Python

Text-to-speech

Hardware-software integration

Conclusion

The Smart Glove demonstrates a low-cost approach to converting predefined hand gestures into spoken words. The project combines wearable sensing, embedded processing, serial communication, and software-based speech generation.

Beyond basic translation, the project explores making assistive communication more expressive through emotion-aware voice modulation, providing a foundation for future development toward more natural and context-aware sign-to-speech systems.
