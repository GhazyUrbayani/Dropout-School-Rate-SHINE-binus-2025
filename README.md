# 🏆 Si Data Tuh - Prediksi Angka Putus Sekolah (DSC 2025)

![Banner](https://img.shields.io/badge/Kompetisi-Rumpun%20Penalaran%202025-blue) ![Status](https://img.shields.io/badge/Peringkat-%234%20Leaderboard-success)

Proyek ini adalah solusi dari tim **"Si Data Tuh"** untuk **Data Science Competition (DSC)**, bagian dari Rumpun Day Penalaran 2025 yang diselenggarakan oleh BINUS University. Kami berhasil meraih **Peringkat #4** dengan membangun model *machine learning* untuk memprediksi angka putus sekolah di Amerika Serikat.

### 💻 Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white">
  <img src="https://img.shields.io/badge/Numpy-013243?style=for-the-badge&logo=numpy&logoColor=white">
  <img src="https://img.shields.io/badge/LightGBM-4169E1?style=for-the-badge&logo=lightgbm&logoColor=white">
  <img src="https://img.shields.io/badge/Matplotlib-007ACC?style=for-the-badge&logo=matplotlib&logoColor=white">
  <img src="https://img.shields.io/badge/Seaborn-34495E?style=for-the-badge&logo=seaborn&logoColor=white">
</p>

---

### 🎯 Konteks & Tantangan Kompetisi

Kompetisi ini mengusung tema **SHINE** dengan fokus pada **Sustainable Development Goal (SDG) 4: Pendidikan Berkualitas**. Tantangan utamanya adalah mengatasi tingginya angka putus sekolah (*dropout rate*) sebagai salah satu penghambat utama kesetaraan pendidikan.

Tujuan utama dari proyek ini adalah:
* **Mengidentifikasi Faktor Risiko:** Menganalisis faktor-faktor yang paling berkontribusi terhadap tingginya angka putus sekolah.
* **Membangun Model Prediktif:** Membuat model *machine learning* yang akurat untuk memprediksi `dropout_rate_percent` pada dataset sekolah.
* **Mendorong Solusi Berbasis Data:** Menumbuhkan solusi yang dapat digunakan untuk merancang program mitigasi angka putus sekolah yang lebih efektif.

---

### 📋 Daftar Isi
1. [Hasil Akhir](#hasil-akhir)
2. [Pendekatan Kami](#pendekatan-kami)
3. [Struktur Repositori](#struktur-repositori)
4. [Dataset dan Metrik](#dataset-dan-metrik)
5. [Instalasi dan Penggunaan](#instalasi-dan-penggunaan)
6. [Tim Kami](#tim-kami)
7. [Lisensi](#lisensi)

---

### ✨ Hasil Akhir

Kami berhasil menyelesaikan kompetisi di **Peringkat #4** pada Leaderboard. Model final kami yang merupakan *ensemble* dari beberapa konfigurasi **GradientBoostingRegressor** berhasil mencapai skor **Mean Absolute Error (MAE) rata-rata 3.8223** pada validasi silang 5-fold.

---

### 🚀 Pendekatan Kami

Solusi kami dibangun melalui beberapa tahapan sistematis, yang tercermin dalam notebook `Si_Data_Tuh__Notebook.ipynb`.

#### 1. Analisis Data Eksploratif (EDA)
- **Analisis Korelasi:**
  - **Pearson (Numerik):** `percent_low_income` menunjukkan korelasi positif terkuat dengan `dropout_rate_percent`.
  - **Cramer's V (Kategorikal):** `grade_level` memiliki hubungan paling signifikan dengan variabel kategorikal lainnya.
- **Distribusi Data:** Kami menganalisis distribusi setiap fitur untuk memahami karakteristiknya dan mengidentifikasi adanya *outlier*.

#### 2. Feature Engineering
Kami membuat beberapa fitur baru untuk menangkap interaksi dan rasio yang lebih kompleks, di antaranya:
- `funding_per_teacher`: Interaksi antara pendanaan per siswa dan rasio murid-guru.
- `low_income_minority_interaction`: Interaksi antara persentase siswa berpenghasilan rendah dan minoritas.
- `score_to_funding_ratio`: Rasio antara skor tes rata-rata dengan pendanaan per siswa.
- `is_high_school`, `is_middle_school`, `is_elementary_school`: Fitur biner berdasarkan kata kunci pada nama sekolah untuk menangkap informasi tingkat pendidikan.

#### 3. Preprocessing & Modeling Pipeline
Kami membangun `Pipeline` menggunakan Scikit-learn untuk memastikan konsistensi dan reprodusibilitas alur kerja.
- **Imputasi:** `SimpleImputer` dengan strategi `mean` untuk fitur numerik dan `most_frequent` untuk fitur kategorikal.
- **Scaling:** `MinMaxScaler` untuk menormalisasi fitur numerik ke dalam rentang [0, 1].
- **Encoding:** `OneHotEncoder` untuk mengubah fitur kategorikal menjadi representasi numerik.
- **Model:** Setelah bereksperimen dengan berbagai model, `GradientBoostingRegressor` terpilih karena performanya yang stabil dan kuat.

#### 4. Ensembling
Untuk meningkatkan stabilitas dan akurasi, model final kami adalah **rata-rata prediksi (ensemble) dari tiga pipeline `GradientBoostingRegressor` terbaik** yang memiliki sedikit perbedaan dalam konfigurasi *scaler* dan *feature engineering*.

---

### 📂 Struktur Repositori

- ├── Si_Data_Tuh__Notebook.ipynb # Notebook utama dengan solusi final (Preprocessing, FE, dan Ensembling)
- ├── drafts/ # Folder berisi notebook eksperimen dan draf awal
- │ ├── binus.ipynb
- │ └── binus_FIX.ipynb
- ├── train_dataset.csv # Dataset training
- ├── test_dataset.csv # Dataset testing
- └── README.md # Anda sedang membacanya

Folder **`drafts`** berisi semua iterasi awal dan eksperimen. Solusi akhir yang menghasilkan submission terbaik berada di `Si_Data_Tuh__Notebook.ipynb`.

---

### 📊 Dataset dan Metrik

#### Deskripsi Dataset
Dataset ini mencakup berbagai indikator dari 1.000 sekolah di Amerika Serikat.

| Kolom | Deskripsi |
| :--- | :--- |
| `id` | ID unik sekolah |
| `school_name` | Nama sekolah |
| `state` | Negara bagian |
| `school_type` | Tipe sekolah (Public, Private, Charter) |
| `grade_level` | Tingkat pendidikan (Elementary, Middle, High) |
| `funding_per_student_usd` | Pendanaan tahunan per siswa (USD) |
| `avg_test_score_percent` | Rata-rata nilai ujian (%) |
| `student_teacher_ratio` | Rasio murid terhadap guru |
| `percent_low_income` | Persentase siswa berpenghasilan rendah (%) |
| `percent_minority` | Persentase siswa minoritas (%) |
| `internet_access_percent` | Persentase akses internet (%) |
| `dropout_rate_percent` | **Angka putus sekolah (Target)** (%) |

#### Metrik Evaluasi
Metrik evaluasi yang digunakan adalah **Mean Absolute Error (MAE)**. Semakin rendah nilai MAE, semakin akurat prediksi model.

$$MAE = \frac{1}{n}\sum_{i=1}^{n}\left | y_i - \hat{y}_i \right |$$

---

### 🛠️ Instalasi dan Penggunaan
Untuk mereplikasi hasil kami, ikuti langkah-langkah berikut:

0.  **Clone repositori ini:**
    ```bash
    git clone [URL_REPOSITORI_ANDA]
    cd [NAMA_FOLDER_REPOSITORI]
    ```

1.  **Buat dan aktifkan virtual environment (direkomendasikan):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Untuk Windows: venv\Scripts\activate
    ```

2.  **Install dependensi yang dibutuhkan:**
    Pastikan Anda memiliki *library* berikut terinstal. Anda bisa menginstalnya menggunakan satu perintah pip:
    ```bash
    pip install pandas numpy scikit-learn lightgbm joblib scipy matplotlib seaborn jupyter
    ```

3.  **Jalankan Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
    Buka file `Si_Data_Tuh__Notebook.ipynb` dan jalankan semua cell untuk melihat proses dan menghasilkan file `submission.csv`.

---

### 👨‍💻 Tim Kami
- **Mudzaki K Hakim**
- **Ghazy Achmed M Urbayani**
- **Mahesa F Andre**

---

### 📜 Lisensi
Proyek ini dilisensikan di bawah [MIT License](LICENSE).
