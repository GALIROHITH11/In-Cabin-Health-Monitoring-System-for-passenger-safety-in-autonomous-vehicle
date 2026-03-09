# In-Cabin Health Monitoring System for Passenger Safety in Semi-Autonomous Vehicles

## Overview

This project presents an AI-based in-cabin health monitoring system
designed to improve passenger safety in semi-autonomous and autonomous
vehicles. The system continuously monitors passenger behavior and
physiological signals to detect potential medical emergencies.

The system integrates computer vision models and physiological sensors
to detect abnormal conditions such as: - Drowsiness - Unconscious
posture - Irregular heart rate - Loss of alertness

When a critical condition is detected, the system automatically triggers
an emergency response, including stopping the vehicle and rerouting it
to a nearby healthcare facility.

------------------------------------------------------------------------

# Key Features

-   Real-time passenger detection using YOLOv8
-   Human posture monitoring using YOLOv8-Pose
-   Eye blinking detection for drowsiness monitoring
-   ECG-based heart rate monitoring
-   Multi-validation emergency detection system
-   Autonomous vehicle integration
-   Real-time communication with vehicle controller via LAN (RJ45
    Ethernet)

------------------------------------------------------------------------

# System Architecture

Main components:

-   ZED2 Camera
-   ECG Sensor
-   Jetson Developer Kit / GPU system
-   Deep Learning Models
-   Vehicle Control System (ROS based)

Workflow:

1.  Camera captures passenger video.
2.  YOLOv8 detects passenger presence.
3.  YOLOv8-Pose analyzes body posture.
4.  Eye blinking model detects eye closure.
5.  ECG sensor monitors heart rate.
6.  Multi-validation logic confirms emergency.
7.  Emergency signal is sent to vehicle controller.

------------------------------------------------------------------------

# Technologies Used

## Programming Language

-   Python

## Deep Learning Framework

-   PyTorch
-   Ultralytics YOLOv8

## Libraries

-   OpenCV
-   NumPy
-   PyTorch
-   Ultralytics
-   CUDA

## Tools

-   Google Colab
-   Label Studio

------------------------------------------------------------------------

# Hardware Requirements

  Hardware               Purpose
  ---------------------- ----------------------------
  NVIDIA RTX 3050 GPU    Model training
  ZED2 Stereo Camera     Real-time cabin monitoring
  ECG Sensor             Heart rate monitoring
  Jetson Developer Kit   Edge computing
  Windows Laptop         Development & testing

------------------------------------------------------------------------

# Software Requirements

  Software      Version
  ------------- --------------
  Python        3.13
  OpenCV        4.12
  PyTorch       CUDA enabled
  Ultralytics   YOLOv8
  CUDA          12.6

------------------------------------------------------------------------

# Dataset

## Camera Dataset

-   Total images: 1544
-   Includes normal posture, sleepy posture, and head leaning posture

Dataset split: - Training: 70% - Validation: 20% - Testing: 10%

## Eye Blinking Dataset

-   Source: Kaggle
-   Images: 27,200

## ECG Dataset

-   Real-time ECG sensor data stored as CSV with timestamps and BPM

------------------------------------------------------------------------

# Models Used

## YOLOv8

Used for detecting passengers inside the vehicle.

## YOLOv8-Pose

Detects 17 human body keypoints including nose, eyes, shoulders, elbows,
hips, knees, and ankles.

## Eye Blinking Model

Detects eye open or closed state to identify drowsiness or
unconsciousness.

------------------------------------------------------------------------

# Emergency Detection Logic

The system uses multi-validation logic to reduce false alarms.

    IF (Posture Abnormal == True) AND (Heart Rate Abnormal == True)
            -> Emergency Detected
            -> Send False signal to vehicle
    ELSE
            -> System Normal

Normal Heart Rate Range:

    60 BPM – 100 BPM

------------------------------------------------------------------------

# Vehicle Integration

The system communicates with the autonomous vehicle using:

-   RJ45 Ethernet connection
-   IPv4 socket communication
-   ROS-based vehicle control system

Emergency Response:

1.  Vehicle slows down
2.  Vehicle stops safely
3.  Vehicle reroutes to nearest hospital

------------------------------------------------------------------------

# Project Structure

    project/
    │
    ├── dataset/
    │   ├── images/
    │   ├── labels/
    │
    ├── models/
    │   ├── yolov8_person_detection
    │   ├── yolov8_pose
    │   ├── eye_blinking
    │
    ├── scripts/
    │   ├── train_yolov8.py
    │   ├── train_pose.py
    │   ├── eye_blink_detection.py
    │   ├── realtime_detection.py
    │
    ├── ecg_module/
    │   ├── ecg_reader.py
    │
    ├── communication/
    │   ├── lan_socket.py
    │
    └── README.md

------------------------------------------------------------------------

# How to Run the Project

## Install Dependencies

    pip install ultralytics
    pip install opencv-python
    pip install torch torchvision
    pip install numpy

## Train YOLO Model

    from ultralytics import YOLO

    model = YOLO("yolov8m.pt")

    model.train(
        data="dataset/data.yaml",
        epochs=150,
        imgsz=640,
        batch=15
    )

## Run Real-Time Monitoring

    python realtime_detection.py

The system will start: - Detecting posture - Monitoring eye blinking -
Checking heart rate - Sending vehicle control signals

------------------------------------------------------------------------

# Future Improvements

-   Integration with edge AI chips
-   Real-time cloud monitoring
-   Improved medical-grade sensors
-   Multi-passenger monitoring
-   Integration with V2X communication

------------------------------------------------------------------------

# Authors

-   Gali Rohith
-   P Surendra
-   G S Vikram
-   K Ram Prasad
-   S B Jeevan

Department of Computer Science and Engineering\
GITAM University, Bengaluru
