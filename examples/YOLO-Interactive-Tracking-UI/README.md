# Ultralytics YOLO Interactive Tracking UI 🎯

A modular, educational real-time object detection and tracking UI built with [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) and OpenCV.

This project is ideal for:

- Learning how to integrate [YOLO](https://docs.ultralytics.com) with [object tracking](https://docs.ultralytics.com/modes/track/)
- Testing on edge devices (e.g., Raspberry Pi, Jetson Nano)
- Real-time demos with interactive user input
- Enhancing CV pipelines with tracking UI/UX overlays

---

## Project Demo

![yolo-ezgif com-optimize](https://github.com/user-attachments/assets/179f62e1-97ba-4345-b7cd-a6aa80681996)

---

## Features

- Real-time object detection and visual tracking
- Click on any object to initiate tracking
- Scope lines and bold bounding box for active tracking
- Dashed boxes for passive (non-tracked) objects
- Live terminal updates with object ID, label, confidence, center
- Configurable thresholds and tracker engine (e.g. `bytetrack`, `botsort`)
- Supports:
  - PyTorch `.pt` models for GPU (Jetson, desktop with CUDA)
  - NCNN `.param + .bin` models for CPU-only (Raspberry Pi, ARM)

---

## Hardware & Model Compatibility

| Platform         | Model Format       | Example Model        | GPU Acceleration | Notes                           |
| ---------------- | ------------------ | -------------------- | ---------------- | ------------------------------- |
| Raspberry Pi 4/5 | NCNN (.param/.bin) | `yolov8n_ncnn_model` | ❌ CPU only      | Recommended format for Pi/ARM   |
| Jetson Nano      | PyTorch (.pt)      | `yolov8n.pt`         | ✅ CUDA          | Real-time performance possible  |
| Desktop w/ GPU   | PyTorch (.pt)      | `yolov8s.pt`         | ✅ CUDA          | Best performance                |
| CPU-only laptops | NCNN (.param/.bin) | `yolov8n_ncnn_model` | ❌               | Decent performance (~10–15 FPS) |

---

## Project Structure

```
YOLO-Interactive-Tracking-UI/
├── interactive_tracker.py   # Main Python tracking UI script
└── README.md                # You're here!
```

---

## Installation

### Basic Dependencies

```bash
pip install ultralytics opencv-python
```

> Use a virtual environment like `venv` or `conda` (recommended).

---

### Optional: Enable GPU (for PyTorch models)

Install PyTorch based on your system and CUDA version:  
👉 https://pytorch.org/get-started/locally/

---

## Quick Start

### Step 1: Download, Convert, or Specify Your Model

- **Official YOLO Models:**  
  For official YOLO models (e.g., `yolov11s.pt` or `yolov8s.pt`), simply specify the model name as `MODEL_PATH_CPU` or `MODEL_PATH_GPU`. These models will be auto-downloaded and cached, or you can manually download them from [Ultralytics Assets Releases](https://github.com/ultralytics/assets/releases) and place them in the folder.
  
- **Custom YOLO Models:**  
  If you're using a custom YOLO model, ensure the model file is in the project folder or provide its relative path in the parameters.

- **Supported Formats:**
  - `yolov8n.pt` (for GPU with PyTorch)
  - `yolov8n_ncnn_model` (for CPU with NCNN)

---

### Step 2: Configure the Script

Edit the top global paramters of `interactive_tracker.py`:

```python
USE_GPU = False  # Set to True for running on GPU

# For official models, simply specify the model name:
MODEL_PATH_GPU = "yolov11s.pt"  # Model that will be run if USE_GPU = True
MODEL_PATH_CPU = "yolov11s.pt"  # or "yolov11s_ncnn_model", Model that will be run if USE_GPU = False


SHOW_FPS = True                   # If True, shows current FPS in top-left corner

CONFIDENCE_THRESHOLD = 0.3        # Min confidence for object detection (lower = more detections, possibly more false positives)
IOU_THRESHOLD = 0.3               # IoU threshold for NMS (higher = less overlap allowed)
MAX_DETECTION = 20                # Maximum objects per frame (increase for crowded scenes)

TRACKER_TYPE = "bytetrack.yaml"   # Tracker config: 'bytetrack.yaml', 'botsort.yaml', etc.

```

---

### Step 3: Run the object tracking

```bash
python interactive_tracker.py
```

---

### Controls

- 🖱️ Left-click → Select an object to track
- 🔄 Press `c` → Cancel/reset tracking
- ❌ Press `q` → Quit the app


---

## Author

- Connect with author: [here](https://www.linkedin.com/in/alireza787b)
- Published Date ![Published Date](https://img.shields.io/badge/published_Date-2025--04--01-purple)


## License & Disclaimer

This project is released under the **AGPL-3.0 license**. For full licensing terms, please visit the [Ultralytics YOLO License](https://github.com/ultralytics/ultralytics/blob/main/LICENSE). 

It is intended solely for educational and demonstration purposes. Please use it responsibly and at your own discretion. The author assumes no liability for any misuse or unintended consequences. Feedback, forks, and contributions are highly encouraged and always appreciated!
