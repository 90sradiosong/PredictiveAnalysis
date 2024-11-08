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


###Target Variable
Target Variable pada proyek ini adalah Max, yaitu nilai pengukuran tertinggi.

##Distribusi Variable
Nilai target variabel max kemudian diterjemahkan menjadi 3 kategori, yaitu:
| Range | Kategori |
| ----- | -------- |
| 0-50 |	Good |
| 51-100	| Moderate |
| 101-200	| Unhealthy |
| 201-300	| Very Unhealthy |
| 300++	 | Dangerous |

Kategori tersebut kemudian divisualisasikan sebagai berikut:

![Distribusi Kategori](https://github.com/user-attachments/assets/aacd855c-8103-4fb9-8a11-a7ae4bf0ad6b)

dapat dilihat secara umum melalui data tersebut, bahwa sebaran data yang ada bersifat imbalance. Hal ini kemudian akan ditangani melalui proses re-sampling pada sub-bab Data Preparation.

## Data Preparation
Terdapat 2 tahapan yang dilakukan pada tahap data preparation, yaitu:
- Encoding data "Date" menjadi 3 kolom, "day", "month", dan "year"
- Melakukan One Hot Encoding untuk data "Critical Component"
- Resampling data berdasarkan "Category" untuk menghasilkan data yang lebih balance


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
| Support Vector Machine | Memiliki performa baik untuk data berdimensi tinggi | Kinerja mungkin turun pada dataset yang besar |


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


**Referensi**
[1] Istiqomah, N. A., & Marleni, N. N. N. (2020, November). Particulate air pollution in Indonesia: quality index, characteristic, and source identification. In IOP Conference Series: Earth and Environmental Science (Vol. 599, No. 1, p. 012084). IOP Publishing.
[2] Anurogo, D., Sulaeman, S., Yamtana, Y., & Andarmoyo, S. (2023). Assessing the Impact of Air Quality on Respiratory Health in Urban Environments: A Case Study of Tangerang. West Science Interdisciplinary Studies, 1(10), 940-951.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
