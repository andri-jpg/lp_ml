# Laporan Proyek Machine Learning - Andrian Syah putra

## Project Overview
Film merupakan salah satu produk dari media massa, film juga merupakan media hiburan dan merupakan salah satu cara berkomunikasi yang menampilkan gambar ( visual ) dan suara ( audio ) secara bersamaan atau biasa disebut media massa audio visual seperti pada Televisi. Selain itu film ditampilkan pada khalayak luas dan film mampu menyampaikan pesan secara mudah dengan adegan – adegan yang diperagakan. Terkadang kita sedikit kesulitan untuk mencari film yang cocok dan mungkin kita sukai, dikarnakan ada begitu banyak daftar film yang ada.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Agar khalayak umum dapat dengan mudah mendapatkan rekomendasi film yang cocok dan mungkin di sukai.
- Referensi : [Universitas Muhammadiyah Ponorogo](http://eprints.umpo.ac.id/4237/2/BAB%20I.pdf#:~:text=A.%20Latar%20Belakang%20Masalah%20Film%20merupakan%20salah%20satu,dan%20merupakan%20salah%20satu%20cara%20berkomunikasi%20yang%20menampilkan) 

## Business Understanding

### Problem Statements
- Film apa yang diberi rating tinggi oleh user?
- Bagaimana agar user mendapatkan rekomendasi film untuk ditonton?
- Metrik apa yang akan digunakan untuk mengukur seberapa akurat prediksi film yang mungkin cocok dengan user?

### Goals
- Mengetahui judul film yang diberi rating tinggi oleh user.
- Membuat model machine learning yang bisa memberi rekomendasi film berdasarkan rating user sebelumnya.
- Menggunakan metrik RMSE untuk mengukur rata-rata kesalahan prediksi.

### Solution statements
- Melakukan data exploratory untuk menemukan jumlah judul film dan user yang memberikan rating.
- Membangun model dengan pendekatan deep learning, yang dapat memberikan user rekomendasi film untuk ditonton.
- Membuat class recommenderNet dengan layer embedding dari library tensorflow dan keras.
- Layer embedding merupakan layer perkalian matrix sederhana yang mengubah integer positif (index) menjadi vector dense dengan ukuran tetap.
- Melakukan training dan hyperparameter tuning pada learning_rate optimizer untuk mendapatkan error sekecil mungkin.

## Data Understanding
Jumlah user yang memberi rating adalah 944, dan jumlah judul film adalah 1682, Hasil ini berdasarkan kode berikut.
```python 
    print('jumlah user :', len(df.user_id.unique()))
    print('jumlah judul film :', len(df.item_id.unique()))
```
dengan output sebagai berikut:
\
![output](https://zippyimage.com/images/2021/11/16/a914136721934a32c7dddc94eb9a7796.png)

Dataset yang digunakan memiliki 1682 judul film, 944 user, 100002 baris data, dan label rating dengan rentang 1 sampai 5.
Sumber dataset : [kaggle](https://www.kaggle.com/zeeshanmulla/recommendation-system-movie/code)

### Variabel-variabel pada movie_id_title dan Recommendation_system adalah sebagai berikut:
* item_id : id judul film
- title : judul film
- user_id : id user
- rating : penilaian user

## Data Preparation

- Membuat variable fix_title yang nantinya akan diisi dengan dataframe yang sudah dihilangkan duplikat datanya.
- Mengkonversi data series menjadi list pada data variable fix_title dengan tolist dari library numpy.
- Membuat variable title_new yang berisi dictionary key value untuk label user_id, title_id, dan rating_title, yang nantinya akan digunakan untuk membuat data judul film yang belum di tonton/diberi rating oleh user.
- Encode fitur user_id dan Item_id menjadi index integer menggunakan enumerate dari library python dan tolist dari library numpy.
- Mapping user_id dan Item_id ke dataframe, dan mengubah data rating menjadi float.
- Train test split dengan mengacak data, dan membagi langsung 80% data train dan 20% data validasi.

## Modeling
Tahap awal modeling adalah, dengan membuat class yang berisi layer embedding dengan activation sigmoid. Layer embedding merupakan layer perkalian matrix sederhana yang mengubah integer positif (index) menjadi vector dense dengan ukuran tetap, output fungsi sigmoid dalam rentang (0, 1), membuatnya ideal untuk masalah klasifikasi biner di mana kita perlu menemukan probabilitas data milik kelas tertentu.
selanjutnya compile model, model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer dengan learning_rate = 0.0001, dan root mean squared error (RMSE) sebagai metrics evaluation. Dilanjutkan dengan training model dengan parameter batch_size = 50, dan epochs = 100. Membuat variable untuk memuat data film yang belum di tonton user berdasarkan dataframe title_new yang sudah di buat sebelumnya, gunakan fungsi predict dan lakukan penyesuaian dengan variable yang telah di buat sebelumnya untuk menampilkan top-N recommendation sebagai berikut.
\
![top](https://zippyimage.com/images/2021/11/18/501fdb447cd14c24fc2a2686013bcc08.png)
## Evaluation
Karna yang ingin kita analisis adalah besarnya kesalahan prediksi, maka digunakan RMSE yang mana semakin kecil nilai nya/mendekati atau sama dengan 0, maka performa model semakin bagus, berikut merupakan visualisasi hasil training model dengan metrics RMSE.
\
![visual](https://zippyimage.com/images/2021/11/16/fac426f1f73243b98c9015c4993a5fc3.png)
\
Visualisasi diatas menunjukan nilai rata-rata error yang cukup rendah, yaitu diangka 0.22 untuk data training, dan 0.23 untuk data validasi, selisih error antara data training dan validasi juga sangat kecil, yang menunjukan model ini relatif dapat memprediksi dengan cukup baik.

RMSE merupakan nilai rata-rata dari jumlah kuadrat kesalahan atau jumlah kuadrat dari nilai prakiraan dan observasi.


**---Ini adalah bagian akhir laporan---**
