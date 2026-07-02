# Hybrid Voice and Vision Automation System

## Overview

A sophisticated automation system built on Raspberry Pi 4 that intelligently bridges AI-powered computer vision with voice control for seamless home automation.

**Key Innovation**: Combines OpenCV's real-time light sensing with Google Speech Recognition, allowing the system to operate autonomously OR respond to voice commands — giving you complete control.

---

## What It Does

### 📹 Auto Mode (Vision-Based)
- Uses your USB webcam as an intelligent light sensor
- Continuously analyzes ambient brightness
- When room lights turn off → LED turns ON instantly
- When room lights turn on → LED turns OFF automatically
- Runs silently in the background

### 🎤 Manual Mode (Voice-Based)
- Say **"Turn on"** → LED activates immediately
- Say **"Turn off"** → LED deactivates immediately
- Say **"Auto"** → System returns to camera control
- Overrides the camera completely while active

---

## What You Need to Build This

### Hardware
- **Raspberry Pi 4** (2GB+ recommended)
- **USB Webcam** with built-in microphone
- **LED** (any color)
- **220Ω or 330Ω resistor** (current limiting)
- **Breadboard** and jumper wires
- **5V power supply** for Raspberry Pi

### Wiring Diagram
```
Raspberry Pi GPIO 17 (Pin 11) ——┬——> LED (Positive Leg)
                               │
                          220Ω Resistor
                               │
                          Ground (Pin 6 or 9)
```

---

## Step-by-Step Setup Guide

### Step 1: Wire It Up
1. Connect the LED's **longer leg** to **GPIO 17** (Physical Pin 11)
2. Connect the LED's **shorter leg** to a **220Ω-330Ω resistor**
3. Connect the other end of the resistor to a **Ground pin** (Pin 6 or 9)
4. Double-check connections before power-on

### Step 2: Grab the Code
Open your Raspberry Pi terminal and clone this repository:

```bash
git clone https://github.com/Iniyan-philomath/Hybrid-Voice-Vision-Automation-Pi.git
cd Hybrid-Voice-Vision-Automation-Pi
```

### Step 3: Install the Software
Update your system and install required packages:

```bash
sudo apt update
sudo apt install python3-pyaudio flac python3-opencv
```

Install Python libraries:

```bash
pip3 install gpiozero opencv-python numpy SpeechRecognition
```

### Step 4: Run the Project

**Main hybrid controller** (recommended):
```bash
python3 hybrid_controller.py
```

**Camera-only mode**:
```bash
python3 auto_light.py
```

**Voice-only mode**:
```bash
python3 voice_led.py
```

> ℹ️ **Note**: When you first run the script, **stay quiet for 2 seconds** so the microphone can calibrate to your room's background noise.

---

## How to Talk to It

| Command | Action | Mode |
|---------|--------|------|
| **"Turn on"** | Force LED ON | Overrides camera |
| **"Turn off"** | Force LED OFF | Overrides camera |
| **"Auto"** | Resume camera control | Returns to vision mode |

---

## Project Files

### 1. `hybrid_controller.py` (Main Script) ⭐
- Runs both camera and voice simultaneously
- Camera handles auto-lighting
- Voice commands override camera
- Best for real-world automation
- ~100 lines of well-commented code

### 2. `auto_light.py`
- Vision-only automation
- No voice control
- Good for testing camera functionality
- ~50 lines of code

### 3. `voice_led.py`
- Voice-only control
- No camera dependencies
- Useful for testing microphone setup
- ~60 lines of code

---

## Troubleshooting

### Issue: "No module named 'gpiozero'"
**Solution**: Install with `pip3 install gpiozero`

### Issue: "Microphone not found"
**Solution**: Check USB webcam is connected: `lsusb`

### Issue: "Permission denied" for GPIO
**Solution**: Run with sudo: `sudo python3 hybrid_controller.py`

### Issue: "LED doesn't turn on"
**Solution**: Check wiring, verify resistor value, test with simple GPIO script

### Issue: "Speech recognition slow/hanging"
**Solution**: Check internet connection, reduce phrase timeout in code

---

## License

MIT License - Use, modify, and distribute freely
