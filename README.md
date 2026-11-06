# Conveyor Belt Fault Detection System

This project aims to provide an efficient solution for detecting faults in conveyor belts using advanced technologies such as computer vision, ultrasonic sensors, and machine learning. The system can identify damages, cracks, and abnormalities in conveyor belts and measure their thickness, ensuring enhanced operational efficiency, reduced downtime, and cost savings in industrial settings.

## Table of Contents

* [Introduction](#introduction)
* [Features](#features)
* [Technologies Used](#technologies-used)
* [Requirements](#requirements)
* [Setup Instructions](#setup-instructions)
* [Usage](#usage)
* [Results](#results)
* [Future Scope](#future-scope)
* [Contributing](#contributing)

---

## Introduction

Industrial conveyor belts are critical components in manufacturing and logistics lines. Unplanned failure of these belts leads to costly production downtime. 

This project introduces an **Edge AI-powered Industrial Inspection System** designed for continuous, real-time monitoring of conveyor belts. The system utilizes a dual-pipeline approach:
1. **Visual Defect Inspection:** High-speed computer vision to detect surface cracks, tears, and structural defects.
2. **Thickness & Wear Monitoring:** Ultrasonic sensing to measure physical belt degradation over time.

By utilizing hardware-triggered image acquisition and local TensorRT inference, the system achieves sub-20ms response times for immediate fault rejection.

---

## Features

* **Zero-Latency Hardware Triggering:** Synchronized frame capture using an E18-D80NK photoelectric sensor driven by an ESP32-S3 hardware interrupt.
* **Unsupervised Anomaly Detection:** PatchCore feature extraction algorithm fine-tuned on normal surface samples to detect arbitrary defects without massive labeled defect datasets.
* **Accelerated Edge Inference:** TensorRT FP16/INT8 compiled model execution delivering ultra-low inference latency (< 15ms).
* **Ultrasonic Belt Thickness Measurement:** Real-time physical thickness degradation tracking using ultrasonic sensor integration.
* **Automated Actuation & Rejection:** High-speed pneumatic/servo actuator triggering via USB Serial UART communication upon detecting defective products.
* **Multi-threaded Data Pipeline:** Isolated camera buffer, inference queue, and hardware serial bridge preventing frame drops.

---

## Technologies Used

* **Computer Vision & Deep Learning:** PyTorch, PatchCore, OpenCV, NVIDIA TensorRT, ONNX Runtime
* **Embedded Hardware & IoT:** ESP32-S3 Microcontroller, E18-D80NK Photoelectric Sensor, Ultrasonic Distance Sensor, Servo Actuator
* **Development Environment:** Visual Studio Code (VS Code) with PlatformIO IDE
* **Programming Languages:** Python 3.10+, C++ (Arduino Framework / ESP-IDF)
* **Serial Communication:** USB UART Protocol (Baudrate: 115200)

---

## Requirements

### Hardware Requirements
* **Host Edge Computer:** PC / Laptop equipped with NVIDIA GPU (e.g., RTX series) or NVIDIA Jetson Edge Box
* **Microcontroller:** ESP32-S3 Dev Module
* **Camera:** 1080p High-Speed USB Webcam (60 FPS supported)
* **Sensors & Actuators:**
  * 1x E18-D80NK Photoelectric Infrared Sensor
  * 1x HC-SR04 Ultrasonic Sensor
  * 1x MG996R / SG90 Servo Motor (Ejector)
  * 5V 2A External Power Supply

### Software Requirements
* **IDE:** Visual Studio Code (VS Code)
* **VS Code Extensions:** PlatformIO IDE, Python, C/C++
* **System Drivers:** NVIDIA CUDA Toolkit, TensorRT SDK, USB-to-UART Bridge VCP Driver
* **Python Packages:** `torch`, `torchvision`, `opencv-python`, `pyserial`, `tensorrt`, `onnxruntime`, `numpy`

---

## Setup Instructions

### 1. Repository Setup
Clone the project repository to your local machine:
```bash
git clone [https://github.com/your-username/conveyor-belt-fault-detection.git](https://github.com/your-username/conveyor-belt-fault-detection.git)
cd conveyor-belt-fault-detection