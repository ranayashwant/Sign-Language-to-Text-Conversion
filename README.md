# 🤟 Sign Language to Text Conversion

<p align="center">
  <img src="data/Screenshot 2024-08-14 at 12.41.27 PM.png" alt="Sign Language Detection Demo" width="700"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Type-Final%20Year%20Project-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/College-DSMNRU%202024-orange?style=for-the-badge" />
</p>

> A real-time hand gesture recognition system that converts sign language gestures to text using webcam input — built as a Final Year Project to improve accessibility for hearing-impaired users.

---

## 🧩 Problem Statement

Deaf and mute individuals rely on sign language to communicate, but most people around them don't understand it. Existing translation tools are either expensive, require special hardware, or don't work in real-time.

This project solves that using just a **webcam** — no special hardware needed.

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-FF6F00?style=for-the-badge&logo=google&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)

---

## ⚙️ How It Works — Pipeline

```
Webcam Feed
    │
    ▼
MediaPipe Hand Detection  ──►  Extract 21 Landmark Coordinates (x, y per point)
    │
    ▼
Normalize Landmarks  ──►  Remove position bias, focus on gesture shape only
    │
    ▼
Random Forest Classifier  ──►  Predict gesture class (A / B / C / D)
    │
    ▼
Display Label + Bounding Box on Screen in Real-Time
```

### 📄 File-by-File Breakdown

| File | What it does |
|---|---|
| `collect_imgs.py` | Opens webcam, captures images for each gesture class and saves to dataset folder |
| `create_dataset.py` | Reads saved images, extracts 21 hand landmarks per image using MediaPipe, saves to `.pickle` |
| `train_classifier.py` | Loads landmark data, trains a Random Forest model, evaluates accuracy, saves model |
| `inference_classifier.py` | Loads trained model, runs real-time webcam detection with bounding box and predicted label |

---

## 📁 Dataset

<p align="center">
  <img src="data/2/0.jpg" alt="Dataset Sample" width="600"/>
</p>

- **400 images** collected manually using webcam (100 per class)
- **4 gesture classes:** A, B, C, D
- Images captured across varied lighting and hand positions for robustness
- Hand landmark coordinates (21 points × x,y = 42 features) extracted and normalized using **MediaPipe**
- Final dataset saved as a `.pickle` file for fast model training

---

## 📊 Results

| Metric | Score |
|---|---|
| Classification Accuracy | X% *(update after final test run)* |
| Gesture Classes | 4 (A, B, C, D) |
| Training Images | 400 |
| Inference Speed | Real-time (webcam) |

---

## 🚀 How to Run

### 1. Clone the repo
```bash
git clone https://github.com/ranayashwant/sign-language-to-text.git
cd sign-language-to-text
```

### 2. Install dependencies
```bash
pip install opencv-python mediapipe scikit-learn
```

### 3. Collect your own images *(optional — skip if using included dataset)*
```bash
python collect_imgs.py
```

### 4. Create dataset from images
```bash
python create_dataset.py
```

### 5. Train the classifier
```bash
python train_classifier.py
```

### 6. Run real-time inference
```bash
python inference_classifier.py
```

> Make sure your webcam is connected and working before running inference.

---

## 🗂️ Project Structure

```
sign-language-to-text/
├── data/                        # Collected gesture images
│   ├── A/
│   ├── B/
│   ├── C/
│   └── D/
├── images/                      # README screenshots
│   ├── demo.png
│   └── dataset.png
├── collect_imgs.py              # Step 1: Collect webcam images
├── create_dataset.py            # Step 2: Extract landmarks → pickle
├── train_classifier.py          # Step 3: Train Random Forest
├── inference_classifier.py      # Step 4: Real-time detection
├── model.p                      # Trained model (pickle)
└── README.md
```

---

## 🔮 Future Improvements

- [ ] Expand to full ASL alphabet (A–Z)
- [ ] Add word-level prediction (not just individual letters)
- [ ] Build a simple web UI using Flask + WebRTC
- [ ] Support for dynamic gestures (movement-based signs)

---

## 👤 Author

**Rana Yashwant Singh**
- 🔗 [LinkedIn](https://linkedin.com/in/ranayashwant) · [GitHub](https://github.com/ranayashwant)
- 📧 yashwant2609@gmail.com

---

## 📄 License

This project is licensed under the MIT License.
