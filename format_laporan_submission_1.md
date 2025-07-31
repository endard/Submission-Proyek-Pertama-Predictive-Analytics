# Laporan Proyek Machine Learning - Endar Danang Suprayogo

## Domain Proyek

Pada industri properti, penentuan harga rumah biasanya bergantung pada intuisi agen atau estimasi manual yang mungkin tidak selalu akurat. Dengan adanya perkembangan teknologi Data Science dan Machine Learning, penentuan harga properti dapat diprediksi secara lebih akurat berdasarkan data historis yang telah ada. Proyek ini bertujuan untuk mengembangkan model prediksi harga rumah menggunakan data-data seperti lokasi bangunan, luas bangunan, jumlah kamar, jumlah kamar mandi, dan tahun pembangunan, guna memberikan prediksi harga yang lebih objektif dan membantu berbagai pihak dalam mengambil keputusan jual beli properti.

## Business Understanding

### Problem Statements

- Bagaimana cara memprediksi harga rumah berdasarkan fitur-fitur seperti lokasi bangunan, luas bangunan, jumlah kamar, jumlah kamar mandi, dan tahun pembangunan?
Pernyataan permasalahan ini berfokus dalam memperkirakan harga rumah secara akurat dengan memanfaatkan variabel-variabel yang umumnya memengaruhi nilai properti. Fitur seperti luas bangunan (SquareFeet), lokasi (Neighborhood), jumlah kamar (Bedrooms), kamar mandi (Bathrooms), dan tahun pembangunan (YearBuilt) perlu dianalisis untuk membangun model prediktif yang andal.

- Apa saja fitur yang paling mempengaruhi harga rumah?
Pertanyaan permasalahan ini bertujuan untuk mengidentifikasi variabel mana yang memiliki dampak paling signifikan terhadap harga rumah.

### Goals

- Mengembangkan model machine learning untuk memprediksi harga rumah.
Tujuan utama proyek ini adalah membangun sebuah model machine learning (seperti Random Forest, KNN, atau Boosting) yang dapat memprediksi harga rumah berdasarkan data historis. Model ini diharapkan dapat memberikan estimasi yang akurat, sehingga berguna bagi penjual maupun pembeli properti.

- Mengetahui fitur yang paling mempengaruhi harga rumah.
Proyek ini juga bertujuan untuk memberikan insight bisnis tentang variabel kunci yang mendorong harga rumah.

## Data Understanding
Data ini memiliki 6 kolom dan 50.000 baris data. Variabel target pada data ini adalah "Price". Serta format yang digunakan adalah CSV. Data yang digunakan merupakan data yang bersih yang berarti bebas dari missing value dan data duplikat. Setiap nilai outlier tidak diubah nilainya karena merupakan nilai yang mencerminkan kondisi pasar yang beragam. [Housing Price Prediction Data](https://www.kaggle.com/datasets/muhammadbinimran/housing-price-prediction-data).

### Variabel-variabel pada Housing Price Prediction Data adalah sebagai berikut:
- SquareFeet : merupakan luas keseluruhan bangunan.
- Bedrooms : merupakan jumlah seluruh kamar tidur di dalam rumah.
- Bathrooms : merupakan jumlah seluruh kamar mandi di dalam rumah.
- Neighborhood : merupakan daerah lingkungan tempat rumah itu berada.
- YearBuilt : merupakan tahun dimana bangunan dibuat.
- Price : merupakan harga rumah.

## Data Preparation
Dalam proses persiapan data untuk analisis lebih lanjut, dilakukan beberapa langkah penting sebagai berikut:
1. Pertama, konversi kolom Neighborhood dengan One-hot Encoding untuk mengubah variabel kategorikal menjadi bentuk numerik yang dapat diproses oleh model machine learning. 
2. Kedua, mengubah kolom YearBuilt menjadi BuildingAge dengan menghitung selisih tahun sekarang terhadap tahun pembangunan, sehingga lebih mudah memahami umur bangunan sebagai fitur prediktif. 
3. Ketiga, dilakukan split dataset dan scaling data train untuk membagi data menjadi training set dan testing set.
4. Terakhir, melakukan normalisasi atau standarisasi pada data train agar model dapat belajar lebih efektif tanpa bias dari perbedaan skala fitur. 
Langkah-langkah tersebut membantu meningkatkan kualitas data sebelum masuk ke tahap pemodelan.

## Modeling
Pada tahap ini dilakukan pengembangan model machine learning untuk menyelesaikan permasalahan prediksi dengan membandingkan tiga algoritma berbeda, yaitu K-Nearest Neighbor (KNN), Random Forest, dan Boosting Algorithm (AdaBoost). Setiap algoritma diuji performanya menggunakan data yang telah diproses sebelumnya, termasuk fitur-fitur seperti BuildingAge dan hasil one-hot encoding dari Neighborhood.

Pada model KNN menggunakan algoritma KNeighborsRegressor dengan parameter n_neighbors bernilai 10. Maka algoritma akan mengecek harga ke dalam 10 data terdekat bedasarkan kemiripan fitur. Lalu menghitung harga rata-rata dari 10 data tersebut untuk dijadikan hasil prediksi.

Model Random Forest menggunakan algoritma RandomForestRegressor dengan parameter n_estimators bernilai 24, kedalaman maksimum max_depth sebesar 8, random_state sebanyak 42, dan n_jobs bernilai -1. Maka algoritma akan membuat sebanyak 24 pohon keputusan dengan kedalaman maksimal sebanyak 8 cabang, dengan data yang digunakan secara acak dan menggunakan semua cpu yang tersedia. 

Pada model Boosting menggunakan algoritma AdaBoostRegressor dengan parameter learning_rate bernilai 0.05 dan random_state sebanyak 42. Maka dengan menggunakan AdaBoost setiap model yang baru akan memperbaiki kesalahan model sebelumnya dan setiap model baru akan memiliki pengaruh sebesar 0.05 terhadap hasil prediksi. Data yang digunakan pada proses merupakan data yang acak.

## Evaluation
Setelah dilakukan pelatihan pelatihan, dilakukan evaluasi dan model dengan kinerja terbaik dipilih berdasarkan metrik evaluasi Mean Squared Error (MSE) terbaik. 

Berikut merupakan nilai dari MSE yang dihasilkan:
KNN	
train 22.604,983946	
test 27.001,187923

RF	
train 23.927,033786	
test 24.649,902284

Boosting	
train 25.544,243797	
test 24.808,125484

Berdasarkan hasil evaluasi terhadap tiga algoritma yang diuji, Random Forest terbukti memiliki performa terbaik dibandingkan dengan K-Nearest Neighbor (KNN) dan Boosting Algorithm. Model Random Forest menghasilkan MSE yang lebih baik dibanding dengan model yang lain, menunjukkan kemampuannya dalam menangani data dengan baik. Pemilihan ini memastikan bahwa solusi yang dihasilkan optimal dan siap digunakan untuk prediksi di dunia nyata.

Berdasarkan analisis feature importance dari model Random Forest, ditemukan bahwa SquareFeet merupakan fitur yang paling berpengaruh dalam menentukan harga rumah. Nilai kepentingan (importance score) dari SquareFeet secara signifikan lebih tinggi dibandingkan fitur-fitur lainnya, seperti BuildingAge (umur bangunan) atau Bedrooms. Hal ini menunjukkan bahwa semakin besar luas bangunan, semakin tinggi pula harga rumah, yang sejalan dengan logika pasar properti pada umumnya.

**---Ini adalah bagian akhir laporan---**