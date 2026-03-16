# 🎯 Real-Time Object Detection and Tracking

> **Task 4 — Apexcify Internship Program**  
> Real-time object detection and multi-object tracking using YOLOv8 and OpenCV.

---

## 📌 Project Overview

This project implements a **real-time object detection and tracking system** using the [YOLOv8](https://docs.ultralytics.com/) model from Ultralytics combined with [OpenCV](https://opencv.org/). It captures live video from a webcam (or a video file), runs YOLOv8's built-in tracker on every frame, and displays the result with **bounding boxes**, **class labels**, **confidence scores**, and **unique tracking IDs** for each detected object — all in real time.

The system is capable of detecting **80 object categories** from the COCO dataset (e.g., person, car, bicycle, dog, laptop, phone, etc.) and persistently tracks each object across consecutive frames by maintaining consistent IDs.

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
  (Assigns/Maintains Track IDs)
        │
        ▼
  Annotate Frame
  (Boxes + Labels + IDs)
        │
        ▼
  Display Output Window
  (Press 'q' to quit)
```

### Step-by-Step Breakdown

| Step | Description |
|------|-------------|
| **1. Model Loading** | Loads the pre-trained `yolov8n.pt` (nano) model weights. The model is auto-downloaded on first run if not present locally. |
| **2. Video Capture** | Opens the default webcam (`index 0`) using `cv2.VideoCapture()`. A path to a video file can also be supplied instead. |
| **3. Frame Reading** | Reads frames one by one inside a `while` loop. If no frame is returned (video ends or camera disconnects), the loop exits gracefully. |
| **4. YOLOv8 Tracking** | Calls `model.track(frame, persist=True)`, which performs detection and tracking in a single step. `persist=True` ensures track IDs are maintained across frames. |
| **5. Annotation** | `results[0].plot()` renders bounding boxes, category labels, confidence scores, and track IDs directly onto the frame. |
| **6. Display** | Displays the annotated frame in an OpenCV window titled **"YOLOv8 Object Tracking"**. |
| **7. Exit** | Pressing the **`q`** key releases the camera and closes all windows cleanly. |

---

## 🗂️ Project Structure

```
TASK 4 Object Detection and Tracking/
│
├── main.py               # Main application script
├── requirements.txt      # Python dependencies
├── yolov8n.pt            # Pre-trained YOLOv8 Nano model weights (~6.5 MB)
└── README.md             # Project documentation (this file)
```

---

## 🔧 Technologies Used

| Technology | Purpose |
|---|---|
| **Python 3.8+** | Programming language |
| **YOLOv8 (Ultralytics)** | State-of-the-art object detection model |
| **OpenCV (`opencv-python`)** | Video capture, frame processing, and display |
| **ByteTrack** | Built-in multi-object tracker inside Ultralytics |
| **COCO Dataset Weights** | Pre-trained on 80 object classes |

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

The **Nano** variant is used for its fast inference speed, making it ideal for real-time webcam tracking even without a GPU. Larger variants (`yolov8s`, `yolov8m`, `yolov8l`, `yolov8x`) offer higher accuracy at the cost of speed.

---

## ⚙️ Setup & Installation

### Prerequisites

- Python **3.8 or higher**
- A **webcam** connected to your machine (or a local video file)
- (Optional but recommended) A **GPU** with CUDA support for faster inference

### 1. Clone / Navigate to the Project Directory

```bash
cd "TASK 4 Object Detection and Tracking"
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

This installs:
- `ultralytics` — YOLOv8 framework
- `opencv-python` — Video capture and display

> **Note:** On first run, PyTorch will also be automatically installed as a dependency of `ultralytics`.

---

## ▶️ Running the Application

```bash
python main.py
```

- An OpenCV window named **"YOLOv8 Object Tracking"** will open.
- All detected objects will be highlighted with **color-coded bounding boxes**.
- Each tracked object is assigned a **persistent numeric ID** (Track ID).
- Press **`q`** at any time to quit.

### Using a Video File Instead of Webcam

To run detection on a pre-recorded video file, change line 11 in `main.py`:

```python
# Change this:
video_source = 0

# To this:
video_source = "path/to/your/video.mp4"
```

---

## 🖥️ Output Example

When running, the display window shows:

- **Bounding Box** — A colored rectangle around each detected object
- **Label** — The class name (e.g., `person`, `car`, `dog`)
- **Confidence Score** — How confident the model is (e.g., `0.91`)
- **Track ID** — A unique persistent ID (e.g., `#1`, `#2`) that follows each object across frames

---

## 📋 Dependencies (`requirements.txt`)

```
ultralytics
opencv-python
```

Install all at once with:
```bash
pip install -r requirements.txt
```

---

## 🚀 Key Features

- ✅ **Real-time inference** — Processes live webcam feed frame by frame
- ✅ **Multi-object tracking** — Simultaneously tracks multiple objects with unique IDs
- ✅ **80 COCO classes** — Detects people, vehicles, animals, everyday objects, and more
- ✅ **Persistent tracking** — Track IDs stay consistent even when objects temporarily leave the frame
- ✅ **Minimal codebase** — Entire implementation in under 50 lines of clean Python
- ✅ **Flexible input** — Supports both webcam and video file inputs

---

## 📚 References

- [Ultralytics YOLOv8 Documentation](https://docs.ultralytics.com/)
- [YOLOv8 Tracking Guide](https://docs.ultralytics.com/modes/track/)
- [OpenCV Documentation](https://docs.opencv.org/)
- [COCO Dataset](https://cocodataset.org/)
- [ByteTrack Paper](https://arxiv.org/abs/2110.06864)

---

## 👨‍💻 Author

**Developed as part of the Apexcify Internship Program**  
Task 4: Object Detection and Tracking  
Date: March 2026

---

## 📝 License

This project is built for educational and internship purposes under the Apexcify Technology internship program.
