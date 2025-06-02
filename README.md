# 🎯 Video Object Detection using YOLOv5

This project demonstrates **video-based object detection** using the YOLOv5 model in **Google Colab**. The complete pipeline includes video upload, object detection with bounding boxes, saving cropped objects, and displaying the output—all inside a Colab notebook.

## 📌 Project Overview

Using the Ultralytics YOLOv5 framework, this notebook allows users to:
- Upload any `.mp4` video
- Run YOLOv5 detection on it
- Save results (bounding boxes, confidence scores, and cropped objects)
- Display the detected video output inside the notebook


## 🛠️ Technologies Used
- Python (Google Colab)
- OpenCV
- YOLOv5 (`yolov5s.pt`)
- Ultralytics GitHub repository
- COCO Dataset labels (pre-trained model)

---

## 🚀 Steps to Run

1. **Clone the YOLOv5 Repository**
```bash
!git clone https://github.com/ultralytics/yolov5 -q
%cd yolov5
!pip install -r requirements.txt -q
````

2. **Upload Your Video File**

```python
from google.colab import files
uploaded = files.upload()
```

3. **Rename and Prepare the Input File**

```python
import os
uploaded_filename = list(uploaded.keys())[0]
os.rename(uploaded_filename, "input.mp4")
```

4. **Run YOLOv5 Detection**

```bash
!python detect.py \
  --weights yolov5s.pt \
  --source input.mp4 \
  --img 640 \
  --conf 0.4 \
  --save-txt \
  --save-conf \
  --save-crop \
  --project runs/detect \
  --name gen4_analysis \
  --exist-ok
```

5. **Display Output Video**

```python
import glob
from IPython.display import HTML
from base64 import b64encode

output_videos = glob.glob('runs/detect/gen4_analysis/*.mp4')
if output_videos:
    video_path = output_videos[0]
    mp4 = open(video_path, 'rb').read()
    data_url = "data:video/mp4;base64," + b64encode(mp4).decode()
    display(HTML(f'<video width=720 controls><source src="{data_url}" type="video/mp4"></video>'))
else:
    print("❌ Output video not found. Check if detection ran successfully.")
```

---

## 📂 Output Features

* 🎯 Bounding boxes with object names and confidence scores
* ✂️ Cropped images of each detected object
* 💾 Text files with detection data
* 📹 Final video with detection overlay

