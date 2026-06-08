# E-Commerce Sales Analysis: End-to-End Data Pipeline & Visualization

## Deskripsi Proyek

Proyek ini menyajikan analisis komprehensif terhadap performa penjualan e-commerce. Menggunakan pendekatan *Extract, Transform, Load* (ETL) berbasis Python, data mentah diproses, distandardisasi, dan diperkaya melalui *feature engineering* untuk mengekstraksi *actionable insights*. Hasil pemrosesan data divisualisasikan dalam sebuah *dashboard* interaktif yang dirancang untuk memfasilitasi pemangku kepentingan dalam memantau metrik utama seperti pendapatan, profitabilitas, dan tren pergerakan produk.

## Tautan Proyek

* **Dashboard Visualisasi (Looker Studio)**:
[https://datastudio.google.com/s/nx7JKkoIsYc](https://datastudio.google.com/s/nx7JKkoIsYc)
* **Dokumentasi & Laporan Analisis (Notion)**:
[[https://app.notion.com/p/ANALISIS-PENJUALAN-E-COMMERCE-3780d45be53980f9a7fdd9d8a8e51816?source=copy_link](https://www.google.com/search?q=https%3A%2F%2Fapp.notion.com%2Fp%2FANALISIS-PENJUALAN-E-COMMERCE-3780d45be53980f9a7fdd9d8a8e51816%3Fsource%3Dcopy_link)](https://app.notion.com/p/ANALISIS-PENJUALAN-E-COMMERCE-3780d45be53980f9a7fdd9d8a8e51816?source=copy_link)

## Data Preparation & Cleansing

Proses pembersihan data dijalankan pada environment Jupyter Notebook/Google Colab memanfaatkan pustaka `pandas`. Dataset awal terdiri dari 200.000 baris data transaksi historis. Tahapan prapemrosesan meliputi:

* Penghapusan kolom *noise* (misalnya kolom 'Unnamed') yang memiliki proporsi *Missing Values* (NaN) absolut.
* Standardisasi *string* pada kolom dimensi seperti `Category`, `Product_Name`, `Province`, dan `Store_Location` menggunakan metode `.strip()` untuk mengeliminasi *whitespace* berlebih dan `.title()` untuk konsistensi format.
* Konversi tipe data pada kolom `Date` dari *string* menjadi *datetime object* untuk memungkinkan analisis *time-series* yang akurat.
* Dekomposisi variabel waktu dengan mengekstraksi atribut `Year`, `Month`, `Day`, dan `Month_Name` guna mengoptimalkan kapabilitas *filtering* dan agregasi temporal pada *dashboard*.
* Pembersihan format karakter non-numerik (seperti tanda titik dan spasi) pada kolom finansial `Unit_Price`, `Revenue`, serta `Unit Cost`, diikuti dengan *type casting* menjadi *integer/float*.

## Feature Engineering

Untuk memperluas dimensi analisis profitabilitas dan margin, variabel metrik kalkulatif ditambahkan ke dalam dataset:

* Pembentukan variabel turunan baru: `Profit`.
* Formula kalkulasi `Profit` dieksekusi berdasarkan persamaan matematis: `Revenue - (Unit Cost * Units_Sold)`.

## Skema Data Final

Output dari *pipeline* ETL disimpan sebagai dataset bersih yang telah divalidasi strukturalnya (File: `Data_Penjualan_Looker_Ready (1).csv`). Dataset ini bertindak sebagai *single source of truth* untuk visualisasi Looker Studio, dengan cakupan *features* sebagai berikut:

* **Identifikasi**: `Transaction_ID`
* **Temporal**: `Date`, `Year`, `Month`, `Day`, `Month_Name`
* **Produk**: `Product_Name`, `Category`
* **Kuantitas & Biaya**: `Units_Sold`, `Unit_Price`, `Unit Cost`
* **Performa Finansial**: `Revenue`, `Profit`
* **Demografi & Transaksi**: `Store_Location`, `Province`, `Payment_Method`
