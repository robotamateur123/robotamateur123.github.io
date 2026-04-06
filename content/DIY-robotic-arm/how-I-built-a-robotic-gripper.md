---
title: "Video 1 - I built a simple 3D-Printed Robot Gripper w/ Raspberry Pi (Beginner Friendly!)"
date: 2026-04-06
description: "Robotic gripper build materials — resources and video links; Wiring diagram and code."
draft: false
cover:
  image: "/diy-robotic-arm/images/gripper-thumb.svg"
  alt: "Robotic gripper project placeholder illustration"
---

## Resources

- 🔌 Wiring diagram: [Open full image](/diy-robotic-arm/images/Vid5-WiringDiagram.png) 
- 💾 Code: see **Source code** below.
- 📹 [Watch on YouTube](https://www.youtube.com/@robotamateur123/videos)

### Wiring diagram

![Raspberry Pi, PCA9685 breakout, and servo wiring](/diy-robotic-arm/images/Vid5-WiringDiagram.png)

### Source code

```python
import time
from adafruit_servokit import ServoKit
kit = ServoKit(channels=16)

gripper = 0

# pulse_width_range sets the min and max range of the servo: where the servo actually goes to
# these values will determine where the servo 0 degrees starts
kit.servo[gripper].set_pulse_width_range(1000, 2000)

# note that the angle is wrt to actuation_range, not the absolute angle!!!
kit.servo[gripper].actuation_range = 90

for i in range(1):
    kit.servo[gripper].angle = 0
    time.sleep(2.0)
    print("Cmd 0: ", kit.servo[gripper].angle)

    kit.servo[gripper].angle = 45
    time.sleep(2.0)
    print("Cmd 90: ", kit.servo[gripper].angle)
```
