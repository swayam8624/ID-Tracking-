Certainly! Below is a detailed **README.md** file for your project:

---

# **RTSP CCTV Surveillance System with YOLOv8 and DeepSORT**

This project provides a real-time surveillance system that processes RTSP streams from CCTV cameras, detects people crossing a specific line of interest, and assigns unique IDs to track them. It utilizes YOLOv8 for object detection and DeepSORT for tracking to maintain synchronized IDs across frames.

## **Table of Contents**
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
- [Customization](#customization)
- [Additional Features](#additional-features)
- [Acknowledgments](#acknowledgments)

---

## **Features**
- **Object Detection:** Detects people using YOLOv8.
- **Tracking:** Tracks people across frames using DeepSORT and assigns unique IDs.
- **Line Crossing Detection:** Notifies when a person crosses a predefined line of interest in the video.
- **RTSP Feed Handling:** Captures and processes real-time CCTV video feeds using RTSP protocol.
- **Real-time Monitoring:** Displays the camera feed with bounding boxes, unique IDs, and alerts for line crossing.

---

## **Installation**

### **1. Clone the Repository**
```bash
git clone https://github.com/your-repo/rtsp-cctv-surveillance.git
cd rtsp-cctv-surveillance
```

### **2. Install Dependencies**
Make sure you have Python 3.8 or higher installed. Then, install the required libraries:

```bash
pip install torch torchvision
pip install ultralytics  # For YOLOv8
pip install opencv-python
pip install filterpy     # For DeepSORT
```

### **3. Download YOLOv8 Pretrained Weights**
YOLOv8 pretrained weights are available via the `ultralytics` library. The script automatically downloads them during the first run, but you can manually download them from the official [YOLOv8 repository](https://github.com/ultralytics/ultralytics).

---

## **Usage**

### **1. Set the RTSP URL**
Replace the `rtsp_url` in the script with your CCTV camera’s RTSP stream URL:

```python
rtsp_url = "rtsp://username:password@camera_ip:port/stream"
```

### **2. Run the Code**
Once the setup is complete, you can run the script to start detecting and tracking people from your RTSP feed.

```bash
python surveillance.py
```

### **3. Key Commands**
- Press **`q`** to quit the video feed display.

---

## **Code Explanation**

1. **YOLOv8 Initialization:**
   - YOLOv8 is used to detect objects (people, in this case) in the video feed. The model weights can be adjusted for different performance needs, such as `yolov8s.pt`, `yolov8m.pt`, or `yolov8l.pt`.

2. **DeepSORT Tracking:**
   - DeepSORT is used to track people across frames and assign them unique IDs. It handles tracking, even when people reappear after temporarily disappearing from the frame.

3. **RTSP Stream Handling:**
   - OpenCV captures the RTSP stream and processes it frame by frame.

4. **Line Crossing Detection:**
   - A line of interest is drawn in the frame, and the system checks whether detected persons have crossed it.

---

## **Customization**

### **1. Adjust Line of Interest**
You can customize the position of the line of interest by adjusting the `line_position` variable in the script:

```python
line_position = 300  # Adjust based on your frame size and camera angle
```

### **2. Modify the YOLOv8 Model**
You can change the YOLOv8 model to balance between speed and accuracy:

- **yolov8n.pt** – Nano model, very fast but less accurate.
- **yolov8s.pt** – Small model, balance between speed and accuracy.
- **yolov8l.pt** – Large model, more accurate but slower.

Modify this line in the code:

```python
yolo_model = YOLO('yolov8s.pt')  # Replace with yolov8n.pt, yolov8m.pt, yolov8l.pt if needed
```

### **3. Add Custom Classes**
By default, the script detects only people (`class 0` in the COCO dataset). You can modify the script to detect other objects by changing the condition:

```python
if int(cls) == 0:  # '0' is the person class in YOLOv8
```

---

## **Additional Features**

### **1. Database Logging**
You can extend the system to log entry/exit events, IDs, and timestamps into a database for historical tracking.

### **2. Multi-camera Support**
You can extend the system to support multiple CCTV cameras by running multiple instances of the script or using threading.

### **3. Alert System**
Add an alert system that sends notifications (e.g., email, SMS) when someone crosses the line of interest.

### **4. Web-based Dashboard**
You can create a web-based dashboard to monitor live feeds and track data in real-time.

---

## **Acknowledgments**
This project uses the following open-source technologies:
- [YOLOv8](https://github.com/ultralytics/ultralytics)
- [DeepSORT](https://github.com/nwojke/deep_sort)
- [OpenCV](https://opencv.org/)

---

Feel free to modify the script according to your needs and contribute to the project!

---

Let me know if you need any adjustments or further details for the `README.md` file!
