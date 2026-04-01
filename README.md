<h1 align="center">📸 Image Based Smart Attendance System<br> <sub>CS232 Artificial Intelligence Project , SVNIT Surat </sub> </h1> <p align="center"> <b>An automated student attendance system</b><br> <i>Leverages CNN for facial recognition and integrates a custom hardware stack for real-time verification and feedback!</i> </p>

---

## 🖼️ Project Showcase

![Attendance System Photo](https://github.com/user-attachments/assets/37eac6f2-6c36-482b-9a51-b7d42df94093)

---

## 📋 Table of Contents

* [🎯 Project Overview](#-project-overview)
* [⚙️ Hardware Architecture](#️-hardware-architecture)
* [🧠 Software Pipeline](#-software-pipeline)
* [🔬 Explainable AI (XAI)](#-explainable-ai-xai)
* [📈 Performance](#-performance)
* [🏗️ Model Architecture](#-model-architecture)
* [🚀 Setup & Installation](#-setup--installation)
* [📂 Project Structure](#-project-structure)

---

## 🎯 Project Overview

The **Image Based Smart Attendance System** is designed to eliminate the manual effort and inaccuracies of traditional attendance marking. By combining high-level **Convolutional Neural Networks (CNN)** with low-level **microcontroller logic**, the system identifies students in real-time, displays their name on an LCD, and provides audio confirmation.

Unlike standard recognition systems, this project includes **Interpretability** tools, allowing developers to see exactly which facial features the AI prioritizes during the identification process.


**🖼️ Advanced Image Preprocessing**
* Real-time data augmentation (Rotation, Zoom, Horizontal Flips).
* Automated rescaling and batch normalization.


**🧠 Optimized CNN Architecture**
* 3-Stage Convolutional Feature Extraction.
* Dropout-free high-precision learning for small datasets.


**🔍 Deep Interpretability (XAI)**
* **First-Layer Activations:** Visualize the raw edge-detection filters.
* **Grad-CAM Heatmaps:** Spatial mapping of the most influential facial pixels.
* **Confidence Profiling:** Full probability distribution across all classes.


**⚡ Production-Ready Inference**
* Standardized pipeline for processing new, unseen images (`test2.jpg`).
* Seamless model serialization (`.h5` format).


---

## ⚙️ Hardware Architecture

The system follows a coordinated master-slave design between a microprocessor and a microcontroller.

### 🔌 Component List

* **Raspberry Pi 4B (1GB RAM):** The central processing unit for AI inference and image analysis.
* **Raspberry Pi Camera Module v2:** Captures the high-resolution input feed.
* **Arduino Uno:** Manages peripheral hardware signals (LCD & Speaker).
* **16x2 LCD Display (with I2C):** Displays status messages and student names.
* **Speaker/Buzzer:** Provides audible success/failure alerts.
* **Support Gear:** Potentiometer (contrast control), Resistors, Breadboard, Jumper wires, and an 8GB Micro-SD card.

---

## 🧠 Software Pipeline

The software is divided into a training phase and a real-time deployment phase:

1. **Dataset Preparation:** Images are augmented (rotated, flipped, zoomed) to ensure the model is robust against different head angles and lighting.
2. **CNN Modeling:** A 3-layer Convolutional Neural Network built with TensorFlow/Keras.
3. **Optimization:** Trained using the `Adam` optimizer and `Categorical Crossentropy` loss.
4. **Hardware Integration:** The Python script on the Pi communicates with the Arduino (via Serial/I2C) to trigger the LCD and Speaker upon successful recognition.

---

## 🔬 Explainable AI (XAI)

To ensure the model is learning faces rather than backgrounds, we implemented two visualization techniques:

### 1. First-Layer Feature Maps

Visualizes the raw edges, textures, and lines that the CNN detects in the initial stage.

### 2. Grad-CAM Heatmaps

Generates a heatmap overlaying the input image to highlight the "focus zones" (eyes, nose, mouth) that dictated the prediction.

---

## 📈 Performance

| Metric | Result |
| --- | --- |
| **Validation Accuracy** | **98.75%** |
| **Inference Confidence** | **99.9% (Average)** |
| **Recognition Speed** | < 1 second |
| **Classes Trained** | 5 Individuals |

---

## 🏗️ Model Architecture

The model follows a hierarchical spatial feature extraction design:

```
┌─────────────────────────────────────────────────────┐
│                  INPUT: (150, 150, 3)               │
└────────────────────┬────────────────────────────────┘
                     ▼
┌─────────────────────────────────────────────────────┐
│             FEATURE EXTRACTION LAYERS               │
│ • Conv2D (32 filters, 3x3) + MaxPooling             │
│ • Conv2D (64 filters, 3x3) + MaxPooling             │
│ • Conv2D (128 filters, 3x3) + MaxPooling            │
└────────────────────┬────────────────────────────────┘
                     ▼
┌─────────────────────────────────────────────────────┐
│               CLASSIFICATION HEAD                   │
│ • Flatten                                           │
│ • Dense (128 units, ReLU)                           │
│ • Softmax Output (5 classes)                        │
└────────────────────┬────────────────────────────────┘
                     ▼
┌─────────────────────────────────────────────────────┐
│                 FINAL PREDICTION                    │
│        Confidence: 99.9% | Accuracy: 98.7%          │
└─────────────────────────────────────────────────────┘

```

---

## 🚀 Setup & Installation

### Software Requirements

```bash
pip install tensorflow opencv-python matplotlib numpy

```

### Quick Start

1. **Train/Save:** Run the training script to generate `facial_recognition_model.h5`.
2. **Hardware Link:** Connect the Raspberry Pi and Arduino via USB.
3. **Flash Arduino:** Upload the LCD/Speaker control sketch to the Uno.
4. **Run Inference:** Execute the main prediction script on the Raspberry Pi.

---

## 📂 Project Structure

```text
Project/
│
├── AI_Project.ipynb              # Main Code file
├── facial_recognition_model.h5   # Trained model weights
├── augmented_images.zip          # Dataset source
├── README.md                     # Documentation
│
├── data/                         # Extracted images
│   ├── train/                    # 5 Folders per person
│   └── test/                     # Validation set
│
└── test2.jpg                     # Sample test image

```
## 👨‍💻 My Contribution
- Implemented Raspberry Pi integration
- Worked on facial recognition pipeline
- Developed attendance tracking logic
