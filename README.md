# YOLO Object Detection Using Shared Memory (Producer–Consumer Model)

## 📌 Overview
This project demonstrates an inter-process communication (IPC) system using **Shared Memory**, **Semaphores**, and **Mutexes** on Windows OS.  

A C++ application acts as a **Producer** that performs YOLOv5 object detection using ONNX Runtime and writes detection results and image frames into shared memory.  

A Python application acts as a **Consumer** that reads data from shared memory, visualizes bounding boxes, and displays results in real time.

This architecture follows the classical **Producer–Consumer Problem**.

---

## 🎥 Demo Video

Watch the full project demonstration on YouTube:  
👉 https://youtu.be/PJQRg-taNT4

---

## 📸 Sample Output Screenshots

### Detection Example 1
![Detection Example 1](assets/boxing1.png)

### Detection Example 2
![Detection Example 2](assets/boxing2.png)

---

## 🧠 System Architecture

```
Video / Webcam
     |
     v
C++ Producer (YOLO + ONNX)
     |
     v
Shared Memory (Circular Queue)
     |
     v
Python Consumer (OpenCV Display)
```

---

## 🗂 Folder Structure

```
EMBEDDED_ASSIGNMENT/
│
├── producer/
│   ├── test.cpp
│   ├── yolov5s.onnx
│   ├── video.mp4
│   └── Visual Studio project files
│
├── consumer/
│   ├── consumer_shm.py
│   ├── coco-classes.txt
│   └── requirements.txt
│
└── README.md
```

---

## ⚙ Technologies Used

- C++
- Python 3.x
- OpenCV
- ONNX Runtime
- NumPy
- PyWin32 (Windows API)
- Windows Shared Memory

---

## 🔁 Data Flow

1. Producer reads video/webcam frames.
2. YOLOv5 performs object detection.
3. Detection results + frame written into shared memory.
4. Consumer reads from shared memory.
5. Consumer draws boxes and shows output.

---

## 🧱 Shared Memory Layout

```
[Control Block]
- write_index (int)
- read_index  (int)
- count       (int)

[Slot 0]
[Slot 1]
[Slot 2]
[Slot 3]
[Slot 4]
```

Each Slot:

```
Header (20 bytes)
- frame_id
- width
- height
- channels
- number_of_detections

Detections (200 × 24 bytes)
- class_id
- confidence
- x
- y
- width
- height

Image Data
- 640 × 640 × 3 (BGR)
```

---

## 🔐 Synchronization Objects

- Semaphore EMPTY → counts free slots  
- Semaphore FULL → counts filled slots  
- Mutex → protects memory access  

Ensures safe producer–consumer operation.

---

## 📦 Installation

### Python Requirements

Create `requirements.txt`:

```
numpy
opencv-python
pywin32
```

Install:

```
pip install -r requirements.txt
python -m pywin32_postinstall
```

---

## ▶ How To Run

### Step 1 – Start Producer (C++)

- Open `producer` project in Visual Studio.
- Build the project.
- Run the executable.

### Step 2 – Start Consumer (Python)

```
cd consumer
python consumer_shm.py
```

---

## ⌨ Controls

- ESC → Exit  
- SPACE → Pause / Resume  

---

## ✅ Output

- Real-time video display  
- Bounding boxes  
- Class name & confidence  
- FPS  
- Frame number  

---

## 🧪 Example Output

```
Frame: 120
FPS: 28.5
Detections: 6
person 0.87
car 0.91
```

---

## 🎯 Learning Outcomes

- Inter-process communication
- Windows synchronization
- Shared memory design
- YOLO inference using ONNX
- Producer–Consumer problem

---

## 👨‍🎓 Author

Student Name  
Course / Subject  
University / College  

---

## 📜 License

This project is created for academic and learning purposes.
