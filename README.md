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
**Use it for:** quick benchmarking, sanity checks, comparing with speaker-independent protocol.

#### `AUDIO_03_modeling_SER_speaker_independent_v01.ipynb`
**Purpose:** Audio emotion recognition with **speaker/actor-independent split**.  
**Why it matters:** Ensures speakers in train do **not** appear in test → prevents leakage and reflects a **more realistic** scenario.  
**Use it for:** “final” SER evaluation, academically preferred protocol.

---

### 2) Visual Expert (FER)

#### `VISUAL_01_modeling_FER_CREMA-D_video_v01.ipynb`
**Purpose:** Facial emotion recognition from **CREMA-D video frames/faces**.  
**What it includes (high level):**
- video/frame data preparation helpers
- model training/evaluation for facial emotion recognition (FER)
- utilities for handling CREMA-D video splits

---

### 3) Multimodal Fusion (Audio + Visual)

#### `FUSION_02_multimodal_audio_visual_final_v01.ipynb`
**Purpose:** The final multimodal pipeline:  
- builds a **master split/manifest**
- loads **audio expert** outputs + **visual expert** outputs
- applies **fusion strategies** (e.g., weighted late fusion)
- reports final metrics and analysis

**Important:** This notebook previously contained a Hugging Face token and has been cleaned. No secrets are stored in this repo.

---

### 4) No-Code Demo Notebook (Run-Only)

#### `DEMO_00_multimodal_emotion_recognition_no_code_v01.ipynb`
**Purpose:** A single-cell / minimal demo notebook for running inference quickly.  
**Goal:** You can run the demo **without editing training pipelines**.

**What it expects:**
- pretrained checkpoints exist in predictable locations (see below)
- CREMA-D video/audio paths are accessible (e.g., via Google Drive in Colab)

---

### 5) Presentation

#### `PRESENTATION_multimodal_emotion_recognition_v01.pptx`
Project slides summarizing:
- problem definition
- methodology (SER/FER/fusion)
- experimental protocols
- results and conclusions

---

## Checkpoints & Large Files Policy

Model checkpoints are often too large for GitHub. If you keep them outside the repo, use a structure like:

```text
checkpoints/
├── best_wav2vec2_speaker_indep.pt
└── best_visual_model.keras
