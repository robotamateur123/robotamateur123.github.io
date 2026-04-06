---
title: "Video 2: DIY home security alarm with Arduino | PIR sensor (HC-SR501), buzzer, LED"
date: 2024-04-15
description: "Motion-triggered alarm with PIR HC-SR501, buzzer, and LED — wiring diagrams, PDF, and full Arduino code."
toc: true
params:
  youtube: "5YpVYsDrbb0"
aliases:
  - /play-with-arduino/video-2-diy-home-security-alarm-with-arduino-copy/
---

## Understanding PIR Sensor (HC-SR501)

In this project, you'll learn how to build a **DIY home security alarm** using the **HC-SR501 PIR motion sensor**, **Arduino**, **buzzer**, and **LED**. We'll cover how the PIR sensor works, how to test it in standalone mode, adjust its sensitivity and timing, and finally integrate it into a complete alarm system.

Perfect for beginners, this hands-on project teaches practical electronics and coding with Arduino.

By the end, you'll:
- Understand how the HC-SR501 detects motion
- Wire and configure the components correctly
- Upload and run the Arduino code for a real motion-triggered alarm

Includes full **wiring diagrams**, **source code**, and recommended **hardware links**.

## Watch the Video
{{< youtube-responsive id="5YpVYsDrbb0" >}}

## Resources
### Hardware Purchase Links 
1. PIR sensor
2. Arduino UNO kit

### Wiring Diagram
![standalone_test_wiring_diagram](/play-with-arduino/images/standalone_test_wiring_diagram.png)
![home_security_alarm_test_wiring_diagram](/play-with-arduino/images/home_security_alarm_test_wiring_diagram.png)

👉 [Download Wiring Diagram PDF](/play-with-arduino/pdf/vid2-wiring_diagrams.pdf)

### Source Code
```cpp
// Define the pin numbers for the components
int BUZZ_PIN = 9;  // Pin number for the buzzer
int PIR_PIN = 3;   // Pin number for the PIR sensor
int LED_PIN = 5;   // Pin number for the LED

int pirState;  // Variable to hold the state of the PIR sensor

void setup() {
  // Set the pinMode for each pin
  pinMode(PIR_PIN, INPUT);   // PIR_PIN is set as an input for the sensor
  pinMode(BUZZ_PIN, OUTPUT); // BUZZ_PIN is set as an output for the buzzer
  pinMode(LED_PIN, OUTPUT);  // LED_PIN is set as an output for the LED
}

void loop() {
  // Continuously check the state of the PIR sensor
  pirState = digitalRead(PIR_PIN); // Read the state of the PIR sensor and store it

  // If the PIR sensor detects motion (HIGH state), activate buzzer and LED
  if(pirState == HIGH){
    digitalWrite(BUZZ_PIN, HIGH); // Turn on the buzzer
    digitalWrite(LED_PIN, HIGH);  // Turn on the LED
  }
  // If no motion is detected (LOW state), turn off buzzer and LED
  else{
    digitalWrite(BUZZ_PIN, LOW); // Turn off the buzzer
    digitalWrite(LED_PIN, LOW);  // Turn off the LED
  }
}
```

