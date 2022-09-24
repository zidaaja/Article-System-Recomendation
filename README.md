# Laporan Proyek Machine Learning - Amazida

## Project Overview
Artikel adalah sebuah tulisan yang berisikan fakta dan berita yang dilengkapi dengan data. Artikel menjadi kebutuhan setiap orang untuk dijadikan bahan bacaan yang valid dan terpercaya. Segala macam bidang memerlukan sebuah artikel untuk mendapatkan informasi yang sesuai dengan yang mereka inginkan. Oleh sebab itu, rekomendasi mengenai artikel dapat membantu pembaca dalam memilih bacaan yang sesuai dengan apa yang orang baca.


## Business Understanding

Bagian laporan ini mencakup:

### Problem Statements

Berdasarkan uraian yang telah disebutkan, maka pernyataan masalah yang didapat sebagai berikut:
- Bagaimana cara merekomendasikan artikel yang mirip dengan artikel yang dibaca pengguna ?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Membangun sistem rekomendasi artikel yang dipersonalisasi untuk pengguna dengan teknik _Content Based Filtering_

### Solution Approach
- Melakukan analisis terhadap dataset yang ada dengan _Univariate Analysis_
- Melakukan pengecekan nilai NULL dan duplikasi terhadap dataset
- Membangun model _Content Based Filtering_ menggunakan vektorisasi teks TF-IDF Vectorizer dan menghitung derajat kesamaan teks dengan _cosine similarity_


## Data Understanding
Dataset yang digunakan pada projek ini adalah dataset [BBC News](https://www.kaggle.com/datasets/malwyshihab/bbc-news-data-2).

Berikut seluruh variabel atau fitur pada data:  

Variabel-variabel pada BBC News Dataset adalah sebagai berikut:
- `Artikel`: Artikel seperti nomor ID
- `Text`: Isi artikel atau berita
- `Category`: Kategori berita atau artikel

Data memiliki 682 data dengan 3 kolom.

Dalam memahami data ini saya melakukan _Exploratory data analysis_ dengan melihat informasi pada data dan terdapat variabel `Artikel` yang bertipe data integer, variabel `Text` dan `Category` bertipe data object. Kemudian, melihat kategori apa saja yang ada didalam dataset tersebut dengan memvisualisasikannya menggunakan plot seperti pada gambar berikut.

<img width="299" alt="image" src="https://user-images.githubusercontent.com/102134676/192095999-fe079476-fd62-4fe7-a71f-f9fbc9715737.png">

Gambar 1. Visualisasi kategori yang ada di dataset

Dapat dilihat bahwa kategori didalam dataset tersebut ada 2 yaitu _sport_ dan _business_


## Data Preparation
Pada tahap preparation yang saya lakukan adalah:
### Mengecek apakah tidak ada data yang bernilai NULL
Saya menghitung nilai null yang terdapat dalam data, dan hasilnya adalah semua variabel atau fitur memiliki 0 nilai NULL, artinya tidak ada data yang bernilai NULL dalam dataset tersebut
### Mengecek apakah tidak ada data yang terduplikat
Saya menghitung nilai duplikat dalam data, dan hasilnya adalah semua variabel atau fitur memiliki 0 _duplicated_, artinya tidak ada data yang terduplikasi dalam dataset tersebut.

Tidak ada data yang memiliki NULL dan terduplikat, maka data kemungkinan sudah siap untuk digunakan.


## Modeling
### Membangun model sederhana menggunakan TF-IDF Vectorizer
Pada proyek ini, saya menggunakan fungsi tfidfvectorizer() dari library sklearn. Dengan menggunakan parameter `min_df = 0.01` untuk mengabaikan term yang muncul kurang dari 1% dalam teks, dan `sublinear_tf = True` untuk menormalisasi bias terhadap teks yang panjang dan teks yang pendek.

### Melakukan fit dan transformasi ke bentuk matrix

`(682, 2)`

Matriks yang dimiliki berukuran (682, 2). Nilai 682 merupakan ukuran data dan 2 merupakan matrik kategori artikel. Kemudian, menggunakan fungsi todense() untuk menghasilkan vektor tf-idf dalam bentuk matriks.

### Menghitung derajat kesamaan dengan Cosine Similarity
Saya menghitung cosine similarity dataframe tfidf_matrix yang diperoleh pada tahapan sebelumnya, output yang ditampilkan berupa matriks kesamaan dalam bentuk array.

| Artikel 	| 329 	| 924 	| 1738 	| 2186 	| 733 	|
|--------:	|----:	|----:	|-----:	|-----:	|----:	|
| Artikel 	|     	|     	|      	|      	|     	|
|   1117  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   120   	| 0.0 	| 0.0 	|  1.0 	|  0.0 	| 1.0 	|
|   1969  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   1739  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   1475  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   2219  	| 0.0 	| 0.0 	|  1.0 	|  0.0 	| 1.0 	|
|   1403  	| 0.0 	| 0.0 	|  1.0 	|  0.0 	| 1.0 	|
|   1929  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   1793  	| 1.0 	| 1.0 	|  0.0 	|  1.0 	| 0.0 	|
|   2043  	| 0.0 	| 0.0 	|  1.0 	|  0.0 	| 1.0 	|


Angka 1.0 mengindikasikan bahwa artikel pada kolom X (horizontal) memiliki kesamaan dengan artikel pada baris Y (vertikal).

### Mendapatkan Rekomendasi
saya melihat data artikel salah satu artikel, misalkan artikel 15:


|     	| Artikel 	| Text 	|                                          Category 	|       	|
|----:	|--------:	|-----:	|--------------------------------------------------:	|-------	|
| 248 	|   248   	|   15 	| moya emotional after davis cup win carlos moya... 	| sport 	|


Dapat dilihat bahwa artikel 15 memiliki kategori sport. Dan berikut hasil dari rekomendasi:

|   	| Artikel 	|                                              Text 	| Category 	|
|--:	|--------:	|--------------------------------------------------:	|---------:	|
| 0 	|      82 	| coach ranieri sacked by valencia claudio ranie... 	|    sport 	|
| 1 	|     460 	| fuming robinson blasts officials england coach... 	|    sport 	|
| 2 	|     495 	| arnesen denies rift with santini tottenham spo... 	|    sport 	|
| 3 	|     612 	| bosvelt optimistic over new deal manchester ci... 	|    sport 	|
| 4 	|     485 	| lewis-francis eyeing world gold mark lewis-fra... 	|    sport 	|
| 5 	|    1214 	| old firm pair handed suspensions celtic s henr... 	|    sport 	|
| 6 	|    1642 	| tulu to appear at caledonian run two-time olym... 	|    sport 	|
| 7 	|    1751 	|   connors rallying cry for british tennis do y... 	|    sport 	|
| 8 	|    1633 	| edu blasts arsenal arsenal s brazilian midfiel... 	|    sport 	|
| 9 	|    1750 	| clijsters hope on aussie open kim clijsters ha... 	|    sport 	|

Dapat dilihat bahwa sistem merekomendasikan artikel dengan kategori yang sama yaitu _sport_.


## Evaluation
Evaluasi pada model _Machine Learning Content Based Filtering_ dapat menggunakan metriks _precission_, yaitu jumlah item rekomendasi yang relevan.
Berikut rumus dari metriks precision:

`Precision = #of recommendation that are relevant/#of item we recommend`

Dan berikut hasil dari rekomendasi artikel:

|   	| Artikel 	|                                              Text 	| Category 	|
|--:	|--------:	|--------------------------------------------------:	|---------:	|
| 0 	|      82 	| coach ranieri sacked by valencia claudio ranie... 	|    sport 	|
| 1 	|     460 	| fuming robinson blasts officials england coach... 	|    sport 	|
| 2 	|     495 	| arnesen denies rift with santini tottenham spo... 	|    sport 	|
| 3 	|     612 	| bosvelt optimistic over new deal manchester ci... 	|    sport 	|
| 4 	|     485 	| lewis-francis eyeing world gold mark lewis-fra... 	|    sport 	|
| 5 	|    1214 	| old firm pair handed suspensions celtic s henr... 	|    sport 	|
| 6 	|    1642 	| tulu to appear at caledonian run two-time olym... 	|    sport 	|
| 7 	|    1751 	|   connors rallying cry for british tennis do y... 	|    sport 	|
| 8 	|    1633 	| edu blasts arsenal arsenal s brazilian midfiel... 	|    sport 	|
| 9 	|    1750 	| clijsters hope on aussie open kim clijsters ha... 	|    sport 	|


Berdasarkan hasil rekomendasi yang saya uji yaitu dengan menggunakan artikel 15, terlihat bahwa artikel 15 memiliki kategori sport dan dari Artikel yang direkomendasikan tersebut 10 artikel memiliki kategori sport. Ini artinya precisionnya sebesar 10/10 atau 100%.

## Conclusion/Kesimpulan
Sistem rekomendasi artikel yang dibangun dengan model _machine learning_ dengan metode _content based filtering_ menghasilkan precision 100%. Namun, diharapkan nanti mencoba dataset yang memiliki kategori lebih bervariasi untuk menguji menggunakan _content based filtering_ ini.

## Referensi
[1] Musto, C., Gemmis, M. D., Lops, P., Narducci, F., & Semeraro, G. (2022). Semantics and content-based recommendations. In Recommender systems handbook (pp. 251-298). Springer, New York, NY.


**---Ini adalah bagian akhir laporan---**
