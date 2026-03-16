# 🎯 Real-Time Object Detection and Tracking

[![Contributors](https://img.shields.io/github/contributors/Gotam-Dulhani/Object-Detection-and-Tracking)](https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking/graphs/contributors)
[![Forks](https://img.shields.io/github/forks/Gotam-Dulhani/Object-Detection-and-Tracking)](https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking/network/members)
[![Stars](https://img.shields.io/github/stars/Gotam-Dulhani/Object-Detection-and-Tracking)](https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking/stargazers)
[![Issues](https://img.shields.io/github/issues/Gotam-Dulhani/Object-Detection-and-Tracking)](https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking/issues)
[![License](https://img.shields.io/github/license/Gotam-Dulhani/Object-Detection-and-Tracking)](https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking/blob/main/LICENSE)

> **Real-time object detection and multi-object tracking** using YOLOv8 and OpenCV — detects 80 COCO object classes from a live webcam feed and assigns persistent tracking IDs across frames.


---

## 📌 Table of Contents

* [About The Project](#-about-the-project)
* [Key Features](#-key-features)
* [Built With](#-built-with)
* [Model Details](#-model-details)
* [How It Works](#-how-it-works)
* [Project Structure](#-project-structure)
* [Getting Started](#-getting-started)
* [Usage](#-usage)
* [Contributing](#-contributing)
* [License](#-license)
* [Contact](#-contact)

---

## 💡 About The Project

This project implements a **real-time object detection and tracking system** using **YOLOv8** (Ultralytics) combined with **OpenCV**. It captures live video from a webcam or video file, runs YOLOv8's built-in ByteTrack tracker on every frame, and displays bounding boxes, class labels, confidence scores, and unique tracking IDs for each detected object — all in real time.

The system detects **80 object categories** from the COCO dataset (person, car, bicycle, dog, laptop, phone, and more) and persistently tracks each object across consecutive frames with consistent IDs — even when objects temporarily leave the frame.

---

## ✨ Key Features

* **Real-Time Inference** – Processes live webcam feed frame by frame.
* **Multi-Object Tracking** – Simultaneously tracks multiple objects with unique persistent IDs.
* **80 COCO Classes** – Detects people, vehicles, animals, and everyday objects.
* **Persistent Tracking** – Track IDs stay consistent even when objects temporarily leave frame.
* **Flexible Input** – Supports both webcam and video file inputs.
* **Minimal Codebase** – Entire implementation in under 50 lines of clean Python.

---

## 🛠 Built With

| Technology | Purpose |
|---|---|
| Python 3.8+ | Core language |
| YOLOv8 (Ultralytics) | State-of-the-art object detection model |
| OpenCV (`opencv-python`) | Video capture, frame processing & display |
| ByteTrack | Built-in multi-object tracker inside Ultralytics |
| COCO Dataset Weights | Pre-trained on 80 object classes |

---

## 📦 Model Details

| Property | Value |
|---|---|
| **Model** | YOLOv8 Nano (`yolov8n.pt`) |
| **Training Dataset** | COCO (Common Objects in Context) |
| **Number of Classes** | 80 |
| **Model Size** | ~6.5 MB |
| **Tracker** | ByteTrack (default in Ultralytics) |
| **Speed** | Optimized for real-time inference on CPU |

> The **Nano** variant is used for fast inference on CPU. Larger variants (`yolov8s`, `yolov8m`, `yolov8l`, `yolov8x`) offer higher accuracy at the cost of speed.

---

## 🧠 How It Works

```
Webcam / Video File
        │
        ▼
Frame Capture (OpenCV)
        │
        ▼
YOLOv8n Inference
(Object Detection)
        │
        ▼
Built-in ByteTrack Tracker
(Assigns / Maintains Track IDs)
        │
        ▼
Annotate Frame
(Boxes + Labels + Confidence + IDs)
        │
        ▼
Display Output Window
(Press 'q' to quit)
```

### Step-by-Step Breakdown

| Step | Description |
|---|---|
| **1. Model Loading** | Loads pre-trained `yolov8n.pt` weights — auto-downloaded on first run if not present |
| **2. Video Capture** | Opens default webcam (`index 0`) via `cv2.VideoCapture()` — video file path also supported |
| **3. Frame Reading** | Reads frames one by one in a `while` loop; exits gracefully if camera disconnects |
| **4. YOLOv8 Tracking** | Calls `model.track(frame, persist=True)` — detection + tracking in a single step |
| **5. Annotation** | `results[0].plot()` renders boxes, labels, confidence scores & track IDs onto the frame |
| **6. Display** | Shows annotated frame in an OpenCV window titled **"YOLOv8 Object Tracking"** |
| **7. Exit** | Press **`q`** to release the camera and close all windows cleanly |

---

## 📁 Project Structure

```
Object-Detection-and-Tracking/
│
├── main.py               # Main application script
├── requirements.txt      # Python dependencies
├── yolov8n.pt            # Pre-trained YOLOv8 Nano model weights (~6.5 MB)
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

* Python 3.8+
* A webcam connected to your machine (or a local video file)
* *(Optional but recommended)* GPU with CUDA support for faster inference

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/Gotam-Dulhani/Object-Detection-and-Tracking.git
cd Object-Detection-and-Tracking
```

**2. Create a virtual environment** *(recommended)*

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

> On first run, PyTorch is automatically installed as a dependency of `ultralytics`.

---

## 📝 Usage

**Run the application:**

```bash
python main.py
```

* An OpenCV window named **"YOLOv8 Object Tracking"** will open.
* Detected objects are highlighted with **color-coded bounding boxes**.
* Each tracked object receives a **persistent numeric Track ID**.
* Press **`q`** at any time to quit.

**Use a video file instead of webcam:**

Edit line 11 in `main.py`:

```python
# Change this:
video_source = 0

# To this:
video_source = "path/to/your/video.mp4"
```

### Output

Each frame displays:

| Element | Description |
|---|---|
| **Bounding Box** | Colored rectangle around each detected object |
| **Label** | Class name (e.g. `person`, `car`, `dog`) |
| **Confidence Score** | Model certainty (e.g. `0.91`) |
| **Track ID** | Unique persistent ID (e.g. `#1`, `#2`) |

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repo
2. Create a feature branch:

```bash
git checkout -b feature/AmazingFeature
```

3. Commit your changes:

```bash
git commit -m "Add AmazingFeature"
```

4. Push and open a Pull Request:

```bash
git push origin feature/AmazingFeature
```

---

## 📝 License

Distributed under the **MIT License**. See `LICENSE` for details.

---

## 📫 Contact

**Gotam Dulhani**
GitHub: [https://github.com/Gotam-Dulhani](https://github.com/Gotam-Dulhani)

---

## 🙏 Acknowledgments

* [Ultralytics YOLOv8 Documentation](https://docs.ultralytics.com/)
* [YOLOv8 Tracking Guide](https://docs.ultralytics.com/modes/track/)
* [OpenCV Documentation](https://docs.opencv.org/)
* [COCO Dataset](https://cocodataset.org/)
* [ByteTrack Paper](https://arxiv.org/abs/2110.06864)
* Open Source Community ❤️
