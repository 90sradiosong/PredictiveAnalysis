# Laporan Proyek Machine Learning - Anggina Primanita

## Domain Proyek

Kualitas udara adalah salah satu aspek penting yang mempengaruhi kesehatan masyarakat. Standar kualitas Udara (Air Quality Standard) adalah salah satu standar yang dapat digunakan untuk mengukur dan melakukan monitoring terhadap kualitas udara[1]. Karena itu, standar ini terus dipantau dan dipublikasikan nilainya. Tangerang adalah salah satu kota di Indonesia yang mengalami polusi udara yang telah mempengaruhi kesehatan masyarakatnya[2] Untuk itu diperlukan sebuah analisis dan model prediksi yang dapat digunakan agar efek dari perubahan standar kualitas udara di kota Tangerang pada kesehatan masyarakat dapat diminimalisir.


## Business Understanding

### Problem Statements

Berdasarkan latar belakang, maka permasalah pada proyek ini adalah sebagai berikut:
- Bagaimana proses pengolahan data yang tepat agar dapat melakukan prediksi indeks standar kualitas menggunakan model yang tepat?
- Bagaimana membangun dan mengukur model prediksi standar kualitas udara yang optimal?

### Goals

Berdasarkan rumusan masalah, maka tujuan dari proyek ini adalah:
- Melakukan analisis dan pengolahan terhadap data Standar Kualitas Udara.
- Membangun model prediksi yang kemudian dievaluasi dengan MSE.
- Menemukan model prediksi yang paling optimal untuk Standar Kualitas Udara.

### Solution statements
Solusi yang ditawarkan untuk menyelesaikan tujuan adalah sebagai berikut:
- Melakukan perbandingan 4 jenis algoritma untuk mendapatkan model yang terbaik.
- Melakukan evaluasi dengan menggunakan Mean Square Error (MSE) dan menemukan model dengan nilai MSE paling optimal.

## Data Understanding
Data yang digunakan pada proyek ini adalah data yang diunggah oleh user Tangerangupdate pada tahun 2023. Data tersebut diunggah pada website Kaggle dan dapat diakses pada pranala berikut ini [link](ourwit/air-quality-in-south-tangerang-indonesia-20-23)

Dataset ini terdiri atas 1096 baris dan 10 kolom.

### Deskripsi Variabel

Variabel-variabel pada dataset Air Quality in South Tangerang adalah sebagai berikut
| Nama | Keterangan|
| --- | ------ |
| Date | Tanggal pengambilan data |
| PM10 | Hasil pengukuran Particulate Matter | 
| SO2 | Hasil pengukuran sulfur dioksida |
| CO | Hasil Pengukuran Karbon Monoksida |
| O3 | Hasil Pengukuran Ozon | 
| NO2 | Hasil Pengukuran Natrium Dioksida | 
| Max | Nilai pengukuran tertinggi | 
| Critical Component | Komponen dengan nilai pengukuran tertinggi | 
| Category | Kategori dari polusi udara, berdasarkan nilai pengukuran tertinggi | 

Target Variable pada proyek ini adalah Max, yaitu nilai pengukuran tertinggi.

### Analisis Data Kosong dan Duplikat

Dari 1096 data, tidak ada data pengukuran yang tanggalnya (kolom Date) bersifat duplikat. Sehingga tidak dilakukan penghapusan data duplikat. Kemudian dilakukan pengecekan terhadap data yang bersifat null. Pada tahap ini, ditemukan 60 data yang pengukuran O3 (Ozon)-nya bernilai null.

### Analisis dan Handling Outliers
Untuk mengetahui keberadaan data yang berupa outlier, data divisualisasikan menggunakan box plot yang dapat dilihat pada gambar berikut:

![boxplotsebelum](https://github.com/user-attachments/assets/ee6b57b1-9066-42cb-9f72-8896cc67414c)

Dapat dilihat bahwa terdapat cukup banyak data yang dinilai sebagai outlier. Pada tahap ini, penghapusan data pencilan dilakukan hanya pada variabel PM10 dan O3. Sedangkan pada CO dan Max, penghapusan tidak dilakukan, dikarenakan ada kemungkinan hal ini disebabkan oleh data yang tidak seimbang. Oleh sebab itu, pada fase ini dilanjutkan ke analisis distribusi variabel.

Penghapusan data outlier dilakukan dengan langkah-langkah sebagai berikut:
1. Menemukan kuartil 1 (Q1) dan kuartil 3(Q3) dari data berdasarkan PM10 dan O3.
2. Menemukan Inter Quartile Range (IQR) dari data dengan menghitung selisih antara Q1 dan Q3
3. Menghapus data outlier yang nilainya kurang dari $$Q1 - 1.5 * IQR$$ atau lebih besar dari $$Q3 + 1.5 * IQR$$

Hasil dari penghapusan outlier adalah 642 baris data.

### Univariate Analysis
Nilai target variabel Max kemudian diterjemahkan menjadi 3 kategori, yaitu:
| Range | Kategori |
| ----- | -------- |
| 0-50 |	Good |
| 51-100	| Moderate |
| 101-200	| Unhealthy |
| 201-300	| Very Unhealthy |
| 300++	 | Dangerous |

Distribusi data pada masing-masing divisualisasikan sebagai berikut:

![distribusikategori](https://github.com/user-attachments/assets/7f80920b-515b-46ba-a201-cc43e769dde4)

dapat dilihat secara umum melalui data tersebut, bahwa sebaran data yang ada bersifat imbalance. Hal ini kemudian akan ditangani melalui proses re-sampling pada sub-bab Data Preparation.

### Multivariate Data Analysis
Untuk mengetahui korelasi antar data numerikal yang ada pada dataset, dilakukan pembuatan matriks korelasi yang dapat dilihat pada gambar berikut

![matrikskorelasi](https://github.com/user-attachments/assets/b104011c-4d60-4149-909b-e41680e1bf2b)

Berdasarkan matriks korelasi tersebut, diketahui bahwa korelasi data numerik dengan variabel target Max adalah sebagai berikut:
- PM2.5 berkorelasi negatif lemah
- PM10 berkorelasi positif lemah
- SO2 berkorelasi negatif lemah
- CO berkorelasi positif dengan kuat
- O3 berkorelasi positif
- NO2 berkorelasi negatif lemah

disimpulkan bahwa seluruh data numerik berkorelasi dengan variabel target meskipun sebagian berkorelasi lemah. Sehingga pada proyek ini seluruh data numerik digunakan dan tidak ada yang di-drop.

## Data Preparation
Terdapat beberapa tahapan yang dilakukan pada tahap data preparation, yaitu:
- Handling Missing Value 
- Feature Engineering dengan memecah kolom "Date" menjadi 3 kolom, "day", "month", dan "year"
- Melakukan One Hot Encoding untuk data "Critical Component"
- Resampling data berdasarkan "Category" untuk menghasilkan data yang lebih balance
- Pembagian data menjadi train set dan test set
- Standarisasi Data

### Handling Missing Value
Berdasarkan hasil analisis, ditemukan bahwa dari 1096 baris terdapat 60 data yang tidak ada nilainya. Ke-60 baris data ini kemudian dihapus dari tabel.

### Feature Engineering
Terdapat data yang masih berupa object yaitu Date. Data Date berformat dd\mm\yyyy, sehingga dilakukan pembagian data menjadi 3 kolom yaitu "Day" yang menyimpan data dd, "Month" yang menyimpan data mm, dan "Year" yang menyimpan data "yyyy"

### Encoding
Data Critical Component adalah data yang bersifat kategorikal. Untuk dapat diproses oleh model, maka perlu dilakukan encoding terhadap data tersebut.

Dikarenakan data Critical Component adalah data yang bersifat nominal, sehingga dapat diterapkan One Hot Encoding yang menghasilkan 8 kolom baru.

Berikut adalah deskripsi data setelah encoding

![deskripsidataencoded_small](https://github.com/user-attachments/assets/834f5c70-a3eb-4940-8412-0781e48eb2d4)

### Resampling
Resampling dilakukan pada data "Category" ini dilakukan untuk meningkatkan keseimbangan pada data. Teknik resampling
 yang dipilih adalah oversampling yang dilakukan dengan teknik Synthetic Minority Over-sampling Technique (SMOTE). Teknik ini dipilih dikarenakan sample pada kategori "Unhealthy" sangat sedikit. Berikut adalah sebaran data sedelah dilakukan oversampling:

![distribusisetelahresample](https://github.com/user-attachments/assets/47600a37-7179-488b-8064-ec53a766aad2)

### Train-test split
Pada proyek ini, data dibagi dengan rasio train:test $$80:20$$, jumlah data setelah dilakukan train-test split adalah sebagai berikut:
- Total # of sample in whole dataset: 1737
- Total # of sample in train dataset: 1389
- Total # of sample in test dataset: 348

### Standarisasi Data
Untuk memastikan bahwa data yang menjadi input dari pelatihan dan evaluasi model terstandar dengan baik, maka dilakukan normalisasi data dengan Standard Scaler.

## Modeling
Model yang digunakan pada proyek ini adalah:
- K-Nearest Neighbor: algoritma K-NN memprediksi nilai data baru dengan membandingkan jaraknya ke sejumlah 
k tetangga terdekat berdasarkan kesamaan fitur dalam data pelatihan. 
- Random Forest: algoritma Random Forest adalah algoritma ensemble learning yang membentuk data menjadi sekumpulan decision tree. Hasil keputusan yang diambil pada algoritma ini umumnya diambil dari rata-rata nilai keputusan dari masing-masing decision tree.
- Ada Boost: algoritma ensemble ini menggabungkan beberapa *weak learners* untuk menjadi satu model yang lebih kuat.
- Decision Tree: algoritma ini membagi data menjadi *branches* pada sebuah tree berdasarkan fitur tertentu. Hasil prediksi yang dihasilkan adalah rata-rata nilai target pada *leaf*nya.

Adapun kelebihan dan kekurangan masing-masing model serta parameter yang digunakan pada project ini adalah sebagai berikut:
  
| Model | Kelebihan | Kekurangan | Parameter yang digunakan |
| --- | --- | --- | --- |
| K-Nearest Neighbor | Memiliki performa baik untuk data yang kecil (data para proyek ini hanya ~1000) | Kinerja mungkin turun ketika berhadapan dengan data berdimensi tinggi | *n_neighbors* = 10, diharapkan menghasilkan prediksi yang lebih mangkus karena menggunakan neighborhood yang lebih besar dari default |
| Random Forest | Memiliki ketahanan yang baik terhadap overfitting | Mungkin membutuhkan banyak memori |  *n_estimators*=50, menggunakan 50 tree pada forest, *max_depth*=16, kedalaman maksimum dari masing-masing tree adalah 16, *random_state*=55, seed untuk random number generator, agar dapat direproduksi kembali, *n_jobs*=-1, menggunakan semua CPU cores | 
| Adaboost | Memiliki ketahanan yang baik terhadap overfitting| Memerlukan data yang seimbang | *learning_rate*=0.05, untuk menghasilkan model yang baik, disarankan learning rate berada di antara 0.01 dan 0.1., *random_state*=55, seed untuk random number generator, agar dapat direproduksi kembali | 
| Decision Tree | dapat memetakan hubungan yang kompleks dan non-linear antara fitur dan variabel target. | Rentan terhadap overfitting | *random_state*=42, seed untuk random number generator, agar dapat direproduksi kembali |


## Evaluation
### Metrik Evaluasi
Metrik evaluasi yang digunakan pada proyek ini adalah **mean squared error**. Metrik ini menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. Metrik ini dipilih pada proyek ini dikarenakan memerlukan pengukuran ketelitian yang baik untuk mendapatkan model terbaik.

Mean Squared Error didefinisikan dalam persamaan sebagai berikut 

$$MSE = \frac{1}{N} \sum_{i=1}^{N} (y_i - ypred_i )^2$$

dengan:
- N: jumlah data
- $$y_i$$: output target ke i
- $$ypred_i$$: output hasil prediksi ke i

### Evaluasi Model
Berdasarkan aplikasi ke-empat model yang dipilih hasil dari perhitungan MSE-nya adalah sebagai berikut

| Model | Train | Test |
| --- | --- | --- |
| KNN	| 0.035685	| 0.03726
| RF	| 0.000111	| 0.000346
| Boosting	| 0.036502	| 0.036762
| DecisionTree	| 0.0	| 0.000552

Hasil perhitungan MSE masing-masing model divisualisasikan pada gambar sebagai berikut

![perbandinganMSE](https://github.com/user-attachments/assets/5ab1ad76-09d9-4d3c-89fa-f15ebc7ed629)

Dapat dilihat bahwa performa dari model Random Forest dan Decision tree mendekati nol, yang berarti kedua model ini adalah model terbaik. Tetapi, dilihat dari performa Trainnya, ada kemungkinan terjadi overfitting pada Decision Tree, hal ini dapat dilihat pada nilai MSE testingnya yang lebih besar daripada Random Forest. Sehingga dapat disimpulkan bahwa Random Forest adalah yang terbaik untuk kasus prediksi Standar Kualitas Udara ini.

Pada project ini telah dilakukan beberapa tahapan untuk mencapai solusi yang diinginkan. Pertama, data Standar Kualitas Udara telah dianalisis dan di-proses untuk menghasilkan data yang siap digunakan sebagai input dari model. Berdasarkan proses analisis, ditemukan bahwa data bersifat *imbalance* sehingga dilakukan proses resampling dengan SMOTE. Selanjutnya, 4 buah model prediksi telah dibangun dan dievaluasi menggunakan nilai MSE. Berdasarkan nilai MSE-nya, model yang paling optimal adalah Random Forest.

**Referensi**

[1] Istiqomah, N. A., & Marleni, N. N. N. (2020, November). Particulate air pollution in Indonesia: quality index, characteristic, and source identification. In IOP Conference Series: Earth and Environmental Science (Vol. 599, No. 1, p. 012084). IOP Publishing.

[2] Anurogo, D., Sulaeman, S., Yamtana, Y., & Andarmoyo, S. (2023). Assessing the Impact of Air Quality on Respiratory Health in Urban Environments: A Case Study of Tangerang. West Science Interdisciplinary Studies, 1(10), 940-951.

**---Ini adalah bagian akhir laporan---**
