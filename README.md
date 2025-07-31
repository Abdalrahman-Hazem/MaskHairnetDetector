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
