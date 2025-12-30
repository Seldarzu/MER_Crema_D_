## README_TR.md (TR) — MER Repo Final

```markdown
# Çok Modlu Duygu Tanıma (MER) — Ses (SER) + Görüntü (FER) + Füzyon

Bu repository, **CREMA-D** veri seti üzerinde kurulmuş uçtan uca bir
**Multimodal Emotion Recognition (MER)** sistemini içerir.

- **Ses (SER)**: iki farklı protokol ile eğitim/değerlendirme
  - Random split (baseline / iyimser)
  - Speaker/actor-independent split (sızıntısız / gerçekçi)
- **Görüntü (FER)**: CREMA-D video üzerinden yüz tabanlı duygu tanıma
- **Füzyon**: ses + görüntü tahminlerini birleştirme (late fusion / weighted)
- **Demo**: eğitim kodlarına dokunmadan hızlıca inference çalıştırma

---

## Repository İçeriği

### 1) Ses Uzmanı (SER) — 2 Ayrı Değerlendirme Protokolü

#### `AUDIO_03_modeling_SER_random_split_v01.ipynb`
**Amaç:** Random train/test split ile ses duygu tanıma.  
**Neden var?** Aynı konuşmacı/aktör hem train hem test’e düşebileceği için
sonuçlar **iyimser** olabilir (speaker leakage riski).  
**Ne için kullanılır?** Hızlı baseline, karşılaştırma, sanity check.

#### `AUDIO_03_modeling_SER_speaker_independent_v01.ipynb`
**Amaç:** Speaker/actor-independent split ile ses duygu tanıma.  
**Neden önemli?** Train’deki konuşmacı test’te **asla bulunmaz** → leakage yok,
daha **gerçekçi** ve akademik olarak tercih edilen protokol.  
**Ne için kullanılır?** “Final” SER değerlendirmesi.

---

### 2) Görsel Uzman (FER)

#### `VISUAL_01_modeling_FER_CREMA-D_video_v01.ipynb`
**Amaç:** CREMA-D video verisi üzerinden yüz tabanlı duygu tanıma (FER).  
**İçerik (genel):**
- video/frame veri hazırlığı yardımcıları
- FER modeli eğitimi/değerlendirmesi
- CREMA-D video split yardımcı fonksiyonları

---

### 3) Multimodal Füzyon (Ses + Görüntü)

#### `FUSION_02_multimodal_audio_visual_final_v01.ipynb`
**Amaç:** Nihai multimodal sistem:
- master manifest/split oluşturma
- audio expert + visual expert çıktıları
- weighted late fusion vb. füzyon stratejileri
- final metrik raporlama

Not: Bu dosyada daha önce HF token bulunuyordu, temizlendi. Repo’da secret yok.

---

### 4) Kod Değiştirmeden Demo (Run-Only)

#### `DEMO_00_multimodal_emotion_recognition_no_code_v01.ipynb`
**Amaç:** Eğitim kodlarına dokunmadan hızlı demo çalıştırmak.  
**Beklenti:** Checkpoint dosyaları belirli path’lerde bulunmalı (aşağıya bak).

---

### 5) Sunum

#### `PRESENTATION_multimodal_emotion_recognition_v01.pptx`
Proje sunumu:
- problem tanımı
- SER/FER/fusion metodolojisi
- protokoller
- sonuçlar

---

## Checkpoint / Büyük Dosya Politikası

Model checkpoint’leri GitHub için genelde büyük olur. Önerilen yapı:

```text
checkpoints/
├── best_wav2vec2_speaker_indep.pt
└── best_visual_model.keras
✅ Öneri:

Checkpoint’leri Drive / Hugging Face Hub’da tut

GitHub’da notebook/kod/rapor olsun

.gitignore ile checkpoint’leri dışarıda bırak

Örnek .gitignore:

gitignore
checkpoints/
*.pt
*.pth
*.keras
*.h5
Çalıştırma Önerisi
Seçenek A — Google Colab (demo için en iyi)
Repo’yu Colab’a al/clone et

Drive mount (kullanıyorsan)

checkpoints/ klasörüne modelleri koy (veya demo içindeki path’leri güncelle)

DEMO_00_multimodal_emotion_recognition_no_code_v01.ipynb çalıştır

Seçenek B — Local
Gerekli kütüphaneleri kur (PyTorch, Transformers, TensorFlow/Keras, OpenCV vb.)

CREMA-D path’lerini doğru ayarla

Demo notebook’u çalıştır

Neden 2 SER Protokolü Var?
Bu repo “yüksek skor” peşinde değil, doğru değerlendirme peşinde:

Random split → leakage riski yüzünden skor şişebilir

Speaker-independent → zor ama gerçekçi ve akademik olarak daha doğru

İkisi de karşılaştırma ve şeffaf raporlama için tutuluyor.

Hazırlayan
Arzu Selda Avcı — Bilgisayar Mühendisliği
Multimodal Deep Learning / Emotion Recognition
