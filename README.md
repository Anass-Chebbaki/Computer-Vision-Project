# 🔧 Keypoint Detection for Robot Grasping

## 📌 Project Overview
This project was developed in collaboration with **Schnell S.p.A.**, a leading company in the construction industry specialized in the production of steel reinforcements through automated bending of iron rods.  

The main goal is to **automate the quality control of bent steel stirrups** using **Computer Vision and Deep Learning** techniques.  
The system detects **keypoints** from static images acquired by a camera, supporting both **robotic grasping** and **geometrical conformity verification**.

---

## 🎯 Objectives and Challenges
- Detect stirrup keypoints regardless of geometry or class.  
- Work with a **small dataset (~270 images)**.  
- Manage **complex and non-standard annotations**.  
- Handle **overlapping and occluded stirrups**.  
- Standardize to a **fixed number of 7 keypoints per object**.  

---

## 🗂️ Dataset
- **Source**: industrial images provided by Schnell S.p.A.  
- **Annotation**: custom annotation tool in **HTML/JavaScript** for bounding boxes and keypoints.  
- **Pre-processing**:  
  - Removed duplicates via Python hashing (MD5/SHA256).  
  - Filtered irrelevant or noisy images.  
  - Normalized keypoints with padding (dummy points at (0,0) for missing ones).  
- **Split**: 70% training, 20% validation, 10% test.  

---

## 🧠 Model Architecture
We adopted **YOLOv11-Pose** (Ultralytics), which integrates:  
- **Object Detection** (bounding boxes).  
- **Pose Estimation** (keypoints).  

### 🔹 Key Features
- **Backbone**: CNN for feature extraction.  
- **Neck**: multi-scale feature aggregation (PANet/FPN).  
- **Heads**:  
  - Detection head → bounding boxes + classes.  
  - Pose head → keypoints estimation.  
- **Loss Function**: weighted sum of Box, Class, DFL, Pose, and Keypoint-object losses.  

---

## ⚙️ Experimental Setup
- **Data Augmentation**:  
  - Color jitter (hue, saturation, brightness).  
  - Rotation (±30°), translation (10%), scaling (0.4), shear (±2°).  
  - Mosaic augmentation.  
- **Training Strategy**:  
  - **Phase 1**: 80 epochs, freeze first 10 layers, LR = 0.01 (cosine decay).  
  - **Phase 2**: 300 epochs, full fine-tuning, LR = 0.001 (cosine decay), early stopping with patience = 70.  
- **Optimizer**: Stochastic Gradient Descent (SGD).  
- **Metrics**: Precision, Recall, mAP, OKS, PCK.  

---

## 📊 Results
- **Bounding Box Detection**:  
  - Precision = 1.000  
  - Recall = 0.995  
  - mAP50 ≈ 0.995  
- **Keypoint Estimation**:  
  - mAP50 ≈ 0.82  
  - OKS ≈ 0.58  
- **Best Architecture**: **YOLOv11-small**  
  - Best trade-off between accuracy and inference time (~0.9s/img).  

---

## 🛠️ Tools & Technologies
- **Languages**: Python, JavaScript, HTML  
- **Deep Learning Framework**: [Ultralytics YOLOv11](https://docs.ultralytics.com)  
- **Python Libraries**:  
  - `PyTorch` (training)  
  - `Ultralytics` (YOLOv11)  
  - `hashlib`, `Pillow` (dataset preprocessing)  
- **Annotation Tool**: custom HTML/JS web app  
- **Development Environment**: Jupyter Notebook, Google Colab  

---

## 👥 Team
- **Anass Chebbaki**  
- **Matteo Stronati**  

Supervision: **Prof. Lucia Migliorelli**  
Tutors: **Lorenzo Federici**, **Riccardo Rosati**

---

## 📌 Conclusions
This project validated the use of **YOLOv11-Pose** for **industrial keypoint detection**, showing:  
- Near-perfect performance in **object detection**.  
- Promising results in **keypoint estimation** despite dataset limitations.  

### 🔮 Future Work
- Collect a **larger and more balanced dataset**.  
- Extend the system to **classify different stirrup types**.  
- Explore frameworks such as **[PyTorch Keypoint Detection](https://github.com/tlpss/keypoint-detection)** to improve flexibility and robustness.  

---
