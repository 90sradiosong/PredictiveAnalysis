# Laporan Proyek Machine Learning - Anggina Primanita

## Project Overview

Game Digital adalah aplikasi perangkat lunak yang paling dekat dengan manusia. Sa'at ini, dalam satu tahun ada banyak sekali game yang dirilis, sehingga sulit untuk menemukan game yang sesuai dengan minat pemain. Salah satu pembeda satu game dengan game yang lain adalah genre-nya. Umumnya, pemain akan menyukai game dengan genre serupa, tetapi, sa'at ini sebuah game bisa memiliki lebih dari satu genre. Untuk itu, diperlukan suatu sistem rekomendasi yang dapat memberikan rekomenadasi game yang sesuai dengan minat pemain berdasarkan genrenya.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa proyek ini penting untuk diselesaikan.
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding



Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Rumusan masalah dari proyek ini adalah:
1. Bagaimana membangun model rekomendasi permainan berdasarkan genrenya?
2. Bagaimana mengevaluasi model rekomendasi permainan berdasarkan genrenya?

### Goals

Tujuan dari proyek ini adalah:
- Membangun model rekomendasi berdasarkan genre
- Mengevaluasi model rekomendasi

### Solution Statements

Pendekatan yang dilakukan untuk mencapai tujuan adalah:
- Menggunakan model content-based filtering
- Melakukan evaluasi 



## Data Understanding
Data yang digunakan pada proyek ini adalah data yang bersumber dari Kaggle yang bernama Top Games Dataset yang diunggah oleh user Waqar Ali yang terakhir diupdate pada tahun 2024. Dataset ini dapat diakses pada link berikut [link dataset] (https://www.kaggle.com/datasets/waqi786/top-games-dataset). Top Games Dataset memiliki 5000 baris data dan 5 kolom.

Variabel-variabel pada Top Games Dataset adalah sebagai berikut:
- Game Name: nama dari game
- Genre: genre dari game. Kolom ini hanya menyimpan 1 genre game
- Platform: platform dimana game dirilis
- Release Year: tahun rilis game. Dataset ini berisi game yang dirilis pada rentang tahun 2000-2023
- User Rating: rating dari game

### Data Insight

Dilakukan pengecekan terhadap jumlah game, genre, dan platform yang ada pada dataset. Berdasarkan hasil pengecekan, diketahui bahwa dataset berisi 58 game, 15 genre, dan 5 platform. 5000 data yang ada pada dataset dihasilkan dari beberapa kombinasi yang berbeda, contohnya, 1 game dapat memiliki beberapa genre atau memiliki beberapa user rating.

Berdasarkan pengecekan duplikasi data, ditemukan bahwa tidak ada data yang bersifat dupblikat, sedangkan pengecekan untuk missing data dilakukan dengan pengecekan entry yang bernilai null. Hasil pengecekan menyatakan bahwa tidak ada entry yang bernilai null. 

### Univariate Analysis

Univariate Data Analysis dilakukan dengan menampilkan histogram dari 2 kolom, yaitu platform dan genre. Histogram menampilkan frekuensi kemunculan masing-masing platform dan genre.

![univariate histogram](https://github.com/user-attachments/assets/d08f24b9-9668-4c59-84f7-46ea284163ee)

Histogram dari genre game menunjukkan bahwa terdapat genre yang sangat dominan, yaitu Genre Sports. Terdapat 7 game dengan genre sports, yang artinya game ini sangat populer. Sebaliknya hanya terdapat 1 game dengan genre Action, yang artinya game ini jarang ditemui.

Histogram dari platform game menunjukkan bahwa platform yang paling populer adalah PlayStation, sedangkan platform lainnya memiliki jumlah game dirilis yang lebih sedikit. Namun, perbedaan antara platform paling populer dan paling tidak populer (Mobile) tidak terlalu jauh.

## Data Preparation

### Drop Unused Column
Pada tahap ini, dibuat dataframe baru untuk menyimpan hasil preprocessing: game_df. Kolom release year, platform, dan user rating tidak memengaruhi hasil rekomendasi, sehingga didrop dari game_df.

Informasi dataframe game_df setelah penghapusan adalah sebagai berikut

![game_df](https://github.com/user-attachments/assets/da4cb853-75f3-4ce0-bb78-e4e4183064a7)

### Penggabungan Genre
Pada tahap Data Understanding diketahui bahwa sebuah game dapat memiliki entry dengan genre yang berbeda. Sehingga dilakukan penggabungan fitur dari seluruh genre. Penggabungan dilakukan dengan menggabungkan masing-masing genre dipisah dengan tanda koma(,). Setelah masing-masing genre digabungkan, pada dataframe tersisa 58 baris. Hal ini sama dengan jumlah nama game yang unik.

## Modeling

### Perhitungan TF-IDF
Langkah pertama dalam pembangunan model content-based recommendation model ini adalah penerapan TF-IDF pada kolom genre. TF-IDF adalah metode yang untuk menentukan seberapa penting suatu kata dalam kumpulan string yang dalam hal ini adalah genre. 

Pada tahap ini, dilakukan beberapa langkah yaitu:
1. Pembuatan Vector fitur dengan Vectorizer
2. Hasil dari tahap ini adalah sebuah vektor yang berisi kata-kata penting dalam kolom genre. Ditemukan 15 kata penting dari kolom genre. Hasil ini berbeda dengan jumlah genre unik, dikarenakan salah satu genre 'role-playing' dianggap menjadi 2 kata berbeda yaitu 'role' dan 'playing'.



## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
