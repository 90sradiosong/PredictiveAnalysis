# Laporan Proyek Machine Learning - Anggina Primanita

## Domain Proyek

Kualitas udara adalah salah satu aspek penting yang mempengaruhi kesehatan masyarakat. Standar kualitas Udara (Air Quality Standard) adalah salah satu standar yang dapat digunakan untuk mengukur dan melakukan monitoring terhadap kualitas udara[1]. Karena itu, standar ini terus dipantau dan dipublikasikan nilainya. Tangerang adalah salah satu kota di Indonesia yang mengalami polusi udara yang telah mempengaruhi kesehatan masyarakatnya[2] Untuk itu diperlukan sebuah analisis dan model prediksi yang dapat digunakan agar efek dari perubahan standar kualitas udara di kota Tangerang pada kesehatan masyarakat dapat diminimalisir.


## Business Understanding

### Problem Statements

Berdasarkan latar belakang, maka permasalah pada proyek ini adalah sebagai berikut:
- Bagaimana proses pengolahan data yang tepat agar dapat melakukan prediksi indeks standar kualitas menggunakan model yang tepat?
- Bagaimana membuat sistem prediksi standar kualitas udara yang memiliki error yang rendah?

### Goals

Berdasarkan rumusan masalah, maka tujuan dari proyek ini adalah:
- Melakukan analisis dan pengolahan terhadap data Standar Kualitas Udara
- Membuat implementasi sistem prediksi dengan error yang rendah sehingga 

### Solution statements
Solusi yang ditawarkan untuk menyelesaikan tujuan adalah sebagai berikut:
- Melakukan perbandingan 3 jenis algoritma untuk mendapatkan model yang terbaik
- Melakukan evaluasi dengan menggunakan Mean Square Error (MSE)

## Data Understanding
Data yang digunakan pada proyek ini adalah data yang diunggah oleh user Tangerangupdate pada tahun 2023. Data tersebut diunggah pada website Kaggle dan dapat diakses pada pranala berikut ini [link](ourwit/air-quality-in-south-tangerang-indonesia-20-23)

Dataset ini terdiri atas 1096 baris dan 10 kolom


### Variabel-variabel pada dataset Air Quality in South Tangerang adalah sebagai berikut
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


### Target Variable
Target Variable pada proyek ini adalah Max, yaitu nilai pengukuran tertinggi.

### Null Data
Berdasarkan hasil analisis, ditemukan bahwa dari 1096 baris terdapat 60 data yang tidak ada nilainya. Ke-60 baris data ini kemudian dihapus dari tabel.

### Distribusi Variable
Nilai target variabel max kemudian diterjemahkan menjadi 3 kategori, yaitu:
| Range | Kategori |
| ----- | -------- |
| 0-50 |	Good |
| 51-100	| Moderate |
| 101-200	| Unhealthy |
| 201-300	| Very Unhealthy |
| 300++	 | Dangerous |

Distribusi data pada masing-masing divisualisasikan sebagai berikut:

![Distribusi Kategori](https://github.com/90sradiosong/PredictiveAnalysis/blob/8772715fadeebcc9fc75cda8670f5c984cd18537/images/distribusikategori.png)

dapat dilihat secara umum melalui data tersebut, bahwa sebaran data yang ada bersifat imbalance. Hal ini kemudian akan ditangani melalui proses re-sampling pada sub-bab Data Preparation.

### Correlation Matrix
Untuk mengetahui korelasi antar data numerikal yang ada pada dataset, dilakukan pembuatan matriks korelasi yang dapat dilihat pada gambar berikut

![Matriks Korelasi] (https://github.com/90sradiosong/PredictiveAnalysis/blob/a5bba1617a16d023f0ff1ea64e4b4ea406e79725/images/matrikskorelasi.png)

Berdasarkan matriks korelasi tersebut, diketahui bahwa korelasi data numerik dengan variabel target Max adalah sebagai berikut:
- PM2.5 berkorelasi negatif lemah
- PM10 berkorelasi positif lemah
- SO2 berkorelasi negatif lemah
- CO berkorelasi positif dengan kuat
- O3 berkorelasi positif
- NO2 berkorelasi negatif lemah

disimpulkan bahwa seluruh data numerik berkorelasi dengan variabel target meskipun sebagian berkorelasi lemah. Sehingga pada proyek ini seluruh data numerik digunakan dan tidak ada yang di-drop.

## Data Preparation
Terdapat 3 tahapan yang dilakukan pada tahap data preparation, yaitu:
- Encoding data "Date" menjadi 3 kolom, "day", "month", dan "year"
- Melakukan One Hot Encoding untuk data "Critical Component"
- Resampling data berdasarkan "Category" untuk menghasilkan data yang lebih balance

### Encoding
Terdapat 2 data kategorikal pada dataset yaitu Date dan Critical Component. Untuk dapat diproses oleh model, maka dilakukan encoding terhadap data-data tersebut. Data Date berformat dd\mm\yyyy, sehingga dilakukan pembagian data menjadi 3 kolom yaitu "Day" yang menyimpan data dd, "Month" yang menyimpan data mm, dan "Year" yang menyimpan data "yyyy"

Selanjutnya data Critical Component adalah data yang bersifat nominal, sehingga dapat diterapkan One Hot Encoding yang menghasilkan 8 kolom baru.

Berikut adalah deskripsi data setelah encoding

![Encoded Data](https://github.com/90sradiosong/PredictiveAnalysis/blob/de34f3541d9de6a1acb778456341729abb6d8f09/images/deskripsidataencoded.png)

### Resampling
Resampling dilakukan pada data "Category" ini dilakukan untuk meningkatkan keseimbangan pada data. Resampling dilakukan dengan teknik Synthetic Minority Over-sampling Technique (SMOTE). Teknik ini dipilih dikarenakan sample pada kategori "Unhealthy" sangat sedikit. Berikut adalah sebaran data sedelah dilakukan oversampling:

![Distribusi Kategori setelah Resampling](https://github.com/90sradiosong/PredictiveAnalysis/blob/a5bba1617a16d023f0ff1ea64e4b4ea406e79725/images/distribusisetelahresample.png)

## Modeling
Model yang digunakan pada proyek ini adalah:
- K-Nearest Neighbor
- Random Forest
- Adaboost
- Support Vector Machine
  
| Model | Kelebihan | Kekurangan |
| --- | --- | --- |
| K-Nearest Neighbor | Memiliki performa baik untuk data yang kecil (data para proyek ini hanya ~1000) | Kinerja mungkin turun ketika berhadapan dengan data berdimensi tinggi |
| Random Forest | Memiliki ketahanan yang baik terhadap overfitting | Mungkin membutuhkan banyak memori |
| Adaboost | Memiliki ketahanan yang baik terhadap overfitting| Memerlukan data yang seimbang |
| Decision Tree | dapat memetakan hubungan yang kompleks dan non-linear antara fitur dan variabel target. | Rentan terhadap overfitting |


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
| KNN	| 0.050712	| 0.068404
| RF	| 0.000093	| 0.000714
| Boosting	| 0.031089	| 0.02306
| DecisionTree	| 0.0	| 0.000962

Hasil perhitungan MSE masing-masing model divisualisasikan pada gambar sebagai berikut

![nilai MSE masing-masing model](https://github.com/90sradiosong/PredictiveAnalysis/blob/a5bba1617a16d023f0ff1ea64e4b4ea406e79725/images/perbandinganMSE.png)

Dapat dilihat bahwa performa dari model Random Forest dan Decision tree mendekati nol, yang berarti kedua model ini adalah model terbaik. Tetapi, dilihat dari performa Trainnya, ada kemungkinan terjadi overfitting pada Decision Tree, hal ini dapat dilihat pada nilai MSE testingnya yang lebih besar daripada Random Forest. Sehingga dapat disimpulkan bahwa Random Forest adalah yang terbaik untuk kasus prediksi Standar Kualitas Udara ini.

**Referensi**
[1] Istiqomah, N. A., & Marleni, N. N. N. (2020, November). Particulate air pollution in Indonesia: quality index, characteristic, and source identification. In IOP Conference Series: Earth and Environmental Science (Vol. 599, No. 1, p. 012084). IOP Publishing.
[2] Anurogo, D., Sulaeman, S., Yamtana, Y., & Andarmoyo, S. (2023). Assessing the Impact of Air Quality on Respiratory Health in Urban Environments: A Case Study of Tangerang. West Science Interdisciplinary Studies, 1(10), 940-951.

**---Ini adalah bagian akhir laporan---**
