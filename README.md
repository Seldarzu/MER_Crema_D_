# Multimodal Emotion Recognition (MER) — Audio (SER) + Visual (FER) + Fusion

This repository contains a complete **Multimodal Emotion Recognition (MER)** pipeline built on the **CREMA-D** dataset.

- **Audio modality (SER)**: trained and evaluated with **two protocols**
  - Random split (baseline / optimistic)
  - Speaker-independent (actor-independent, leakage-free / realistic)
- **Visual modality (FER)**: facial emotion recognition using **CREMA-D video**
- **Fusion**: combines audio + visual predictions (late fusion / weighted strategies)
- **Demo**: a single notebook to run an end-to-end inference demo **without modifying any training code**

---

## Repository Contents

### 1) Audio Expert (SER) — Two Evaluation Protocols

#### `AUDIO_03_modeling_SER_random_split_v01.ipynb`
**Purpose:** Audio emotion recognition with **random train/test split**.  
**Why it exists:** Provides a baseline that can be **optimistic** due to potential speaker leakage (same actor may appear in both train and test).  
**Use it for:** Quick benchmarking, sanity checks, and comparison with the speaker-independent protocol.

#### `AUDIO_03_modeling_SER_speaker_independent_v01.ipynb`
**Purpose:** Audio emotion recognition with **speaker/actor-independent split**.  
**Why it matters:** Ensures speakers in training do **not** appear in testing, preventing leakage and reflecting a **more realistic** scenario.  
**Use it for:** Final SER evaluation and academically preferred reporting.

---

### 2) Visual Expert (FER)

#### `VISUAL_01_modeling_FER_CREMA-D_video_v01.ipynb`
**Purpose:** Facial emotion recognition from **CREMA-D video frames/faces**.  

**Includes:**
- Video/frame preprocessing utilities
- FER model training and evaluation
- CREMA-D video split handling helpers

---

### 3) Multimodal Fusion (Audio + Visual)

#### `FUSION_02_multimodal_audio_visual_final_v01.ipynb`
**Purpose:** Final multimodal pipeline that:
- Builds a **master split / manifest**
- Loads predictions from **audio experts** and **visual experts**
- Applies **fusion strategies** (e.g., weighted late fusion)
- Reports final metrics and analysis

**Note:** This notebook previously contained a Hugging Face token and has been fully cleaned.  
No secrets are stored in this repository.

---

### 4) No-Code Demo Notebook (Run-Only)

#### `DEMO_00_multimodal_emotion_recognition_no_code_v01.ipynb`
**Purpose:** A minimal demo notebook for quick end-to-end inference.  

**Goal:** Run the full MER pipeline **without editing any training code**.

**Expected setup:**
- Pretrained checkpoints available at fixed paths
- CREMA-D audio/video paths accessible (e.g., Google Drive in Colab)

---

### 5) Presentation

#### `PRESENTATION_multimodal_emotion_recognition_v01.pptx`
Project presentation covering:
- Problem definition
- SER / FER / Fusion methodology
- Experimental protocols
- Results and conclusions

---

## Checkpoints & Large Files Policy

Trained model checkpoints are often too large for GitHub.

**Recommended external structure:**
```text
checkpoints/
├── best_wav2vec2_speaker_indep.pt
└── best_visual_model.keras
If demo notebooks reference these paths, keep filenames stable.

Recommended practice
Store checkpoints on Google Drive or Hugging Face Hub

Keep only code, notebooks, and figures in GitHub

Exclude checkpoints via .gitignore

Example .gitignore:

gitignore
Kodu kopyala
checkpoints/
*.pt
*.pth
*.keras
*.h5
How to Run
Option A — Google Colab (Recommended for Demo)
Clone or upload this repository to Colab

Mount Google Drive (if using Drive paths)

Place pretrained models under checkpoints/

Run:

DEMO_00_multimodal_emotion_recognition_no_code_v01.ipynb

Option B — Local Execution
Install required dependencies (PyTorch, Transformers, TensorFlow/Keras, OpenCV, etc.)

Ensure CREMA-D audio/video paths are correct

Run the demo notebook

Why Two SER Protocols?
This repository intentionally includes both protocols to demonstrate the impact of evaluation design:

Random split may inflate performance due to speaker leakage

Speaker-independent split is more challenging but realistic and academically preferred

Both are included for transparency and fair comparison.

Author
Arzu Selda Avcı
Computer Engineering — Multimodal Deep Learning / Emotion Recognition
