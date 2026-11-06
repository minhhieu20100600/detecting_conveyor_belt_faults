# Conveyor Belt Fault Detection System

This project aims to provide an efficient solution for detecting faults in conveyor belts using advanced technologies such as computer vision, ultrasonic sensors, and machine learning. The system can identify damages, cracks, and abnormalities in conveyor belts and measure their thickness, ensuring enhanced operational efficiency, reduced downtime, and cost savings in industrial settings.

---

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Results](#results)
- [Future Scope](#future-scope)
- [Contributing](#contributing)

---

## Introduction

Conveyor belt systems are critical in industrial operations. However, faults such as tears, cracks, and thickness degradation can cause significant production losses and safety risks. This project integrates high-speed computer vision, ultrasonic sensors, and local TensorRT Edge AI models to detect and diagnose these issues in real time.

  

---

## Features
- Real-time surface defect and crack detection using hardware-triggered image acquisition.
- Thickness measurement of the conveyor belt using an ultrasonic sensor.
- Zero-latency hardware interrupt driven by ESP32-S3 for precise capture alignment.
- Local TensorRT Edge AI inference delivering sub-20ms system response time.
- Automated actuation for fault rejection and emergency system shutdown upon severe damage detection.
- Data monitoring via a local Python/FastAPI web dashboard integrated with serial IoT bridge.

---

## Technologies Used
- **Hardware**: ESP32-S3 Microcontroller, E18-D80NK Photoelectric Sensor, HC-SR04 Ultrasonic Sensor, High-Speed USB Camera, Servo Actuator.
- **Software**: Python 3.10+, PyTorch, NVIDIA TensorRT, OpenCV, VS Code (PlatformIO IDE), Serial UART Protocol.
- **AI Model**: Unsupervised PatchCore Anomaly Detection fine-tuned on normal surface features and compiled to TensorRT FP16/INT8 engine.

---

## Requirements
### Hardware
- ESP32-S3 Dev Module
- E18-D80NK Photoelectric Infrared Sensor
- HC-SR04 Ultrasonic Sensor
- High-Speed USB Webcam (1080p @ 60 FPS)
- Connecting wires, breadboard, and 5V 2A power supply

### Software
- Python 3.10 or above
- Visual Studio Code (VS Code) with PlatformIO IDE extension
- NVIDIA CUDA Toolkit & TensorRT SDK
- PySerial, OpenCV, PyTorch, ONNX Runtime
- Flask / FastAPI (for local web server)

---

## Setup Instructions

1. **Hardware Setup**:
   - Mount the USB camera directly above the conveyor belt for a top-down view.
   - Position the E18-D80NK photoelectric sensor at the entry point to act as a hardware trigger.
   - Position the HC-SR04 ultrasonic sensor beneath or alongside the conveyor belt for thickness evaluation.
   - Connect the components to the ESP32-S3 microcontroller as specified in the repository wiring diagram.
      
       
2. **Software & Firmware Setup**:
   - Clone the repository:
     ```bash
     git clone [https://github.com/yourusername/conveyor-belt-fault-detection.git](https://github.com/yourusername/conveyor-belt-fault-detection.git)
     cd conveyor-belt-fault-detection
     ```
   - Install Python dependencies:
     ```bash
     pip install -r requirements.txt
     ```
   - Open the `firmware` folder in **VS Code** with **PlatformIO IDE** and flash the C++ firmware to the ESP32-S3.

3. **Train & Optimize the AI Model**:
   - Collect 50–100 images of normal (OK) conveyor belt surfaces.
   - Run the training script to build the PatchCore Memory Bank:
     ```bash
     python src/train/train_patchcore.py
     ```
   - Export and compile the model to high-performance TensorRT `.engine` format:
     ```bash
     python scripts/export_onnx.py --input models/raw_weights/patchcore.pt --output models/export/patchcore.onnx
     python scripts/build_tensorrt.py --onnx models/export/patchcore.onnx --output models/engines/patchcore_fp16.engine --precision fp16
     ```

4. **Run the System**:
   - Start the main real-time inspection engine and local web server:
     ```bash
     python src/main.py
     ```
   - Open the local webpage in your browser to monitor real-time defect logs and thickness metrics.

---

## Usage
- Position the camera, trigger sensor, and ultrasonic sensor as per the setup instructions.
- Power on the ESP32-S3 and start the conveyor belt.
- Monitor real-time video preview, anomaly heatmaps, and thickness updates on the local dashboard.
- Automatic alerts, servo ejection, or system shutdowns will trigger immediately upon fault detection.

---


## Future Scope
- Integration with thermal imaging cameras to detect friction overheating before physical tearing occurs.
- Implementation of Industrial MQTT protocol for multi-device cloud analytics.
- Porting the full execution pipeline to standalone NVIDIA Jetson Orin Nano Edge modules.

---

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request for any improvements or new features.