# Multi-Class Fresh and Rotten Fruit Detection (16 Classes)

Sistem klasifikasi kualitas dan kesegaran buah berbasis **Computer Vision** untuk membedakan buah segar (*fresh*) dan busuk (*rotten*) ke dalam **16 kelas** (8 jenis buah × 2 kondisi). Proyek ini dirancang untuk membantu petani, distributor, dan industri pengolahan buah dalam menyortir kualitas buah secara otomatis, akurat, dan efisien guna menekan kerugian ekonomi akibat pembusukan pascapanen.

Aplikasi ini dilengkapi dengan antarmuka web interaktif berbasis **Streamlit** untuk mempermudah pengguna mengunggah citra buah dan mendapatkan hasil klasifikasi beserta tingkat keyakinan (*confidence score*) secara *real-time*.

## 📋 Daftar Isi

* [Latar Belakang](#-latar-belakang)
* [Deskripsi Dataset](#-deskripsi-dataset)
* [Anggota Tim](#-anggota-tim)
* [Alur Kerja Sistem (System Workflow)](#-alur-kerja-sistem-system-workflow)
* [Alur Pengerjaan Proyek (Project Roadmap)](#-alur-pengerjaan-proyek-project-roadmap)
* [Aplikasi Web Streamlit](#-aplikasi-web-streamlit)
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
| 1 | **Muhamad Ifsal Fadhilah** | *123240138* |
| 2 | **Muhammad Affan Musyafa'**  | *123240155* |
| 3 | **Firraz Muhammad Raihan Daffa**  | *123240170* |
| 4 | **Mufid Dhamarjati Kusuma**  | *123240171* |
| 5 | **Reno Miftahudin**  | *123240248* |

## ⚙️ Alur Kerja Sistem (System Workflow)

Alur kerja teknis sistem pemrosesan citra hingga menghasilkan keputusan klasifikasi berjalan melalui tahapan berikut:

```
[Input Citra Buah (Web Streamlit)] 
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
       │
       ▼
[Antarmuka Streamlit]    ──► Visualisasi hasil prediksi, confidence level, dan probabilitas kelas secara interaktif
```

## 🗓️ Alur Pengerjaan Proyek (Project Roadmap)

Pengerjaan proyek dibagi ke dalam 6 fase terstruktur agar kolaborasi tim di GitHub berjalan rapi:

1. **Fase 1: Inisiasi & Manajemen Repositori**
   * Pembuatan struktur direktori proyek, setup `.gitignore`, konfigurasi *environment* (`requirements.txt`), dan pembagian *branch* kerja per anggota (`feature/eda`, `feature/preprocessing`, `feature/modeling`, `feature/streamlit-ui`).

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

6. **Fase 6: Integrasi Aplikasi Web Streamlit & Dokumentasi**
   * Pengembangan antarmuka interaktif berbasis **Streamlit** (`app.py`) untuk mempermudah pengujian inferensi model langsung melalui web browser.
   * *Merge* seluruh *feature branch* ke *branch* `main` melalui *Pull Request*, pengujian ulang inferensi aplikasi secara *end-to-end*, dan finalisasi dokumentasi laporan.

## 🌐 Aplikasi Web Streamlit

Aplikasi inferensi dibangun menggunakan [Streamlit](https://streamlit.io/) untuk memberikan antarmuka visual interaktif yang ramah pengguna:

* **Unggah Citra Langsung:** Mendukung format file citra (`.jpg`, `.jpeg`, `.png`) dengan mekanisme *drag-and-drop*.
* **Pratinjau Citra (*Image Preview*):** Menampilkan citra buah yang diunggah secara langsung di antarmuka.
* **Hasil Klasifikasi Real-time:** Menampilkan jenis buah dan status kesegarannya (**Fresh** atau **Rotten**).
* **Skor Kepercayaan (*Confidence Score*):** Menampilkan persentase tingkat kepastian model terhadap prediksi beserta grafik probabilitas kelas kandidat.

## 📁 Struktur Direktori

```
fresh-rotten-fruit-quality-classifier/
├── data/                   # Direktori dataset (diabaikan di git jika ukuran besar)
│   ├── raw/                # 3.200 citra asli
│   └── augmented/          # 12.335 citra hasil augmentasi
├── models/                 # Model terlatih (.h5 / .pt / .pkl)
├── notebooks/              # Jupyter / Google Colab notebooks untuk eksperimen
│   ├── 01_eda_dataset.ipynb
│   ├── 02_preprocessing_augmentation.ipynb
│   └── 03_model_training_evaluation.ipynb
├── src/                    # Kode sumber modular Python
│   ├── preprocess.py       # Fungsi resize, normalisasi, dan data loader
│   ├── model.py            # Definisi arsitektur model
│   ├── train.py            # Skrip pelatihan model
│   └── evaluate.py         # Skrip evaluasi dan visualisasi confusion matrix
├── app.py                  # Aplikasi Web Interaktif Streamlit
├── results/                # Grafik training, confusion matrix, dan sampel prediksi
├── .gitignore              # Daftar file/folder yang tidak di-push ke GitHub
├── requirements.txt        # Daftar library Python (termasuk streamlit)
└── README.md               # Dokumentasi utama proyek
```

## 🚀 Instalasi & Cara Menjalankan

1. **Clone repositori ini:**

   ```bash
   git clone https://github.com/Mesalllnya/fresh-rotten-fruit-quality-classifier.git
   cd fresh-rotten-fruit-quality-classifier
   ```

2. **Install dependensi yang diperlukan:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Jalankan Aplikasi Web Streamlit:**

   ```bash
   streamlit run app.py
   ```

4. **(Opsional) Menjalankan pipeline pelatihan atau evaluasi:**

   ```bash
   python src/train.py
   python src/evaluate.py
   ```
