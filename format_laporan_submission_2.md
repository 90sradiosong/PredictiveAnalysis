# Laporan Proyek Machine Learning - Anggina Primanita

## Project Overview

Video game digital (Gim) adalah aplikasi perangkat lunak yang paling dekat dengan manusia. Saat ini, ada banyak sekali gim yang dirilis. Pada tahun 2023, terdapat 14.326 game yang dirilis pada platform STEAM [1]. Banyaknya permainan membuat pemain menjadi sulit untuk menemukan game yang sesuai dengan minatnya. Salah satu faktor pembeda yang menjelaskan tipe atau karakteristik dari suatu gim adalah genre-nya [2]. Umumnya, pemain akan menyukai gim dengan genre serupa karena memiliki pengalaman bermain yang mirip. Saat ini, sebuah gim bisa memiliki lebih dari satu genre, sehingga pemain mungkin mengalami kesulitan dalam memilih permainan yang mirip dengan genre yang disukainya. Untuk itu, diperlukan suatu sistem rekomendasi yang dapat memberikan rekomendasi game yang sesuai dengan minat pemain berdasarkan genrenya.

## Business Understanding

### Problem Statements
Berdasarkan latar belakang, maka permasalah pada proyek ini adalah sebagai berikut:

1. Bagaimana proses pengolahan data yang tepat agar dapat model dapat memberikan rekomendasi berdasarkan genre gim?
2. Bagaimana membangun dan mengevaluasi model rekomendasi gim berdasarkan genre?
   
### Goals
Berdasarkan problem statements, maka tujuan dari proyek ini adalah:

1. Melakukan analisis dan pengolahan terhadap data gim.
2. Membangun model content-based filtering dan mengevaluasinya.

### Solution statements
Solusi yang ditawarkan untuk menyelesaikan tujuan adalah sebagai berikut:

1. Melakukan pembangunan model content-based filtering berdasarkan genre.
2. Melakukan evaluasi dengan melihat hasil similarity dari Top-N hasil rekomendasi dari model yang dibangun dengan precision@K

## Data Understanding

Data yang digunakan pada proyek ini adalah data yang bersumber dari Kaggle yang bernama Top Games Dataset yang diunggah oleh user Waqar Ali yang terakhir diupdate pada tahun 2024. Dataset ini dapat diakses pada link berikut [link dataset] (https://www.kaggle.com/datasets/waqi786/top-games-dataset). Top Games Dataset memiliki 5000 baris data dan 5 kolom.

Variabel-variabel pada Top Games Dataset adalah sebagai berikut:
- Game Name: nama dari game
- Genre: genre dari game. Kolom ini hanya menyimpan 1 genre game
- Platform: platform dimana game dirilis
- Release Year: tahun rilis game. Dataset ini berisi game yang dirilis pada rentang tahun 2000-2023
- User Rating: rating dari game

### Data Insight

Dilakukan pengecekan terhadap jumlah game, genre, dan platform yang ada pada dataset. Berdasarkan hasil pengecekan, diketahui bahwa dataset berisi 58 game, 14 genre, dan 5 platform. 5000 data yang ada pada dataset dihasilkan dari beberapa kombinasi yang berbeda, contohnya, 1 game dapat memiliki beberapa genre atau memiliki beberapa user rating.

Berdasarkan pengecekan duplikasi data, ditemukan bahwa tidak ada data yang bersifat duplikat, sedangkan pengecekan untuk missing data dilakukan dengan pengecekan entry yang bernilai null. Hasil pengecekan menyatakan bahwa tidak ada entry yang bernilai null. 

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
Pada tahap Data Understanding diketahui bahwa sebuah game dapat memiliki entry dengan genre yang berbeda. Sehingga dilakukan penggabungan fitur dari seluruh genre. Penggabungan dilakukan dengan menggabungkan masing-masing genre dipisah dengan tanda koma(,). Setelah masing-masing genre digabungkan, pada dataframe tersisa 58 baris. Jumlah ini sama dengan jumlah nama game yang unik.

### Perhitungan TF-IDF
Langkah pertama dalam pembangunan model content-based recommendation model ini adalah penerapan TF-IDF pada kolom genre. TF-IDF adalah metode yang untuk menentukan seberapa penting suatu kata dalam kumpulan string yang dalam hal ini adalah genre. 

Pada tahap ini, dilakukan beberapa langkah yaitu:
1. Pembuatan Vector fitur dengan Vectorizer. Hasil dari tahap ini adalah sebuah vektor yang berisi kata-kata penting dalam kolom genre. Ditemukan 15 kata penting dari kolom genre. Hasil ini berbeda dengan jumlah genre unik, dikarenakan salah satu genre 'role-playing' dianggap menjadi 2 kata berbeda yaitu 'role' dan 'playing'.
2. Membentuk tfidf_matrix, yaitu matrix hasil transformasi dari vector yang dihasilkan pada tahap sebelumnya
3. Membentuk matrix untuk menyimpan hasil cosine similarity dan menghitung cosine similarity dari masing-masing game berdasarkan fitur genrenya. Cosine similarity adalah ukuran kesamaan antara dua vektor dengan menghitung kosinus sudut di antara keduanya. Dalam hal ini, vektor yang dihitung kesamaannya adalah gabungan dari berbagai genre pada kolom Genre.
4. Membuat dataframe cosine_sim_df dari variabel cosine_sim dengan baris dan kolom berupa nama game

Berikut adalah hasil 10 sampel game dari dataframe

![cosinesimmatrix](https://github.com/user-attachments/assets/f84c41e4-5a78-4eb6-af69-be837de711e4)

Terlihat hasil perhitungan kedekatan dari beberapa game. Sebagai contoh: Game Genshin Impact memiliki nilai kedekatan sebesar 0.958689 dengan game League of Legends:Wild Rift, yang artinya game ini memiliki genre yang mirip. Pemain Game Genshin Impact mungkin akan menyukai rekomendasi game League of Legends.

## Modeling and Results

### Model Development menggunakan Content-Based Filtering

Model rekomendasi dihasilkan dengan memilih game dengan cosine similarity tertinggi dari game input. Model ini dibuat pada method game_recommendation. Method ini memiliki 4 parameter

1. nama_game : nama dari game yang dicari rekomendasinya
2. similarity_data: dataframe yang menyimpan hasil perhitungan cosine similarity
3. items: data yang akan ditampilkan, berisi nama dan hasil gabungan genre
4. k: banyaknya jumlah rekomendasi yang diminta

Method ini bekerja dengan mencari index dari nama_game yang dicari pada similarity_data. Kemudian, berdasarkan index yang ditemukan, dicari Top-K entry dengan nilai similarity tertinggi. Entry ini disimpan pada sebuah variabel yang akan digunakan sebagai output.

Untuk output hasil, nilai cosine similarity dari masing-masing game rekomendasi ditambahkan pada variabel output dan terakhir, items yang berisi nama game dan genre ditambahkan sebagai kolom pada data kembalian.

### Result

Untuk melakukan evaluasi, dilakukan percobaan dengan salah satu input game yaitu "Fortnite". Fortnite memiliki data sebagai berikut:

![datafortnite](https://github.com/user-attachments/assets/56eb8f66-bf00-47f0-a894-743e8ee6571d)

Hasil rekomendasi yang diberikan model adalah sebagai berikut:

![hasilrekomendasi](https://github.com/user-attachments/assets/c6528482-e7a8-472a-82ed-075e624bbe4f)

Terlihat bahwa masing-masing game memiliki nilai cosine similarity pada TOP-5 yang tinggi (lebih besar dari 0.9) yang artinya sistem ini telah memberikan rekomendasi yang baik berdasarkan genrenya.

# Evaluation

Untuk mengevaluasi model yang telah dibangun, dilakukan perhitungan menggunakan precision@K. Precision@K adalah sebuah metrik yang dapat digunakan untuk menghitung kualitas rekomendasi, di mana nilai yang lebih tinggi menyatakan rekomendasi yang lebih baik. Adapun formula yang digunakan untuk menghitung nilai tersebut adalah sebagai berikut

$$ Precision@K = \frac{Jumlah\ item\ yang\ relevan\ pada\ Top-K}{K}$$

Pada proyek ini, perhitungan precision@K dilakukan untuk k=1 sampai dengan k=5. Hasilnya adalah sebagai berikut:

![precisionatk](https://github.com/user-attachments/assets/f83b5491-0785-4223-be0e-c7833bbc19e4)

Berdasarkan hasil evaluasi, dapat dilihat pada nilai precision@K yang terbaik adalah K = 2, artinya rekomendasi yang paling relevan akan diberikan pada K = 2.

Pada proyek ini, data dari permainan berdasarkan genre-nya telah diproses dan digunakan untuk membangun model rekomendasi Content-based Filtering berdasarkan genrenya. Model rekomendasi yang telah dibangun dapat merekomendasikan permainan dengan genre yang kemiripannya di atas 0.9. Untuk memastikan kualitas rekomendasinya, model tersebut kemudian dievaluasi. Evaluasi yang dipilih adalah precision@K. Metriks ini  dengan metrik precision@K yang memberikan hasil terbaik yaitu 92.0 pada K=2, selanjutnya nilai precision@K menurun.


# Referensi

[1] SteamDB. Steam Game Releases by Year. (2024). Dapat diakses pada: https://steamdb.info/stats/releases/ (Terakhir diakses tanggal: 09 December 2024). 

[2] Arsenault, Dominic. "Video game genre, evolution and innovation." Eludamos: Journal for computer game culture 3.2 (2009): 149-176.

**---Ini adalah bagian akhir laporan---**

