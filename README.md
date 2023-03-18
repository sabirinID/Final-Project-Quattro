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

### 1.4 Univariate Analysis
Univariate Analysis dikakukan untuk melihat distribusi data dari setiap _feature_ secara terpisah.Bisa melihat distribusi data apakah berdistribusi normal, _left skew_, atau _right skew_ dengan menggunakan kdeplot. Kemudian melihat ada berapa banyak outlier yang ada pada setiap _feature_ dengan menggunakan boxplot.
#### 1.4.1 Data Distribution
Dari distribusi data dapat disimpulkan:
- Sebagian besar fitur memiliki distribusi yang _positively skewed_, karena nilai mean > median.
- Sebagian besar fitur memiliki _outlier_ atau pencilan.
- Fitur `OperatingSystem` distribusinya multimodal (nilai mode > 2).
- Fitur `Month` distribusinya mendekati bimodal dengan data tertinggi pada bulan Mei dan November.
- Fitur `VisitorType` dengan nilai Returning_Visitor sangat mendominasi.
- Fitur `Weekend` dengan nilai False mendominasi.
- Fitur `Revenue` dengan nilai False (tidak melakukan _purchasing_) sangat mendominasi.

Pada saat data pre-processing perlu dilakukan:
- Penghapusan _outlier_ pada setiap fitur bisa menggunakan IQR atau Z-Score.
- Melakukan transformasi fitur dengan _Log Transformation_, karena terdapat banyak fitur yang memiliki sebaran _right skew_ (Long Right Tailed)
- Melakukan _Feature Encoding_ untuk fitur `Month`, `Weekend`, dan `Revenue` menggunakan _Label Encoding_, sedangkan untuk fitur `VisitorType` menggunakan _One Hot Encoding_, karena terdapat nilai > 2 dan bukan tipe ordinal.
- Melakukan _Imbalance Class_ untuk fitur `Revenue`, karena fitur ini merupakan target yang mempunyai ketimpangan data yang signifikan.
### 1.5 Multivariate Analysis
Untuk melakukan Multivariate Analysis bisa menggunakan pair plot. Pair plot digunakan untuk menganalisa antar dua variabel pada data (bivariate analysis).
Pada bagian scatter plot dapat dilihat sebaran data dari dua variabel yang dipilih. Parameter hue bisa ditambahkan untuk mempertegas sebaran scatter plot setiap fitur terhadap target. dari Multivariate Analysis yang dilakukan didapatkan insight:
- Hampir tidak ada scatter plot dengan warna yang terpisah dengan baik.
- Fitur dengan pemisahan warna yang kurang baik bisa berpengaruh pada tingkat akurasi model.
- Scatter plot dengan sebaran warna yang terpisah mengindikasikan bahwa dataset memiliki kombinasi fitur yang baik.
- Satu-satunya kolom yang cukup baik untuk dijadikan fitur adalah PageValues yang menunjukkan pemisahan warna secara jelas.

#### 1.5.1 Data Correlation
Scatter plot menunjukkan perbedaan sebaran warna yang cukup mencolok, hal ini menandakan bahwa PageValues dengan Revenue memiliki korelasi yang cukup baik. untuk memperjelas pola hubungan PageValues dengan Revenue bisa digunakan point plot sehingga dapat diketahui bahwa Semakin tinggi nilai PageValues berbanding lurus dengan semakin tingginya nilai Revenue. PageValues dan Revenue memiliki pola hubungan positive linear association yang membentuk pola garis lurus berdasarkan Pearson Correlation.
Untuk mencari korelasi data secara mudah juga bisa menggunakan correlation heatmap. Fitur PageValues dan Revenue berkorelasi sedang (0,49), karena ketika tidak ada pembelian yang dilakukan, jumlah sesi dengan Page Values ​​= 0 relatif tinggi, yaitu sebanyak 9.230 sesi. Fitur BounceRates dan ExitRates berkorelasi tinggi (0,91), karena ketika Bounce Rate meningkat, Exit Rate juga meningkat berdasarkan hasil perhitungan oleh Google Analytics, sehingga kita memilih salah satu fitur, yaitu yang memiliki correlation lebih besar (ExitRates), atau bisa juga melakukan PCA. Korelasi antara durasi atau waktu yang dihabiskan pelanggan di halaman tertentu terhadap jumlahnya terlihat cukup jelas. sehingga dapat disimpulkan bahwa untuk menghasilkan Revenue, maka harus memiliki Bounce Rates yang rendah, Exit Rates yang rendah, dan Page Values yang tinggi.




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
