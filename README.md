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
- Bagaimana performa model dalam memprediksi film yang cocok dengan user?

### Goals
- Mengetahui judul film yang diberi rating tinggi oleh user.
- Membuat model machine learning yang bisa memberi rekomendasi film berdasarkan rating user sebelumnya.
- Mengetahui nilai error dengan menggunakan metrik RMSE untuk mengukur rata-rata kesalahan prediksi.
 
### Solution statements
- Melakukan data exploratory untuk menemukan jumlah judul film dan user yang memberikan rating.
- Menggunakan metode Collaborative filtering berbasis model.
- Membangun model dengan pendekatan deep learning, yang dapat memberikan user rekomendasi film untuk ditonton.
 
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
- `item_id` : id judul film
- `title` : judul film
- `user_id` : id user
- `rating`: penilaian user
- `timestamp` : durasi film
 
## Data Preparation

### Feature selection
- Menghapus kolom label yang tidak di perlukan, yaitu `timestamp`.
- Membuat variable `fix_title` yang nantinya akan diisi dengan dataframe yang sudah dihilangkan duplikat datanya.
### Data transformation
- Mengkonversi data series menjadi list pada data variable `fix_title` dengan tolist dari library numpy.
- Encode fitur `user_id` dan `Item_id` menjadi index integer menggunakan enumerate dari library python dan tolist dari library numpy.
- Mapping `user_id` dan `Item_id` ke dataframe, dan mengubah data `rating` menjadi float.
### Data Normalization
- Min Max scaling pada nilai rating dengan kode berikut
```python
    y = df['rating'].apply(lambda x: (x - min_rating) / (max_rating - min_rating)).values
```
### Train Test Split
- Train test split dengan mengacak data, dan membagi langsung 80% data train dan 20% data validasi.
 
## Modeling
Tahap awal modeling adalah, dengan membuat class yang berisi layer embedding dengan activation sigmoid. Layer embedding merupakan layer perkalian matrix sederhana yang mengubah integer positif (index) menjadi vector dense dengan ukuran tetap, output fungsi sigmoid dalam rentang (0, 1), membuatnya ideal untuk masalah klasifikasi biner di mana kita perlu menemukan probabilitas data milik kelas tertentu.
selanjutnya compile model, model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer dengan learning_rate = 0.0001, dan root mean squared error (RMSE) sebagai metrics evaluation. Dilanjutkan dengan training model dengan parameter batch_size = 50, dan epochs = 100. Membuat variable untuk memuat data film yang belum di tonton user berdasarkan dataframe `title_new` yang sudah di buat sebelumnya, gunakan fungsi predict dan lakukan penyesuaian dengan variable yang telah di buat sebelumnya untuk menampilkan top-N recommendation sebagai berikut.
\
![30c917b0ff610db88e7788439b814816.png](https://zippyimage.com/images/2021/11/19/30c917b0ff610db88e7788439b814816.png)

## Evaluation

RMSE merupakan nilai rata-rata dari jumlah kuadrat kesalahan atau jumlah kuadrat dari nilai prakiraan dan observasi                           
Karna yang ingin kita analisis adalah besarnya kesalahan prediksi, maka digunakan RMSE yang mana semakin kecil nilai nya/mendekati atau sama dengan 0, maka performa model semakin bagus, RMSE dihitung dengan mengkuadratkan error (prediksi – observasi) dibagi dengan jumlah data (= rata-rata), lalu diakarkan.    

Rumus RMSE adalah sebagai berikut.
RMSE = \sqrt{\frac{\sum_{n}^{i=1}(\hat{y}-y_{i})^{2}}{n}}
\
berikut merupakan visualisasi hasil training model dengan metrics RMSE.
\
![visual](https://zippyimage.com/images/2021/11/16/fac426f1f73243b98c9015c4993a5fc3.png)
\
Visualisasi diatas menunjukan nilai rata-rata error yang cukup rendah, yaitu diangka 0.23 untuk data training, dan 0.24 untuk data validasi, selisih error antara data training dan validasi juga sangat kecil, yang menunjukan model ini relatif dapat memprediksi dengan cukup baik.
 
**---Ini adalah bagian akhir laporan---**


 
