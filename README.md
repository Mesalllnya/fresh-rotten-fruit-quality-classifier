# Multi-Class Fresh and Rotten Fruit Detection (16 Classes)

Sistem klasifikasi kualitas dan kesegaran buah berbasis **Computer Vision** untuk membedakan buah segar (*fresh*) dan busuk (*rotten*) ke dalam **16 kelas** (8 jenis buah × 2 kondisi). Proyek ini dirancang untuk membantu petani, distributor, dan industri pengolahan buah dalam menyortir kualitas buah secara otomatis, akurat, dan efisien guna menekan kerugian ekonomi akibat pembusukan pascapanen.

## 📋 Daftar Isi

* [Latar Belakang](#-latar-belakang)

* [Deskripsi Dataset](#-deskripsi-dataset)

* [Anggota Tim](#-anggota-tim)

* [Alur Kerja Sistem (System Workflow)](#-alur-kerja-sistem-system-workflow)

* [Alur Pengerjaan Proyek (Project Roadmap)](#-alur-pengerjaan-proyek-project-roadmap)

* [Struktur Direktori](#-struktur-direktori)

* [Instalasi & Cara Menjalankan](#-instalasi--cara-menjalankan)

## 🎯 Latar Belakang

Sekitar sepertiga dari total buah yang diproduksi mengalami pembusukan seiring waktu sebelum sampai ke tangan konsumen, yang berdampak pada kerugian finansial besar serta penurunan kepercayaan pembeli. Proses penyortiran manual oleh manusia cenderung lambat, subjektif, dan tidak konsisten dalam skala besar. Melalui pendekatan *Computer Vision* dan *Machine Learning / Deep Learning*, sistem ini mengotomatisasi identifikasi kesegaran buah berdasarkan karakteristik visual pada citra.

## 📊 Deskripsi Dataset

Dataset yang digunakan dalam proyek ini terdiri dari citra buah segar dan busuk yang dikumpulkan dari toko buah serta lahan pertanian asli, dan telah divalidasi oleh pakar agrikultur.

* **Total Citra Asli:** 3.200 citra

* **Total Citra Hasil Augmentasi:** 12.335 citra (dihasilkan melalui teknik *rotation*, *flipping*, *zooming*, dan *shearing*)

* **Jumlah Kelas:** 16 kelas

| Jenis Buah | Kelas Segar (*Fresh*) | Kelas Busuk (*Rotten*) | 
| ----- | ----- | ----- | 
| **Apel (*Apple*)** | `fresh_apple` | `rotten_apple` | 
| **Pisang (*Banana*)** | `fresh_banana` | `rotten_banana` | 
| **Jeruk (*Orange*)** | `fresh_orange` | `rotten_orange` | 
| **Anggur (*Grape*)** | `fresh_grape` | `rotten_grape` | 
| **Jambu Biji (*Guava*)** | `fresh_guava` | `rotten_guava` | 
| **Jujube** | `fresh_jujube` | `rotten_jujube` | 
| **Delima (*Pomegranate*)** | `fresh_pomegranate` | `rotten_pomegranate` | 
| **Stroberi (*Strawberry*)** | `fresh_strawberry` | `rotten_strawberry` | 

## 👥 Anggota Tim

| No | Nama Anggota | NIM |
| ----- | ----- | ----- |
| 1 | **Muhamad Ifsal Fadhilah** | *(123240138)* |
| 2 | **Anggota 2** *(Isi Nama)* | *(Isi NIM)* |
| 3 | **Anggota 3** *(Isi Nama)* | *(Isi NIM)* |
| 4 | **Anggota 4** *(Isi Nama)* | *(Isi NIM)* |
| 5 | **Anggota 5** *(Isi Nama)* | *(Isi NIM)* |

## ⚙️ Alur Kerja Sistem (System Workflow)

Alur kerja teknis sistem pemrosesan citra hingga menghasilkan keputusan klasifikasi berjalan melalui tahapan berikut:

```
[Input Citra Buah] 
       │
       ▼
[1. Image Preprocessing] ──► Resize dimensi standar (mis. 224x224 px), konversi ruang warna (RGB/HSV), & normalisasi piksel
       │
       ▼
[2. Data Augmentation]   ──► Penerapan rotation, flipping, zooming, & shearing (khusus pada data latih)
       │
       ▼
[3. Feature Extraction]  ──► Ekstraksi pola visual (warna permukaan, bercak pembusukan, & tekstur kulit buah)
       │
       ▼
[4. Classification Model]──► Pemrosesan fitur melalui model terlatih untuk menghitung probabilitas 16 kelas
       │
       ▼
[Output Prediksi]        ──► Label Kelas (mis. "Fresh Apple" / "Rotten Banana") + Skor Kepercayaan (Confidence Score)

```

## 🗓️ Alur Pengerjaan Proyek (Project Roadmap)

Pengerjaan proyek dibagi ke dalam 6 fase terstruktur agar kolaborasi tim di GitHub berjalan rapi:

1. **Fase 1: Inisiasi & Manajemen Repositori**

   * Pembuatan struktur direktori proyek, setup `.gitignore`, konfigurasi *environment* (`requirements.txt`), dan pembagian *branch* kerja per anggota (`feature/eda`, `feature/preprocessing`, `feature/modeling`, `feature/evaluation`).

2. **Fase 2: Eksplorasi & Pemisahan Dataset (EDA & Splitting)**

   * Audit jumlah citra pada masing-masing dari 16 kelas.

   * Pemisahan ketat antara **3.200 citra asli** dan **12.335 citra augmentasi** sebelum *splitting* (80% Train, 10% Validation, 10% Test) untuk mencegah kebocoran data (*data leakage*) antara data latih dan data uji.

3. **Fase 3: Preprocessing & Pipeline Augmentasi**

   * Standarisasi ukuran resolusi gambar, pembersihan citra rusak (*corrupt files*), dan penerapan *pipeline* augmentasi (*rotation, flipping, zooming, shearing*).

4. **Fase 4: Pengembangan & Pelatihan Model (*Model Training*)**

   * Pembangunan *baseline model* dan model utama untuk klasifikasi 16 kelas.

   * Pemantauan grafik *training/validation accuracy* dan *loss* untuk mencegah *overfitting*.

5. **Fase 5: Evaluasi & Analisis Kesalahan (*Error Analysis*)**

   * Pengujian model pada *unseen test set*.

   * Analisis *Confusion Matrix* untuk mengidentifikasi kelas buah mana yang paling sering tertukar (misalnya tingkat kemiripan visual antara buah yang mulai matang dan mulai membusuk).

6. **Fase 6: Integrasi Akhir & Dokumentasi**

   * *Merge* seluruh *feature branch* ke *branch* `main` melalui *Pull Request*, pengujian ulang skrip *inference* secara *end-to-end*, dan finalisasi dokumentasi laporan.

## 📁 Struktur Direktori

```
multiclass-fruit-quality-vision/
├── data/                   # Direktori dataset (diabaikan di git jika ukuran besar)
│   ├── raw/                # 3.200 citra asli
│   └── augmented/          # 12.335 citra hasil augmentasi
├── notebooks/              # Jupyter / Google Colab notebooks untuk eksperimen
│   ├── 01_eda_dataset.ipynb
│   ├── 02_preprocessing_augmentation.ipynb
│   └── 03_model_training_evaluation.ipynb
├── src/                    # Kode sumber modular Python
│   ├── preprocess.py       # Fungsi resize, normalisasi, dan data loader
│   ├── model.py            # Definisi arsitektur model
│   ├── train.py            # Skrip pelatihan model
│   └── evaluate.py         # Skrip evaluasi dan visualisasi confusion matrix
├── results/                # Grafik training, confusion matrix, dan sampel prediksi
├── .gitignore              # Daftar file/folder yang tidak di-push ke GitHub
├── requirements.txt        # Daftar library Python yang dibutuhkan
└── README.md               # Dokumentasi utama proyek

```

## 🚀 Instalasi & Cara Menjalankan

1. **Clone repositori ini:**

   ```
   git clone https://github.com/<username-kamu>/multiclass-fruit-quality-vision.git
   cd multiclass-fruit-quality-vision
   
   ```

2. **Install dependensi yang diperlukan:**

   ```
   pip install -r requirements.txt
   
   ```

3. **Jalankan pipeline pelatihan atau evaluasi:**

   ```
   python src/train.py
   python src/evaluate.py
   
   ```
