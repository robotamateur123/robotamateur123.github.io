---
title: "Video 4: DIY Cheap Home Security Alarm For Beginners | Arduino Nano, PIR sensors, and SIM800L"
toc: true
---

## Summary
In this beginner-friendly tutorial, we show you how to build a DIY cheap home security alarm using an Arduino Nano, PIR sensors, and a SIM800L module. The alarm detects motion and calls you when triggered. The video covers wiring diagrams, enclosure design with Onshape, assembly, Arduino code explanation, and troubleshooting tips for the SIM800L module. Downloadable resources and a detailed list of affordable hardware components are provided.

## Watch the Video
{{< youtube-responsive id="5QtXKAlHNS8" query="si=3MNu42FTqhahRUVC" >}}

## Resources

### Hardware Purchase Links
- Arduino Nano: [AliExpress](https://a.aliexpress.com/_EHjKvCZ)
- SIM800L Module: [AliExpress](https://a.aliexpress.com/_Eupg3dF)
- PIR Sensor: [AliExpress](https://a.aliexpress.com/_EGOVSGd)
- SIM Card: Approx. $2 (local purchase)
- Prototyping Board (4cm x 6cm): [AliExpress](https://a.aliexpress.com/_EIoGoC9)
- Power Cables (for SIM800L and Arduino Nano): Approx. $2 each
- 10k Ohm Resistors Kit: [AliExpress](https://a.aliexpress.com/_EG9fLN3)
- Wires: [AliExpress](https://a.aliexpress.com/_EGtZok9)
- 3D Printing Filament: Approx. $2
- Screws Set: [AliExpress](https://a.aliexpress.com/_EjIcJhx)
- Soldering Pins: [AliExpress](https://a.aliexpress.com/_EGzSjrr)
- Jumper Wires: [AliExpress](https://a.aliexpress.com/_Ezvyai1)

### Wiring Diagram

**Soldering Diagram**  
![vid4-soldering_diagram](/play-with-arduino/images/vid4-soldering_diagram.jpg)

**Wiring Diagram with LED**  
![vid4-wiring_diagram_with_LED](/play-with-arduino/images/vid4-wiring_diagram_with_LED.jpg)

**Wiring Diagram without LED**  
![vid4-wiring_diagram_without_LED](/play-with-arduino/images/vid4-wiring_diagram_without_LED.jpg)


### Enclosure Design
Download here: [Onshape Enclosure Design Folder](https://drive.google.com/drive/folders/1oOsKck_TNGyfORTsG8uyVFidPvIZxPSW?usp=drive_link)

### Source Code
```cpp
#include <SoftwareSerial.h>

// Define the pin numbers for the components
int PIR_PIN = 3;   // Pin number for the PIR sensor
int LED_PIN = 5;   // Pin number for the LED

int pirState;  // Variable to hold the state of the PIR sensor
bool callMade = false; // Flag to track if call has been made

//Create software serial object to communicate with SIM800L
SoftwareSerial sim800l(11, 10); //SIM800L Tx & Rx is connected to Arduino #11 & #10

void setup() {
  // Set the pinMode for each pin
  pinMode(PIR_PIN, INPUT);   // PIR_PIN is set as an input for the sensor
  pinMode(LED_PIN, OUTPUT);  // LED_PIN is set as an output for the LED

  //Begin serial communication with Arduino and Arduino IDE (Serial Monitor)
  Serial.begin(9600);
  
  //Begin serial communication with Arduino and SIM800L
  sim800l.begin(9600);

  Serial.println("Initializing..."); 
  pirState = digitalRead(PIR_PIN);
  if(pirState == HIGH){
    Serial.println("pirState init: 1"); 
  }
  delay(60000);

  sim800l.println("AT"); //Once the handshake test is successful, it will back to OK
  updateSerial();
  sim800l.println("AT+CSQ"); //Signal quality test, value range is 0-31 , 31 is the best
  updateSerial();
  sim800l.println("AT+CCID"); //Read SIM information to confirm whether the SIM is plugged
  updateSerial();
  sim800l.println("AT+CREG?"); //Check whether it has registered in the network
  updateSerial();
}

void loop() {
  // Continuously check the state of the PIR sensor
  pirState = digitalRead(PIR_PIN); // Read the state of the PIR sensor and store it
  
  // If the PIR sensor detects motion (HIGH state), activate LED and make a call
  if(pirState == HIGH && !callMade){
    Serial.println("pirState 1"); 
    digitalWrite(LED_PIN, HIGH);  // Turn on the LED

    Serial.println("Calling ..."); 
    sim800l.println("AT"); //Once the handshake test is successful, it will back to OK
    updateSerial();
    sim800l.println("ATD+ +ZZxxxxxxxxxxx;"); //  change ZZ with country code and xxxxxxxxxxx with phone number to dial
    updateSerial();
    delay(20000); // wait for 20 seconds...
    sim800l.println("ATH"); //hang up
    updateSerial();

    callMade = true; // Set flag to true indicating call has been made
    delay(5000); // Wait for 5 seconds before checking PIR sensor again
  }

  // Reset call flag if no motion is detected
  if(pirState == LOW){
    // Serial.println("pirState 00000000"); 
    callMade = false;
    digitalWrite(LED_PIN, LOW);  // Turn off the LED
  }
}

void updateSerial() {
  delay(500);
  while (Serial.available()) {
    sim800l.write(Serial.read());//Forward what Serial received to Software Serial Port
  }
  while(sim800l.available()) {
    Serial.write(sim800l.read());//Forward what Software Serial received to Serial Port
  }
} 
```
