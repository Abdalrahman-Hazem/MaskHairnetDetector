# MaskHairnetDetector

This project is a real-time mask and hairnet detection system built with:
- A **custom-trained YOLOv8 model**, exported to ONNX format
- A **Streamlit web interface** for image-based inference
- **ONNX Runtime** for fast and lightweight model inference

---

## 📦 Features

- Supports image uploads via a simple Streamlit UI
- Runs inference using a YOLOv8 ONNX model
- Applies confidence filtering and custom **Non-Maximum Suppression (NMS)**
- Draws bounding boxes with class labels
- Displays **class-wise detection counts**
- Supports **CPU and GPU (CUDA)** inference

---

## 🧠 Classes Detected

The model detects the following 4 classes:

1. `NO mask`  
2. `NOhairnet`  
3. `hairnet`  
4. `mask`

---

## 📁 Project Structure
├── streamlit_app.py # Main Streamlit web app
├── best.onnx # Exported YOLOv8 ONNX model
├── requirements.txt # Python dependencies
└── README.md # This file


---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/MaskHairnetDetector
cd MaskHairnetDetector

# Using conda
conda create -n MaskHairNetProject python=3.10
conda activate MaskHairNetProject

pip install -r requirements.txt

streamlit run streamlit_app.py

=======================================================================================

# Fixing YOLOv8 ONNX Inference in Streamlit Without PyTorch

Overview:
I faced issues while deploying a YOLOv8 ONNX model in a Streamlit app for mask and hairnet detection. Although the model worked locally using the Ultralytics YOLO API, the deployment using ONNXRuntime in Streamlit produced incorrect bounding boxes, duplicated detections, and dependency issues.

Problems Encountered:
1. **Incorrect and duplicated bounding boxes**:
   - Bounding boxes were stacked on top of each other or offset from the true object locations.
   - This was due to poor handling of postprocessing and bounding box scaling.

2. **Dependency failure**:
   - We initially used `torchvision.ops.nms`, which relies on PyTorch.
   - Streamlit Cloud doesn't support custom packages like PyTorch by default, causing a `ModuleNotFoundError`.

Solution:
1. **Removed Torch Dependencies**:
   - Deleted `torch` and `torchvision` imports.
   - Replaced `torchvision.ops.nms()` with a pure NumPy implementation of Non-Maximum Suppression (NMS).

2. **Corrected Bounding Box Handling**:
   - Added a helper function `xywh2xyxy()` to convert center-based YOLO box format to corner-based.
   - Properly scaled coordinates back to original image dimensions after resizing during preprocessing.
   - Implemented a clean and reliable NumPy-based `non_max_suppression()` function.

3. **Streamlined Postprocessing**:
   - The `postprocess()` function now handles:
     - Conversion of model output.
     - Confidence thresholding.
     - NMS.
     - Bounding box scaling.

Outcome:
The Streamlit app now works reliably with:
- Accurate detection of bounding boxes.
- No dependency on PyTorch.
- Efficient performance using ONNXRuntime and NumPy.

Recommendation:
For deployment in cloud environments like Streamlit Cloud, always avoid heavyweight dependencies unless explicitly supported. When using ONNX, rely on NumPy for postprocessing and remove torch-based utilities unless necessary.

Author: Abdalrahman Hazem
