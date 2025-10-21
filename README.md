# Face Mask Detection System 🎭😷

A real-time face mask detection system built using Python, OpenCV, and Deep Learning. This project can detect whether a person is wearing a mask, not wearing a mask, or wearing it incorrectly in images, video streams, and through webcam feed.



---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Technology Stack](#technology-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Dataset](#dataset)
- [Model Architecture](#model-architecture)
- [Results](#results)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)

---

## 🧠 Overview

This project uses a Convolutional Neural Network (CNN) to classify whether a person is wearing a face mask correctly. The system can be deployed for real-time monitoring in public spaces, entrances, or any area where mask compliance is required.

**Use Cases:**
- Public health monitoring
- Entrance control systems
- Smart city applications
- COVID-19 safety compliance

---

## ✨ Features

- **Real-time Detection:** Processes webcam feed at 25-30 FPS
- **Multi-class Classification:** Detects three states:
  - ✅ **Mask Worn Correctly**
  - ⚠️ **Mask Worn Incorrectly** (chin/nose exposed)
  - ❌ **No Mask**
- **Multiple Face Detection:** Can detect multiple faces in a single frame
- **Cross-platform:** Works on Windows, Linux, and macOS
- **Easy Deployment:** Simple setup and execution

---

## ⚙️ How It Works

1. **Face Detection:** Uses Haar Cascades or MTCNN to detect faces in the frame
2. **Preprocessing:** Crops, resizes, and normalizes the detected face regions
3. **Classification:** Passes the processed face through a trained CNN model
4. **Visualization:** Draws bounding boxes and labels with color coding:
   - **Green:** Mask worn correctly
   - **Yellow:** Mask worn incorrectly  
   - **Red:** No mask detected

---

## 🛠 Technology Stack

- **Python 3.8+** - Programming language
- **OpenCV** - Computer vision and image processing
- **TensorFlow/Keras** - Deep learning framework
- **NumPy** - Numerical computations
- **Matplotlib** - Data visualization
- **Streamlit** (Optional) - Web interface

---

## 📥 Installation

### Prerequisites
- Python 3.8 or higher
- Webcam (for real-time detection)

### Step-by-Step Setup

1. **Clone the repository**
```bash
git clone https://github.com/padhu113118/face-mask-detection.git
cd face-mask-detection



