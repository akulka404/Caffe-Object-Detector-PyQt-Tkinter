# Caffe-Object-Detector-PyQt-Tkinter

A Python-based computer vision application that combines multiple real-time image processing and object detection techniques into a unified GUI. The project uses a MobileNet SSD Caffe deep-learning model for object detection, OpenCV for image processing, and presents everything through a two-layer GUI built with PyQt5 and Tkinter.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies & Dependencies](#technologies--dependencies)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Running the Application](#running-the-application)
- [GUI Walkthrough](#gui-walkthrough)
- [Detectable Object Classes](#detectable-object-classes)

---

## Overview

This Software Development Project (SDP) demonstrates several computer-vision techniques unified under a single application:

1. **Neural-network-based object detection** – a pretrained MobileNet SSD Caffe model detects and labels up to 20 object categories in a live webcam feed.
2. **OpenCV object tracking** – three state-of-the-art trackers (CSRT, KCF, MOSSE) let you select and follow a region of interest across video frames.
3. **Haar-cascade detection** – classical face and eye detection using OpenCV's pre-trained Haar cascade classifiers.
4. **Shape detection** – Hough transform-based line and circle detection, including HSV-tunable circle detection via trackbars.

The application starts with an animated Koch snowflake startup screen (drawn with Python's `turtle` module) and then launches the main PyQt5 GUI from which all features are accessible.

---

## Features

| Feature | Description |
|---|---|
| **Object Detection** | Real-time detection of 20 object categories using a MobileNet SSD Caffe model, displayed inside a Tkinter window with Start/Stop controls. |
| **Object Tracking (CSRT)** | Discriminative Correlation Filter with Channel and Spatial Reliability – accurate, slower tracker. |
| **Object Tracking (KCF)** | Kernelized Correlation Filter – fast and efficient single-object tracker. |
| **Object Tracking (MOSSE)** | Minimum Output Sum of Squared Error – very fast, lightweight correlation tracker. |
| **Haar-Cascade Face & Eye Detection** | Detects faces and eyes in a live webcam feed using OpenCV's built-in XML classifiers. |
| **Hough Line Detection** | Detects lane lines in a video file (`input.mp4`) using Canny edge detection and the Probabilistic Hough Transform. |
| **Hough Circle Detection** | Detects circular objects in a live webcam feed; HSV color range and edge-detection thresholds are tunable via on-screen trackbars. |
| **Animated Startup Screen** | A recursive Koch snowflake fractal is rendered with the `turtle` module before the main GUI appears. |

---

## Technologies & Dependencies

| Package | Purpose |
|---|---|
| Python 3 | Core language |
| [OpenCV (`cv2`)](https://opencv.org/) | Image capture, processing, DNN inference, object tracking, Haar cascades |
| [PyQt5](https://pypi.org/project/PyQt5/) | Main application GUI framework |
| [Tkinter](https://docs.python.org/3/library/tkinter.html) | Secondary GUI for the object-detection window (built into Python) |
| [NumPy](https://numpy.org/) | Array and numerical operations |
| [imutils](https://github.com/jrosebr1/imutils) | Convenience functions for OpenCV (resize, video stream) |
| [Pillow (PIL)](https://python-pillow.org/) | Converting OpenCV frames for display inside Tkinter |
| `turtle` | Animated startup sequence |
| MobileNet SSD (Caffe) | Pretrained deep-learning model for object detection |

Install Python dependencies with:

```bash
pip install opencv-python PyQt5 numpy imutils Pillow
```

---

## Project Structure

```
Caffe-Object-Detector-PyQt-Tkinter/
│
├── SDP.py                             # Entry point – animated startup, then launches sdpf.py
├── sdpf.py                            # Main PyQt5 GUI (Shape Detection / Object Tracking /
│                                      #   Haar-Cascade Detection / Object Detection)
├── sdpx.py                            # Shape detection sub-window (Hough Lines / Circles)
├── OtherWindow.py                     # Object tracking sub-window (CSRT / KCF / MOSSE)
├── shape.py                           # Shape-type selection sub-window
│
├── main.py                            # Standalone Tkinter object-detection app
├── settings.py                        # Shared global state (start_video, start_processing)
│
├── csrt.py                            # CSRT object tracker
├── kcf.py                             # KCF object tracker
├── mosse.py                           # MOSSE object tracker
│
├── face.py                            # Haar-cascade face & eye detection
├── circle.py                          # Hough circle detection with HSV trackbars
├── solution.py                        # Hough line/lane detection on a video file
│
├── MobileNetSSD_deploy.prototxt.txt   # MobileNet SSD model architecture
├── MobileNetSSD_deploy.caffemodel     # MobileNet SSD pretrained weights
│
├── haarcascade_frontalface_default.xml # OpenCV frontal-face Haar cascade
├── haarcascade_eye.xml                # OpenCV eye Haar cascade
│
└── input.mp4                          # Sample video used for Hough line/lane detection
```

---

## Getting Started

### Prerequisites

- Python 3.6 or later
- A webcam (most features require camera index `1`; adjust `cv2.VideoCapture(1)` to `cv2.VideoCapture(0)` if needed)
- All model and cascade files must remain in the same directory as the scripts

### Installation

```bash
# Clone the repository
git clone https://github.com/akulka404/Caffe-Object-Detector-PyQt-Tkinter.git
cd Caffe-Object-Detector-PyQt-Tkinter

# Install dependencies
pip install opencv-python PyQt5 numpy imutils Pillow
```

---

## Running the Application

### Full application (recommended)

```bash
python SDP.py
```

This plays the Koch snowflake startup animation and then opens the main PyQt5 window (`sdpf.py`).

### Main GUI only (skip startup animation)

```bash
python sdpf.py
```

### Standalone Tkinter object-detection window

```bash
python main.py
```

### Individual trackers (from the command line)

```bash
# CSRT tracker (webcam)
python csrt.py

# KCF tracker (webcam)
python kcf.py

# MOSSE tracker (webcam)
python mosse.py

# Any tracker on a video file
python csrt.py --video path/to/video.mp4
```

---

## GUI Walkthrough

### 1. Startup Screen (`SDP.py`)
A colorful Koch snowflake fractal is drawn using the `turtle` module. After ~1.5 seconds the screen closes and the main window appears.

### 2. Main Window (`sdpf.py`)
The main PyQt5 window presents four buttons alongside a short project description:

| Button | Action |
|---|---|
| **Shape Detection** | Opens the Shape Detection sub-window |
| **Object Tracking** | Opens the tracker-selection sub-window |
| **Haar-Cascade Detection** | Starts face & eye detection in a live webcam feed |
| **Object Detection** | Opens a Tkinter window running MobileNet SSD on the webcam |

### 3. Shape Detection Sub-Window (`sdpx.py` / `shape.py`)
Choose between:
- **Hough Lines** – runs Canny edge detection and Probabilistic Hough Transform on `input.mp4` to identify lane lines.
- **Hough Circles** – opens a live webcam feed with on-screen HSV trackbars to tune circle detection parameters.

### 4. Object Tracking Sub-Window (`OtherWindow.py`)
Choose a tracker algorithm:
- **CSRT** – most accurate, suitable for objects that change appearance.
- **KCF** – fast and reliable for single-object tracking.
- **MOSSE** – fastest tracker, good for simple, predictable motions.

Press **`s`** in the tracker window to draw a bounding box around the object to track; press **`q`** to quit.

### 5. Haar-Cascade Detection (`face.py`)
Detects frontal faces and eyes in real time. Each detected face is outlined in blue; detected eyes are outlined in green. Press **`Esc`** to quit.

### 6. Object Detection Window (`sdpf.py` → Tkinter / `main.py`)
A Tkinter window with Start Video, Stop Video, Start Execution, and Stop Execution buttons:
- **Start Video** – begins capturing frames from the webcam.
- **Start Execution** – runs MobileNet SSD inference on each frame and draws labelled bounding boxes.
- **Stop Execution** – pauses inference while video continues.
- **Stop Video** – stops the webcam feed entirely.

---

## Detectable Object Classes

The MobileNet SSD model can detect the following 20 categories:

`aeroplane`, `bicycle`, `bird`, `boat`, `bottle`, `bus`, `car`, `cat`, `chair`, `cow`, `diningtable`, `dog`, `horse`, `motorbike`, `person`, `pottedplant`, `sheep`, `sofa`, `train`, `tvmonitor`