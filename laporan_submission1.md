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
| Nama | Jenis | Keterangan| Variabel |
| --- | ----- | ------ | ------ |
| Date | Kategorikal Nominal | Tanggal pengambilan data | ------ |
| PM10 | Numerik Kontinu | Hasil pengukuran Particulate Matter | ------ |
| SO2 | Numerik Kontinu | Hasil pengukuran sulfur dioksida | ------ |
| CO | Numerik Kontinu | Hasil Pengukuran Karbon Monoksidra | ------ |
| O3 | Numerik Kontinu | Hasil Pengukuran Ozon | ------ |
| NO2 | Numerik Kontinu | Hasil Pengukuran Natrium Dioksida | ------ |
| Max | Numerik Kontinu | Nilai pengukuran tertinggi | ------ |
| Critical Component | Kategorikal Nominal | Komponen dengan nilai pengukuran tertinggi | ------ |
| Category | Kategorikal Nominal | Kategori dari polusi udara, berdasarkan nilai pengukuran tertinggi | ------ |


**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**Referensi**
[1] Istiqomah, N. A., & Marleni, N. N. N. (2020, November). Particulate air pollution in Indonesia: quality index, characteristic, and source identification. In IOP Conference Series: Earth and Environmental Science (Vol. 599, No. 1, p. 012084). IOP Publishing.
[2] Anurogo, D., Sulaeman, S., Yamtana, Y., & Andarmoyo, S. (2023). Assessing the Impact of Air Quality on Respiratory Health in Urban Environments: A Case Study of Tangerang. West Science Interdisciplinary Studies, 1(10), 940-951.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
