Here's a clean, professional `README.md` you can directly paste into your GitHub repo for the EMG-controlled multi-servo project:

---

# 💪 EMG-Controlled Robotic Fingers using Raspberry Pi Pico & SG90 Servos

## Overview

This project demonstrates **EMG signal-based control of robotic fingers** using the Raspberry Pi Pico and SG90 servo motors. It detects muscle flex and double-flex gestures via an EMG sensor and maps these to corresponding servo motions — simulating lifelike robotic hand movement.

---

## 🎯 Features

* **EMG Signal Processing**

  * Reads analog muscle signals from an EMG sensor
  * Applies **RMS filtering** over a buffer for stability
  * Classifies gestures into:

    * `relax` – hand open
    * `flex` – grip
    * `double flex` – wave motion

* **Servo Control**

  * Controls **3 SG90 servos**
  * Implements **natural phase offset** between finger motions
  * Modular `moveServo()` and `moveAllServos()` functions for scalability

* **Non-Blocking Execution**

  * Uses `Timer` interrupts for EMG sampling (non-blocking control)
  * Keeps main thread free for future expansion (e.g., I2C comms, GUI logging)

---

## 🧠 EMG Gesture Mapping

| Gesture     | Detected Pattern | Action                |
| ----------- | ---------------- | --------------------- |
| Relax       | Low RMS (< 3000) | Open all fingers      |
| Flex        | RMS > 3000       | Close all fingers     |
| Double Flex | RMS > 8000       | Perform waving motion |

---

## 📦 Hardware Used

* **Microcontroller:** Raspberry Pi Pico
* **Servos:** 3 × SG90 servo motors
* **Sensor:** MyoWare-style EMG sensor
* **Power:** External 5V regulated supply (for stable servo control)
* **Connections:**

  * EMG Signal → GPIO26
  * Servos → GPIO15, 14, 13
  * EMG V+ → `VBUS` (5V from USB/external)
  * GND lines tied together



## 🧰 MicroPython Code Summary

```python
- read_u16()        → EMG ADC reading
- computeRMS()      → Smooths muscle signal (10-sample buffer)
- classifyGesture() → Interprets RMS to flex/double-flex/relax
- moveServo()       → Maps angle to SG90 duty cycle
- moveAllServos()   → Moves all servos with phase delay
- emg_callback()    → Timer-based EMG sampling & gesture handling
```



## 📈 Improvements Implemented

✔ Modular functions (`moveServo()`, `readEMG()`)
✔ RMS filtering for stability
✔ Non-blocking loop using `Timer()`
✔ Realistic motion using phase offsets
✔ Multi-gesture recognition (`flex`, `double_flex`)
✔ Abstraction using servo arrays








