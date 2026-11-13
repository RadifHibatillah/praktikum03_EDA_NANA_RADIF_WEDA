# Analisis Pola Dropout dan Keberhasilan Akademik Mahasiswa Pendidikan Tinggi

Repositori Proyek Kelompok Mata Kuliah **Exploratory Data Analysis (KMTI21133)** - Program Studi Teknik Informatika, STT Terpadu Nurul Fikri.

## 1. Tujuan & Latar Belakang Proyek
Tingkat putus kuliah (*dropout*) di perguruan tinggi berdampak langsung pada efisiensi institusi pendidikan dan keberlanjutan studi mahasiswa. Proyek ini bertujuan mengeksplorasi sejauh mana faktor kesulitan finansial (tunggakan biaya kuliah dan status debitur) berkaitan dengan risiko mahasiswa mengalami *dropout*, dibandingkan dengan faktor dukungan beasiswa, performa akademik semester awal (semester 1 dan 2), serta usia mahasiswa saat pertama kali mendaftar.

## 2. Pertanyaan Analisis

### Pertanyaan Payung
> *"Apakah masalah kesulitan finansial—khususnya tunggakan SPP dan status debitur—merupakan faktor yang paling berkaitan dengan tingginya risiko mahasiswa Dropout, jika dibandingkan dengan faktor dukungan beasiswa, performa akademik, dan usia saat mendaftar?"*

### Pertanyaan Turunan & Kolom Terkait
1. **Dampak Dukungan Beasiswa terhadap Kelulusan dan Dropout**
   - **Pertanyaan:** Apakah intervensi berupa pemberian beasiswa menghasilkan persentase kelulusan (`Graduate`) yang lebih tinggi sekaligus menekan angka `Dropout` pada mahasiswa dibandingkan mahasiswa non-beasiswa?
   - **Kolom yang digunakan:** `Scholarship holder`, `Tuition fees up to date`, `Debtor`, `Target`
2. **Pola Performa Akademik Semester 1 dan Semester 2**
   - **Pertanyaan:** Bagaimana perbandingan performa akademik di semester 1 dan semester 2 antara mahasiswa yang `Dropout` dan `Graduate`, serta apakah penurunan nilai antarsemester merupakan indikator kuat sebelum mahasiswa `Dropout`?
   - **Kolom yang digunakan:** `Curricular units 1st sem (grade)`, `Curricular units 2nd sem (grade)`, `Curricular units 1st sem (approved)`, `Curricular units 2nd sem (approved)`, `Target`
3. **Kerentanan Dropout Berdasarkan Usia Saat Mendaftar**
   - **Pertanyaan:** Apakah mahasiswa yang mendaftar pada usia yang lebih tua memiliki tingkat kerentanan `Dropout` yang lebih besar dibandingkan mahasiswa reguler yang mendaftar di usia muda?
   - **Kolom yang digunakan:** `Age at enrollment`, `Daytime/evening attendance`, `Marital status`, `Target`

## 3. Sumber Data & Akses
- **Nama Dataset:** Predict Students' Dropout and Academic Success
- **Sumber Primer:** UCI Machine Learning Repository / Realinho et al. (Instituto Politécnico de Portalegre, Portugal)
- **Lisensi:** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Ukuran Dataset:** 4.424 baris × 35 variabel (34 variabel prediktor numerik/kategorikal terkode dan 1 variabel target kategorikal).
- **Penanganan Privasi:** Dataset sudah teranonimisasi penuh dari sumber primer dan tidak memuat kolom identitas langsung (nama, nomor induk mahasiswa, alamat, maupun kontak pribadi).

## 4. Struktur Repositori
```text
nama-proyek-tim/
├── README.md                 # Dokumentasi utama, pertanyaan analisis, panduan, & pembagian peran
├── requirements.txt          # Daftar pustaka Python beserta versinya
├── data_dictionary.md        # Kamus data (nama, tipe, satuan, deskripsi, sumber, privasi)
├── cleaning_log.md           # Log keputusan pembersihan data (M2)
├── AI_usage_log.md           # Log transparansi penggunaan AI generatif (M1-M5)
├── data/
│   ├── raw/                  # Data asli/mentah (DILARANG DIUBAH/DITIMPA)
│   └── processed/            # Data bersih hasil pemrosesan notebook (M2)
├── notebooks/
│   ├── 01_quality.ipynb      # Diagnosis kualitas data (M2)
│   ├── 02_cleaning.ipynb     # Pembersihan dan validasi data (M2)
│   ├── 03_univariate.ipynb   # Analisis univariat: distribusi, sebaran, outlier (M3)
│   ├── 04_multivariate.ipynb # Analisis bivariat & multivariat (M3)
│   └── 05_advanced.ipynb     # Analisis lanjut: regresi, clustering, PCA (M5)
├── knime/
│   └── workflow.knwf         # Workflow KNIME (M4)
└── reports/
    ├── figures/              # Grafik ekspor yang dipakai di laporan
    └── [Laporan & Slide PDF] # Proposal M1, DQR M2, Slide M3, Catatan M4, Laporan & Slide M5

```

## 5. Cara Menjalankan (Reproduktibilitas)

Seluruh path berkas menggunakan path relatif dari root repositori.

1. **Clone repositori:**
```bash
git clone <URL-Repositori-Tim>
cd <nama-proyek-tim>

```


2. **Buat virtual environment & install pustaka:**
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

```


3. **Urutan Eksekusi Notebook (*Restart & Run All*):**
* `notebooks/01_quality.ipynb` — Diagnosis kualitas data mentah dari `data/raw/`
* `notebooks/02_cleaning.ipynb` — Pembersihan, validasi, dan ekspor ke `data/processed/`
* `notebooks/03_univariate.ipynb` — Analisis distribusi, sebaran, dan outlier tiap variabel
* `notebooks/04_multivariate.ipynb` — Analisis korelasi, crosstab, dan hubungan antarvariabel
* `notebooks/05_advanced.ipynb` — Analisis eksploratif lanjutan


4. **Menjalankan Workflow KNIME (M4):**
* Buka KNIME Analytics Platform, import `knime/workflow.knwf`, dan jalankan menggunakan dataset pada folder `data/raw/`.



## 6. Tim & Pembagian Peran

Tim terdiri atas 3 mahasiswa dengan pembagian fokus analisis serta rotasi peran utama pada setiap milestone.

| Nama Anggota | Fokus Pengerjaan & Kontribusi Utama |
| --- | --- |
| **M. Radifah Hibatillah** | Ketua tim & koordinasi teknis, pipeline *data cleaning* (`01_quality` & `02_cleaning`), pengelolaan repositori, serta analisis eksplorasi **Pertanyaan Turunan 2 & 3** |
| **Klaudia Weda** | Penyusunan laporan lengkap (M1–M5), kurasi visualisasi & *data storytelling*, sintesis **Pertanyaan Payung**, serta penyusunan slide presentasi |
| **Anastasya Nadhia Amelia** | Dokumentasi kamus data & log transparansi AI, validasi kualitas laporan, serta analisis eksplorasi **Pertanyaan Turunan 1** dan analisis lanjutan |

### Rotasi Peran Resmi per Milestone

| Milestone | Koordinator | Data Engineer | Analis | Penulis / Visual Designer |
| --- | --- | --- | --- | --- |
| **M1** (Proposal & Akuisisi) | M. Radifah Hibatillah | Anastasya Nadhia Amelia | M. Radifah Hibatillah | Klaudia Weda |
| **M2** (Data Quality Report) | Klaudia Weda | M. Radifah Hibatillah | Anastasya Nadhia Amelia | Klaudia Weda |
| **M3** (EDA Tahap 1) | Anastasya Nadhia Amelia | M. Radifah Hibatillah | M. Radifah Hibatillah & Anastasya Nadhia Amelia | Klaudia Weda |
| **M4** (Workflow KNIME) | M. Radifah Hibatillah | Anastasya Nadhia Amelia | Klaudia Weda | M. Radifah Hibatillah |
| **M5** (Produk Akhir) | Klaudia Weda | M. Radifah Hibatillah | Anastasya Nadhia Amelia | Klaudia Weda |
