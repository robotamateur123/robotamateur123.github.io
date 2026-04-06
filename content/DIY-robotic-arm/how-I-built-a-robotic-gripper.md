---
title: "Video 1 - I built a simple 3D-Printed Robot Gripper with Raspberry Pi (Beginner Friendly!)"
date: 2026-04-06
description: "Robotic gripper build materials — resources and video links; Wiring diagram and code."
draft: false
params:
  youtube: "c-ZyGVxRe7U"
---

## Resources

- 🔌 Wiring diagram: [Open full image](/diy-robotic-arm/images/Vid5-WiringDiagram.png)
- 🧩 **3D-printed parts (CAD / STL):**
  - [Onshape — open in browser, then right-click a part → **Export**](https://cad.onshape.com/documents/a982843b6e5d3aab64560b76/w/64c56c1cb32ccc51f182beda/e/5062ba00eacdf3958d4a41df?renderMode=0&uiState=69d3b85381f4fa9bdad34fce)
  - [Google Drive — direct download (folder)](https://drive.google.com/drive/folders/1kBx7XS37JYXXpA-7wwmAKh1xhRelPrf9?usp=sharing)
- 💾 Code: see **Source code** below.
- 📹 [Watch on YouTube](https://youtu.be/c-ZyGVxRe7U)

## Watch the Video

{{< youtube-responsive id="c-ZyGVxRe7U" >}}

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
