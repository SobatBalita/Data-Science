# SobatBalita - Data Science Stunting dan Wasting

Repository ini berisi proses Data Science untuk pengolahan dataset tabular antropometri balita pada proyek **SobatBalita**. Dataset digunakan untuk mendukung pengembangan model Machine Learning yang memprediksi status **stunting** dan **wasting** berdasarkan data antropometri.

## Gambaran Umum

SobatBalita merupakan aplikasi web berbasis Artificial Intelligence untuk membantu proses skrining awal kesehatan balita. Pada bagian Data Science, fokus pekerjaan berada pada pengolahan data tabular yang berisi informasi jenis kelamin, umur, tinggi badan, berat badan, serta label status stunting dan wasting.

Tahapan utama yang dilakukan meliputi:

- Data gathering dan data understanding
- Data quality assessment
- Data cleaning
- Exploratory Data Analysis
- Explanatory analysis
- Feature engineering
- Data preprocessing
- Persiapan dataset untuk modeling

## Dataset

Sumber awal dataset berasal dari Kaggle:

**Stunting Wasting Dataset (Synthetic)**  
https://www.kaggle.com/datasets/jabirmuktabir/stunting-wasting-dataset/data

Pada notebook ini, dataset yang digunakan adalah versi hasil **noise injection**. Noise injection dilakukan untuk menyimulasikan kondisi data yang lebih realistis, karena data pada praktik nyata tidak selalu bersih dan dapat mengandung nilai kosong, duplikasi, kategori tidak valid, maupun nilai pengukuran yang tidak realistis.

Dengan menggunakan versi tersebut, proses data quality assessment, data cleaning, dan preprocessing dapat dilakukan secara lebih bermakna sebelum dataset digunakan dalam proses pemodelan Machine Learning.

## Struktur File

| File | Keterangan |
|---|---|
| `Wasting_Dataset (1).ipynb` | Notebook utama untuk proses pengolahan dataset tabular, mulai dari data understanding, cleaning, EDA, feature engineering, hingga preprocessing. |
| `stunting_wasting_dataset_dirty.csv` | Dataset utama yang digunakan pada notebook. Dataset ini merupakan versi hasil noise injection dari dataset awal Kaggle. |
| `df_clean.csv` | Dataset hasil proses cleaning dasar. |
| `df_feat.csv` | Dataset hasil feature engineering dan preprocessing yang sudah disiapkan untuk tahap modeling. |
| `modeling_ML_stuntingWasting_fix.ipynb` | Notebook modeling Machine Learning untuk prediksi stunting dan wasting, jika disertakan dalam repository. |

## Penjelasan Output Dataset

### `df_clean.csv`

`df_clean.csv` adalah dataset hasil pembersihan data dasar. Dataset ini dibuat setelah data awal melalui beberapa proses cleaning, seperti:

- Normalisasi nama kolom
- Penghapusan missing value
- Penghapusan data duplikat
- Pembersihan teks kategori
- Konversi kolom numerik
- Filter kategori yang valid
- Filter nilai antropometri yang tidak realistis
- Pembulatan nilai tinggi badan dan berat badan

Dataset ini masih mempertahankan label kategori asli, seperti `Normal`, `Stunted`, `Severely Stunted`, `Tall`, `Normal weight`, `Underweight`, dan kategori wasting lainnya.

### `df_feat.csv`

`df_feat.csv` adalah dataset lanjutan setelah proses feature engineering dan preprocessing. Dataset ini sudah berisi fitur tambahan dan target numerik yang dapat digunakan untuk proses modeling.

Fitur tambahan yang dibuat antara lain:

- `kelompok_umur`
- `rasio_berat_tinggi`
- `bmi`
- `interaksi_tb_bb`
- `stunting_target`
- `wasting_target`
- `stratify_label`

Dataset ini digunakan sebagai input utama pada tahap modeling Machine Learning.

## Data Dictionary

| Kolom | Keterangan |
|---|---|
| `jenis_kelamin` | Jenis kelamin balita. Pada tahap preprocessing dapat diubah menjadi nilai numerik. |
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

Kolom `stunting_target`, `wasting_target`, dan `stratify_label` tidak dimasukkan ke dalam fitur training. `stunting_target` dan `wasting_target` digunakan sebagai target prediksi, sedangkan `stratify_label` hanya digunakan untuk menjaga proporsi kelas pada proses train-test split.

## Catatan Penting

Model dan dataset dalam proyek ini digunakan untuk kebutuhan pembelajaran dan pengembangan sistem skrining awal. Hasil prediksi tidak dapat menggantikan pemeriksaan, diagnosis, atau saran medis dari tenaga kesehatan.
