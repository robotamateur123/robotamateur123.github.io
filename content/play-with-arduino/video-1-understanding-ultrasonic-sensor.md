---
title: "Video 1: Understanding Ultrasonic Sensor"
toc: true
---
## Understanding Ultrasonic Sensor (HC-SR04)

Ultrasonic sensors measure distance using sound waves. The HC-SR04 is a common module that works by sending an ultrasonic pulse and timing how long it takes to reflect back.

📖 Learn more in the full blog: [Medium Article](https://medium.com/@robotamateur123/understanding-ultrasonic-sensor-e3791f883061)

## Watch the Video
{{< youtube-responsive id="hqQZ0IiPRmo" >}}

## Ressources
### Hardware Purchase Links 
1. Ultrasonic sensor
2. Arduino UNO kit

### Source Code
```cpp
#include <NewPing.h>
#define TRIGGER_PIN 9 // Arduino pin tied to trigger pin on the ultrasonic sensor.
#define ECHO_PIN 8 // Arduino pin tied to echo pin on the ultrasonic sensor.
#define MAX_DISTANCE 200 // Maximum distance we want to ping for (in centimeters). Maximum sensor distance is rated at 400–500cm.
NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE); // 
// NewPing setup of pins and maximum distance.

void setup() {
 Serial.begin(9600); // Open serial monitor at 9600 baud to see ping results.
}

void loop() {
 delay(50); // Wait 50ms between pings (about 20 pings/sec). 29ms should be the shortest delay between pings.
 Serial.print("Distance = ");
 Serial.print(sonar.ping_cm()); // Send ping, get distance in cm. (0 = outside set distance range, no ping echo)
 Serial.println(" cm");
}
```

