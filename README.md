# 📊 Superstore Sales Executive Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Advanced_Formulas-0078D4?style=for-the-badge)
![Data Modeling](https://img.shields.io/badge/Data_Modeling-Star_Schema-107C41?style=for-the-badge)

## 📌 Dashboard Preview
![Dashboard Preview](dashboard_preview.png)

---

## 🎯 Project Overview
Proyek ini adalah aplikasi **Business Intelligence interaktif** yang dibangun menggunakan **Microsoft Power BI** untuk menganalisis performa penjualan historis dari jaringan ritel *Superstore*. 

Dashboard ini dirancang untuk menjawab pertanyaan-pertanyaan strategis di level eksekutif (C-Level & Sales Director), seperti pemantauan pendapatan utama, evaluasi pencapaian target tahunan per wilayah, analisis tren waktu, dan persebaran penjualan secara geografis di Amerika Serikat.

---

## ✨ Key Features & Interactivity
* **Executive KPI Cards:** Menampilkan metrik utama bisnis secara instan (*Total Sales* senilai **$2.26M** dan *Total Orders* sebanyak **5.009** transaksi unik).
* **Target vs. Actual Analysis:** Grafik batang perbandingan berdampingan (*Clustered Column Chart*) yang memvisualisasikan realisasi penjualan terhadap target bulanan/tahunan di tiap wilayah.
* **Dynamic Tooltips:** Kiat alat melayang yang dikonfigurasi menggunakan formula DAX untuk menampilkan persentase pencapaian target (**% Target Achieved**) secara akurat saat pengguna mengarahkan kursor ke atas grafik.
* **Geographical Mapping:** Pemetaan berbasis gelembung (*Bubble Map*) untuk mengidentifikasi area dengan volume penjualan tertinggi di seluruh negara bagian AS.
* **Time-Series Drill Down:** Analisis hierarki tanggal (*Date Hierarchy*) pada grafik garis untuk melihat fluktuasi dari level Tahun, Kuartal, Bulan, hingga Hari.
* **Interactive Slicer & Cross-Filtering:** Kendali filter wilayah (*Region*) interaktif yang memungkinkan pemotongan data secara serentak di seluruh komponen visualisasi.

---

## 🛠️ Data Modeling & Architecture
Proyek ini menerapkan praktik terbaik *Data Modeling* standar industri dengan membangun relasi antar-tabel menggunakan struktur **Star Schema**:
* **Tabel Fakta (`train`):** Berisi riwayat transaksi detail (Order ID, Order Date, Sales, City, State, dll.).
* **Tabel Dimensi (`Target_Wilayah`):** Berisi data target penjualan bulanan/tahunan.
* **Relationship:** Dibangun menggunakan relasi **Many-to-One (`* : 1`)** berdasarkan kolom **`Region`**, memungkinkan filter dari tabel target mengalir secara mulus ke tabel transaksi.

| Tabel Asal | Kolom Relasi | Jenis Relasi | Tabel Tujuan |
| :--- | :--- | :--- | :--- |
| `train` | Region | Many-to-One (`* : 1`) | `Target_Wilayah` |

---

## 💻 Advanced DAX Measures
Berikut adalah beberapa formula **Data Analysis Expressions (DAX)** utama yang ditulis dan digunakan di dalam mesin penghitung *dashboard* ini:

### 1. Menghitung Total Transaksi Unik
Mencegah duplikasi penghitungan pada keranjang belanja (*shopping cart*) dengan menghitung hanya nomor struk yang unik:
```dax
Total Transaksi = DISTINCTCOUNT('train'[Order ID])