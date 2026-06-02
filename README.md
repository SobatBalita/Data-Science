# SobatBalita - Data Science Stunting dan Wasting

Repository ini berisi proses Data Science untuk pengolahan dataset tabular antropometri balita pada proyek **SobatBalita**. Dataset digunakan untuk mendukung pengembangan model Machine Learning yang memprediksi status **stunting** dan **wasting** berdasarkan data antropometri.

## Gambaran Umum

SobatBalita merupakan aplikasi web berbasis Artificial Intelligence yang dikembangkan untuk membantu proses skrining awal kesehatan balita. Pada bagian Data Science, fokus pekerjaan berada pada pengolahan data tabular yang berisi informasi jenis kelamin, umur, tinggi badan, berat badan, serta label status stunting dan wasting.

Tahapan utama yang dilakukan dalam notebook ini meliputi:

- Data gathering dan data understanding
- Data quality assessment
- Data cleaning
- Exploratory Data Analysis
- Explanatory analysis
- Feature engineering
- Data preprocessing
- Persiapan dataset untuk modeling

## Dataset

Dataset yang digunakan berasal dari Kaggle:

**Stunting Wasting Dataset (Synthetic)**  
https://www.kaggle.com/datasets/jabirmuktabir/stunting-wasting-dataset/data

Dataset ini merupakan dataset sintetis yang berisi data antropometri anak dengan fokus pada status stunting dan wasting. Meskipun dataset relatif sudah terstruktur, proses data cleaning tetap dilakukan untuk memastikan data bebas dari missing value, duplikasi, kategori tidak valid, serta nilai antropometri yang tidak realistis sebelum digunakan pada tahap analisis dan pemodelan.

## Struktur File

| File | Keterangan |
|---|---|
| `sobatbalita_stunting_wasting_data_science.ipynb` | Notebook utama untuk proses pengolahan dataset tabular, mulai dari data understanding, cleaning, EDA, feature engineering, hingga preprocessing. |
| `df_clean.csv` | Dataset hasil proses cleaning dasar. |
| `df_feat.csv` | Dataset hasil feature engineering dan preprocessing yang sudah disiapkan untuk tahap modeling. |
| `modeling_ML_stuntingWasting_fix.ipynb` | Notebook modeling Machine Learning untuk prediksi stunting dan wasting, jika disertakan dalam repository. |

## Alur Pengolahan Data

### 1. Data Gathering

Dataset dibaca dari Kaggle menggunakan file CSV utama dari dataset **Stunting Wasting Dataset (Synthetic)**. Dataset awal memiliki:

- 100.000 baris
- 6 kolom

Kolom awal pada dataset meliputi:

- `Jenis Kelamin`
- `Umur (bulan)`
- `Tinggi Badan (cm)`
- `Berat Badan (kg)`
- `Stunting`
- `Wasting`

### 2. Data Quality Assessment

Tahap ini dilakukan untuk mengecek kualitas dataset sebelum diproses lebih lanjut. Pemeriksaan yang dilakukan meliputi:

- Missing value
- Data duplikat
- Tipe data
- Konsistensi kategori
- Nilai minimum dan maksimum pada fitur numerik
- Nilai antropometri yang tidak realistis

Hasil assessment menunjukkan bahwa dataset tidak memiliki missing value, tetapi terdapat data duplikat yang perlu dihapus.

### 3. Data Cleaning

Tahap cleaning dilakukan untuk memastikan dataset memiliki struktur dan kualitas yang layak untuk analisis serta pemodelan.

Proses cleaning yang dilakukan meliputi:

- Normalisasi nama kolom
- Penghapusan data duplikat
- Pembersihan teks kategori
- Konversi kolom numerik
- Validasi kategori
- Validasi rentang nilai umur, tinggi badan, dan berat badan
- Pembulatan nilai numerik

Setelah proses cleaning dasar, dataset menghasilkan:

- `df_clean.csv`
- 92.692 baris

### 4. Exploratory Data Analysis

EDA dilakukan untuk memahami distribusi data dan hubungan antarvariabel. Analisis yang dilakukan meliputi:

- Distribusi status stunting
- Distribusi status wasting
- Hubungan umur dan tinggi badan terhadap status stunting
- Hubungan tinggi badan dan berat badan terhadap status wasting
- Korelasi antarfitur numerik
- Hubungan antara status stunting dan wasting

### 5. Feature Engineering

Feature engineering dilakukan untuk membuat fitur tambahan yang lebih informatif bagi model Machine Learning.

Fitur tambahan yang dibuat:

| Fitur | Keterangan |
|---|---|
| `kelompok_umur` | Kelompok usia balita berdasarkan umur dalam bulan. |
| `rasio_berat_tinggi` | Rasio berat badan terhadap tinggi badan. |
| `bmi` | Body Mass Index sebagai fitur tambahan proporsi tubuh. |
| `interaksi_tb_bb` | Fitur interaksi antara tinggi badan dan berat badan. |

Fitur `rasio_tinggi_umur` dan `rasio_berat_umur` tidak digunakan karena umur 0 bulan merupakan nilai valid pada data balita. Pembagian langsung terhadap umur dapat menghasilkan nilai tidak stabil.

### 6. Data Preprocessing

Tahap preprocessing dilakukan untuk menyiapkan dataset agar dapat digunakan pada tahap modeling.

Proses preprocessing meliputi:

- Encoding `jenis_kelamin`
- Mapping label `stunting` menjadi `stunting_target`
- Mapping label `wasting` menjadi `wasting_target`
- Pembuatan `stratify_label`
- Pemisahan fitur dan target
- Train-test split dengan stratifikasi

Setelah feature engineering dan validasi fitur, dataset akhir menghasilkan:

- `df_feat.csv`
- 91.998 baris
- 8 fitur input
- 2 target prediksi

## Penjelasan Output Dataset

### `df_clean.csv`

`df_clean.csv` adalah dataset hasil pembersihan data dasar. Dataset ini dibuat setelah dataset awal melalui proses cleaning seperti penghapusan duplikasi, normalisasi kolom, pembersihan kategori, konversi tipe data numerik, dan validasi nilai antropometri.

Dataset ini masih mempertahankan label kategori asli, seperti:

- `Normal`
- `Stunted`
- `Severely Stunted`
- `Tall`
- `Normal weight`
- `Underweight`
- `Severely Underweight`
- `Risk of Overweight`

### `df_feat.csv`

`df_feat.csv` adalah dataset lanjutan setelah proses feature engineering dan preprocessing. Dataset ini sudah berisi fitur tambahan dan target numerik yang dapat digunakan untuk proses modeling.

Kolom penting pada `df_feat.csv` meliputi:

- `jenis_kelamin`
- `umur_bulan`
- `tinggi_badan_cm`
- `berat_badan_kg`
- `kelompok_umur`
- `rasio_berat_tinggi`
- `bmi`
- `interaksi_tb_bb`
- `stunting_target`
- `wasting_target`
- `stratify_label`

## Data Dictionary

| Kolom | Keterangan |
|---|---|
| `jenis_kelamin` | Jenis kelamin balita. Pada tahap preprocessing diubah menjadi nilai numerik. |
| `umur_bulan` | Usia balita dalam bulan. |
| `tinggi_badan_cm` | Tinggi badan balita dalam sentimeter. |
| `berat_badan_kg` | Berat badan balita dalam kilogram. |
| `stunting` | Label status stunting dalam bentuk kategori. |
| `wasting` | Label status wasting dalam bentuk kategori. |
| `kelompok_umur` | Kelompok umur balita yang dibuat dari fitur umur. |
| `rasio_berat_tinggi` | Rasio berat badan terhadap tinggi badan. |
| `bmi` | Body Mass Index sebagai fitur tambahan proporsi tubuh. |
| `interaksi_tb_bb` | Fitur interaksi antara tinggi badan dan berat badan. |
| `stunting_target` | Target numerik untuk status stunting. |
| `wasting_target` | Target numerik untuk status wasting. |
| `stratify_label` | Kombinasi label stunting dan wasting untuk menjaga proporsi kelas saat train-test split. |

## Label Target

### Stunting

| Label | Keterangan |
|---|---|
| `Normal` | Tinggi badan sesuai dengan umur. |
| `Stunted` | Tinggi badan lebih rendah dari standar umur. |
| `Severely Stunted` | Tinggi badan jauh lebih rendah dari standar umur. |
| `Tall` | Tinggi badan lebih tinggi dari standar umur. |

### Wasting

| Label | Keterangan |
|---|---|
| `Normal weight` | Berat badan sesuai terhadap tinggi badan. |
| `Underweight` | Berat badan lebih rendah dari yang seharusnya. |
| `Severely Underweight` | Berat badan jauh lebih rendah dari yang seharusnya. |
| `Risk of Overweight` | Berat badan berisiko lebih tinggi terhadap tinggi badan. |

## Catatan Modeling

Pada tahap modeling, fitur training hanya menggunakan kolom input yang relevan, yaitu:

- `jenis_kelamin`
- `umur_bulan`
- `kelompok_umur`
- `tinggi_badan_cm`
- `berat_badan_kg`
- `rasio_berat_tinggi`
- `bmi`
- `interaksi_tb_bb`

Kolom berikut tidak dimasukkan ke dalam fitur training:

- `stunting_target`
- `wasting_target`
- `stratify_label`

`stunting_target` dan `wasting_target` digunakan sebagai target prediksi, sedangkan `stratify_label` hanya digunakan untuk menjaga proporsi kelas pada proses train-test split. Dengan demikian, proses modeling menghindari data leakage karena target tidak dimasukkan ke dalam fitur training.

## Catatan Penting

Model dan dataset dalam proyek ini digunakan untuk kebutuhan pembelajaran dan pengembangan sistem skrining awal. Hasil prediksi tidak dapat menggantikan pemeriksaan, diagnosis, atau saran medis dari tenaga kesehatan.
