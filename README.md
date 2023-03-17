# Online Shoppers Purchasing Intention
Final Project ini disusun sebagai salah satu syarat untuk menyelesaikan Data Science Career Bootcamp di <a href="https://www.rakamin.com/">Rakamin</a>.

<p align="center">
  <img src="Images/banner-by-namogoo.png" width="1024" height="auto">
  <br>
  Image by <a href="https://www.namogoo.com/">Namogoo</a>
</p>

## Authors and Contributors
* Dimas as Data Science Team Lead, Data Scientist
* Dila as Data Scientist
* Lana as Data Analyst
* Ucup as Data Analyst
* Aulia as Business Intelligence Analyst
* Keven as Business Intelligence Analyst
* Andre as Machine Learning Engineer

## Table of Contents
* [Preparation](#Stage-0-Preparation)
    * [Problem Statement](#01-Problem-Statement)
    * [Goal](#02-Goal)
    * [Objective](#03-Objective)
    * [Business Metrics](#04-Business-Metrics)
* [Exploratory Data Analysis](#Stage-1-Exploratory-Data-Analysis)
    * [Data Exploration](#11-Data-Exploration)
    * [Data Understanding](#12-Data-Understanding)
    * [Exploratory Data Analysis](#13-Exploratory-Data-Analysis)    
* [Data Preprocessing](#Stage-2-Data-Preprocessing)
    * [Data Cleansing](#21-Data-Cleansing)
    * [Feature Engineering](#22-Feature-Engineering)

## Stage 0. Preparation

### 0.1. Problem Statement

### 0.2. Goal

### 0.3. Objective

### 0.4. Business Metrics

## Stage 1. Exploratory Data Analysis

### 1.1. Data Exploration
Dataset [Online Shoppers Purchasing Intention](https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset/) merupakan dataset yang dibentuk secara khusus, sehingga setiap sesi akan dimiliki oleh pelanggan yang berbeda selama periode 1 tahun. Dataset ini terdiri dari 12.330 baris dan 18 kolom fitur, setiap baris berisi data yang berkaitan dengan sesi kunjungan (waktu yang dihabiskan) pelanggan pada situs e-commerce.

### 1.2. Data Understanding
#### 1.2.1. Data Dimension
Dataset ini memiliki dimensi data, yaitu
- Jumlah baris: 12.330
- Jumlah kolom: 18 
#### 1.2.2. Data Types and Structure
Untuk mendapatkan ringkasan singkat tentang dataset, kami menggunakan fungsi `info()`. Hasil observasi yang didapatkan adalah sebagai berikut.
- Dari total 18 kolom, ada 4 kolom atau fitur dengan tipe data yang kurang sesuai, yaitu `OperatingSystems`, `Browser`, `Region`, dan `TrafficType`, seharusnya string bukan integer, karena kemungkinan sudah melalui proses _label encoding_, sedangkan kolom lainnya sudah sesuai.
- Tidak ada kolom yang memiliki nilai kosong atau _missing values_.
- Tipe data berupa boolean (2), float (7), integer (7), dan string (2).
#### 1.2.3. Detect Missing Values
Untuk memastikan adanya _missing values_ dalam dataset, kita menggunakan metode `isna()`.
- Tidak ada kolom yang _null_ (bernilai None ataupun NaN).
#### 1.2.4. Detect Duplicates
Untuk menemukan adanya _duplicates_, kita menggunakan metode `duplicated()`. Ternyata ditemukan data duplikat sebanyak 125 baris. Walaupun demikian, kita berasumsi bahwa data tersebut merupakan data unik, yang terkait dengan sesi kunjungan pelanggan.
#### 1.2.5. Unique Elements
Untuk mencari elemen unik dalam dataset, kita menggunakan fungsi `nunique()`.
- Fitur `Administrative_Duration`, `Informational_Duration`, dan `ProductRelated_Duration` memiliki elemen unik yang cukup banyak, sehingga kita bisa hapus fitur ini atau kita bisa buat fitur baru `TotalPage_Duration`.
- Fitur `Administrative`, `Informational`, dan `ProductRelated` juga bisa buat fitur baru `TotalPage`.
- Fitur `BounceRates`, `ExitRates`, dan `PageValues` akan dipertahankan.

### 1.3. Descriptive Statistics
Untuk mendapatkan perincian statistik dasar dari dataset, kita menggunakan metode `describe()`.
#### 1.3.1. Numerical Features
Dalam fitur numerikal:
- Ada perbedaan yang signifikan antara nilai mean dan median (P50), yaitu mean > median, karena kemungkinan dipengaruhi oleh adanya _outlier_ atau pencilan, sehingga distribusi data akan cenderung menceng ke kanan atau _positively skewed_.
#### 1.3.2. Categorical Features
Berikut ini nilai yang paling umum dalam fitur kategorikal, berturut-turut adalah:
- `Month` : May (27,3%),
- `VisitorType` : Returning_Visitor (85,6%),
- `Weekend` : False (76,7%), dan
- `Revenue` : False (84,5%).

#### 1.3.3. Target Feature
Fitur `Revenue` digunakan sebagai _target feature_ atau label kelas.
- Dari total 12.330 sesi, 84,5% atau 10.422 sesi merupakan **kelas negatif** yang tidak diakhiri dengan pembelian, sedangkan 15,5% sisanya atau 1.908 sesi merupakan **kelas positif** yang diakhiri dengan pembelian.
- Dataset _imbalance_ atau tidak seimbang, karena proporsi data minoritas (dalam hal ini kelas positif) relatif rendah, dengan _degree of imbalance_: [moderate](https://developers.google.com/machine-learning/data-prep/construct/sampling-splitting/imbalanced-data/).
- Pada saat data pre-processing, kita perlu melakukan _handling imbalance data_, seperti
  - Oversampling: menduplikasi data minoritas
  - Undersampling: menghapus data mayoritas

### 1.4. Exploratory Data Analysis

## Stage 2. Data Preprocessing

### 2.1. Data Cleansing

### 2.2. Feature Engineering

## Stage 3. Business Insight

- Di daerah `Region` 1 memiliki jumlah pengunjung situs web e-commerce yang terbanyak. Solusi untuk meningkatkan ketertarikan pengunjung, kita bisa melakukan promosi ke daerah-daerah yang jarang mengunjungi situs web dengan memberikan penawaran spesial, seperti gratis ongkos pengiriman (ongkir).
- Pengunjung yang berkunjung pada _weekend_ lebih banyak dibandingkan dengan hari-hari biasa atau _weekday_, sehingga kita bisa mengadakan _event_ untuk menarik pelanggan melakukan transaksi pada _event_ tersebut.
- Bagi pelanggan yang sering berkunjung ke situs web dan melakukan transaksi akan mendapatkan kupon gratis belanja sebesar Rp50.000 yang dapat digunakan pada transaksi berikutnya untuk menarik minat pelanggan.
- Pada fitur `Month`, diketahui bahwa bulan Maret, Mei, November, dan Desember merupakan bulan-bulan yang sering dikunjungi pengunjung, Solusi kita, coba untuk mengadakan suatu _event_ di setiap bulan seperti event (yang dilakukan kompetitor) 1.1 hingga 12.12.

## License

The source code for the site is licensed under the MIT license, which you can find [here](https://github.com/sabirinID/Final-Project-Quattro/blob/main/LICENCE).

## References

Sakar, C. O. & Kasto, Y. (2018). UCI Machine Learning Repository. University of California, Irvine, School of Information and Computer Sciences. https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset

Sakar, C. O., Polat, S. O., Katircioglu, M., & Kasto, Y. (2019). Real-time prediction of online shoppers’ purchasing intention using multilayer perceptron and LSTM recurrent neural networks. Neural Computing and Applications, 31(11), 6893-6908. https://doi.org/10.1007/s00521-018-3523-0
