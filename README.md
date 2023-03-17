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
- Jumlah baris: 12330
- Jumlah kolom: 18 
#### 1.2.2. Data Types and Structure
Untuk mendapatkan ringkasan singkat tentang dataset, kami menggunakan fungsi `info()`. Hasil observasi yang didapatkan adalah sebagai berikut.
- Dari total 18 kolom, ada 4 kolom fitur dengan tipe data yang kurang sesuai, yaitu `OperatingSystems`, `Browser`, `Region`, dan `TrafficType`, seharusnya string bukan integer, kemungkinan sudah melalui proses _label encoding_, sedangkan kolom lainnya sudah sesuai.
- Tidak ada kolom yang memiliki nilai kosong atau _missing values_.
- Tipe data berupa boolean (2), float (7), integer (7), dan string (2).

### 1.3. Exploratory Data Analysis

## Stage 2. Data Preprocessing

### 2.1. Data Cleansing

### 2.2. Feature Engineering

## License

The source code for the site is licensed under the MIT license, which you can find [here](https://github.com/sabirinID/Final-Project-Quattro/blob/main/LICENCE).

## References

Sakar, C. O. & Kasto, Y. (2018). UCI Machine Learning Repository. University of California, Irvine, School of Information and Computer Sciences. https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset

Sakar, C. O., Polat, S. O., Katircioglu, M., & Kasto, Y. (2019). Real-time prediction of online shoppers’ purchasing intention using multilayer perceptron and LSTM recurrent neural networks. Neural Computing and Applications, 31(11), 6893-6908. https://doi.org/10.1007/s00521-018-3523-0
