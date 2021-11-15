# Laporan Proyek Machine Learning - Andrian Syah putra
 
## Teknologi
 
Penggunaan komputer sampai saat ini terus meningkat tiap tahunnya, Hampir segala bidang memerlukan komputer, contohnya pendidikan, bisnis, pemerintahan dan lainnya. Harga komputer berbeda beda sesuai dengan spesifikasinya, tinggal kita sesuaikan kebutuhan saja, karna banyaknya model part komputer dipasaran membuat kita sedikit kesulitan untuk memprediksi harga komputer sesuai spesifikasi yang kita inginkan.
 
**Rubrik/Kriteria Tambahan**:
- Agar khalayak umum dapat memprediksi harga komputer sebelum membeli,dengan membuat model ML yang dapat memprediksi harga komputer.
- Referensi : [5 Kegunaan komputer dalam kehidupan sehari-hari](https://tekno.kompas.com/read/2021/09/21/20030027/5-kegunaan-komputer-dalam-kehidupan-sehari-hari)
 
## Business Understanding
 
### Problem Statements
 
- Dari beberapa fitur yang ada,yang mana yang paling berpengaruh ke harga komputer.
- Fitur apa yang paling tidak berpengaruh terhadap harga komputer.
- Apakah komputer dengan cd lebih mahal daripada komputer tanpa cd?.
- Berapa harga komputer berdasarkan spesifikasi tertentu.
 
### Goals
 
- Mengetahui fitur yang paling berpengaruh terhadap harga.
- Mengetahui fitur yang paling tidak berpengaruh terhadap harga komputer.
- Mengetahui apakah komputer dengan cd lebih mahal daripada tanpa cd.
- Membuat model machine learning yang dapat memprediksi harga komputer berdasarkan spesifikasinya seakurat mungkin.
 
 
### Solution statements
- Melakukan visualisasi data untuk mencari fitur yang paling berpengaruh terhadap harga komputer.
- Menggunaakan 3 algoritma yaitu RF, KNN, dan boosting.
- Kemudian mengevaluasi ketiga algoritma tersebut untuk mendapatkan model dengan akurasi tertinggi.
- Setelah mendapatkan model dengan akurasi tertinggi, barulah dilakukan hyperparameter tuning.
- Melakukan hyperparameter tuning pada baseline untuk mendapatkan akurasi seakurat mungkin.                             
 
## Data Understanding
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
- Mempersiapkan variable models untuk mengumpulkan hasil predict model yang akan dievaluasi.
- Model pertama adalah KNN, dengan parameter n_neighbors=7.
- Model kedua adalah RandomForest, dengan parameter n_estimator=75, max_depth=16, n_jobs=-1.
- model ketiga adalah boosting, dengan parameter n_estimator=43, learning_rate=0.04.
- Kemudian memanggil fungsi fit pada setiap model untuk melakukan training.
- Memanggil fungsi predict pada setiap model untuk mendapat hasil prediksi.
                                
## Evaluation
Karna untuk menyelesaikan kasus regresi, Model ini menggunakan metrik evaluasi Mean Squared Error, Dengan hasil sebagai berikut.
\
![test](https://zippyimage.com/images/2021/11/12/bd5e4e8508eba8de2a5e79a752fef810.png)
\
![visual](https://zippyimage.com/images/2021/11/15/21283abe5f25e273dee68b8071eee66a.png)

- Mean Squared Error Bertujuan memberi tahu seberapa dekat garis regresi dengan sekumpulan poin.
- Berdasarkan hasil evaluasi, algoritma Random forest memiliki nilai prediksi paling mendekati nilai asli.

![hasil](https://zippyimage.com/images/2021/11/15/7d203414acf50bd3181037fc5e2d9940.png)

**---Ini adalah bagian akhir laporan---**
