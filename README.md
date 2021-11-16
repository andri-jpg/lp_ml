# Laporan Proyek Machine Learning - Andrian Syah putra
 
## Domain Proyek
 
Penggunaan komputer sampai saat ini terus meningkat tiap tahunnya, Hampir segala bidang memerlukan komputer, contohnya pendidikan, bisnis, pemerintahan dan lainnya. Harga komputer berbeda beda sesuai dengan spesifikasinya, tinggal kita sesuaikan kebutuhan saja, karna banyaknya model part komputer dipasaran membuat kita sedikit kesulitan untuk memprediksi harga komputer sesuai spesifikasi yang kita inginkan.
 
**Rubrik/Kriteria Tambahan**:
- Agar khalayak umum dapat memprediksi harga komputer sebelum membeli,dengan membuat model ML yang dapat memprediksi harga komputer.
- Referensi : [5 Kegunaan komputer dalam kehidupan sehari-hari](https://tekno.kompas.com/read/2021/09/21/20030027/5-kegunaan-komputer-dalam-kehidupan-sehari-hari)
 
## Business Understanding
 
### Problem Statements
 
- Dari beberapa fitur yang ada,yang mana yang paling berpengaruh ke harga komputer?
- Fitur apa yang paling tidak berpengaruh terhadap harga komputer?
- Apakah komputer dengan cd lebih mahal daripada komputer tanpa cd?
- Berapa harga komputer berdasarkan spesifikasi tertentu?
 
### Goals
 
- Mengetahui fitur yang paling berpengaruh terhadap harga.
- Mengetahui fitur yang paling tidak berpengaruh terhadap harga komputer.
- Mengetahui apakah komputer dengan cd lebih mahal daripada tanpa cd.
- Membuat model machine learning yang dapat memprediksi harga komputer berdasarkan spesifikasinya seakurat mungkin.
 
 
### Solution statements
- Melakukan visualisasi data untuk mencari fitur yang paling berpengaruh terhadap harga komputer.
- Menggunaakan 3 algoritma yaitu RF, KNN, dan boosting.

1. Algoritma RandomForest (RF) termasuk kedalam kategori model ensemble. RF merupakan versi bagging dari decision tree, pada kasus regresi hasil prediksi merupakan rata rata prediksi seluruh pohon decision tree pada model ensemble.

2. KNN bekerja dengan membandingkan jarak sample ke sample pelatihan lain dengan memilih sejumlah k-tetangga terdekat.

3. Algoritma Boosting bekerja dengan menggambungkan beberapa model sederhana sehingga membentuk model yang kuat, model pertama dibangun dari data latih, kemudian ia membuat model kedua untuk memperbaiki kesalahan model pertama, begitu seterusnya sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum.

- Kemudian mengevaluasi ketiga algoritma tersebut untuk mendapatkan model dengan akurasi tertinggi.
- Setelah mendapatkan model dengan akurasi tertinggi, barulah dilakukan hyperparameter tuning.
- Melakukan hyperparameter tuning pada baseline untuk mendapatkan akurasi seakurat mungkin.                             
 
## Data Understanding
Fitur yang paling berpengaruh terhadap harga pada dataset ini adalah ram, sedangkan yang paling tidak berpengaruh adalah ads, seperti yang terlihat di correlation matrix berikut
\
[corr](https://zippyimage.com/images/2021/11/15/a2969e740d05f7968e2c6d3f14a85af4.png)        
\
Komputer dengan cd ternyata memiliki harga yang lebih tinggi seperti yang terlihat di visualisasi berikut
[viscd](https://zippyimage.com/images/2021/11/15/9147f4a5e1ca7e7804ee30322e6befc5.png)

Dataset yang digunakan memiliki 6259 tipe komputer dengan spesifikasi yang berbeda beda, dan memiliki 10 label yang mana label price merupakan fitur target. Sumber dataset: [Kaggle](https://www.kaggle.com/ritikmaheshwari/computer-price-prediction?select=ComputerPricesData.csv).
 
 
### Variabel-variabel pada ComputerPriceData adalah sebagai berikut:
- price : harga dalam Rupee
- speed : kecepatan komputer
- hd : kapasitas hardisk
- cd : ada tidaknya CD rom
- multi : apakah memiliki port multi?
- ads : frekuensi iklan
- trend : tren di pasar
- premium : apakah komputer tersebut premium?
- ram : Ukuran ram
- screen : ukuran monitor
 
 
## Data Preparation

1. Encoding fitur kategori.
Karna dalam dataset yang digunakan terdapat fitur kategori, dan komputer tidak bisa memproses data berbentuk kategori, maka dilakukan encoding, dalam kasus ini kita menggunakan teknik One-Hot encoding dari library sklearn.

2. Train test split
Untuk membagi data train dan data test, disini kita menggunakan Train_test_split dari library sklearn dengan ukuran test data sebesar 20% dan data train sebesar 80%.

3. Standarisasi
Melakukan scaler pada data numerik agar mendekati disribusi normal, hal ini membantu meningkatkan performa model yang kita bangun, dalam kasus ini kita menggunakan StandardScaler dari library sklearn.
                     
## Modeling
1. Kelebihan algoritma random forest yaitu dapat mengatasi noise dan missing value, cocok digunakan dalam jumlah data yang besar, namun sulit untuk interpretasi dan membutuhkan tuning yang tepat.
2. Kelebihan algoritma KNN adalah pelatihan nya sangat cepat dan mudah di pelajari sedangkan kekurangannya adalah nilai k sering bias, keterbatasan memori dan mudah tertipu atribut yang tidak relevan.
3. kelebihan algoritma boosting adalah mampu membangun model yang kuat dengan ensemble algoritma lemah, namun sulit untuk menentukan parameter yang tepat.

- Mempersiapkan variable models untuk mengumpulkan hasil predict model yang akan dievaluasi.
- Model pertama adalah KNN, dengan parameter n_neighbors=25.
- Model kedua adalah RandomForest, dengan parameter n_estimator=30, max_depth=15, n_jobs=-1.
- model ketiga adalah boosting, dengan parameter n_estimator=38, learning_rate=0.09.
- Kemudian memanggil fungsi fit pada setiap model untuk melakukan training.
- Memanggil fungsi predict pada setiap model untuk mendapat hasil prediksi.
                                
## Evaluation
Karna untuk menyelesaikan kasus regresi, Model ini menggunakan metrik evaluasi Mean Squared Error, Dengan hasil sebagai berikut.
\
![test](https://zippyimage.com/images/2021/11/15/2aae08ff1a2a49dde060028fc856eb99.png)
\
![visual](https://zippyimage.com/images/2021/11/15/5e3a46462be91d0b87d3919d99de0e57.png)

- Mean Squared Error Bertujuan memberi tahu seberapa dekat garis regresi dengan sekumpulan poin.
- Berdasarkan hasil evaluasi, algoritma Random forest memiliki nilai prediksi paling mendekati nilai asli.

![hasil](https://zippyimage.com/images/2021/11/15/ee3a9c01dd57296797ac632c16e8b2b6.png)

**---Ini adalah bagian akhir laporan---**
