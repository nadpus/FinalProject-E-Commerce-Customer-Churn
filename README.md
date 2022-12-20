# **E-Commerce Customer Churn Analysis and Prediction**

Created by:
1. Nadia Puspitasari
2. Matthew Nicholas
3. Rayhan Romy Syahputra

(this file is reupload and has been revised from the [original source](https://github.com/PurwadhikaDev/BetaTeam_JC_DS_1802_LS_03_FinalProject))

---

## Context

Sebuah perusahaan X di Amerika Serikat memiliki bisnis di bidang E-Commerce dimana pembeli dan penjual bisa bertransaksi (melakukan penjualan/pembelian) melalui website tersebut. Transaksi pembelian dari website E-Commerce bisa datang dari berbagai kategori barang/jasa. Perusahaan X mendapatkan keuntungan dari tiap transaksi yang dilakukan oleh customer, sehingga adanya pertumbuhan customer dibutuhkan agar perusahaan bisa mendapatkan lebih banyak keuntungan. Di beberapa tahun terakhir perusahaan mengalami pertumbuhan customer yang cukup baik, namun dari data terbaru mulai menunjukkan bahwa adanya peningkatan customer yang churn dari keseluruhan customer di website E-Commerce tersebut. 

Sebagai konteks, ada dua cara agar perusahaan dapat mempertahankan pertumbuhan keuntungan. Pertama yaitu mempertahankan customer lama agar menetap sebagai customer. Cara kedua yaitu mencari customer baru. Berdasarkan statistik dari berbagai industri bisnis, hasil riset menemukan bahwa customer acquisition memiliki biaya 4-5x lipat lebih dari customer retention

Pada kesimpulannya, mendapatkan customer baru memakan biaya yang lebih banyak dibandingkan dengan mempertahankan customer lama untuk tidak churn sehingga kita harus lebih fokus ke customer retention. Sehingga, perusahaan harus memikirkan cara untuk memprediksi customer yang berpotensi untuk churn dan memberikan treatment yang diperlukan agar customer menetap di platform E-Commerce perusahaan.

Kita asumsikan perusahaan per tahunnya menggelontorkan dana $100.000 untuk memaintain 1000 customer lama. Sehingga **retention cost: $100/customer**

Sedangkan, customer acquisition cost yang dihabiskan oleh perusahaan sebanyak $450.000 untuk mendapatkan 1000 customer baru. Sehingga **acquisition Cost: $450/customer**

## Problem Statement

Salah satu tantangan yang dihadapi oleh bisnis E-Commerce adalah untuk membuat customer agar menetap dan tetap melakukan transaksi. **Perusahaan mengalami penurunan pertumbuhan customer akibat customer churn yang mengakibatkan keuntungan perusahaan stagnan/berkurang**.

## Goals

Berdasarkan masalah yang dihadapi, perusahaan harus bisa **memprediksi customer mana saja yang berpotensi untuk churn, lalu memberikan treatment yang tepat untuk customer tersebut agar tidak churn**. Sehingga perusahaan bisa **mempertahankan keuntungan** yang telah didapatkan. Juga, **meminimalisir retention cost yang diperlukan** untuk customer yang mau melakukan churn.

## Analytic Approach

Kita akan menganalisis data untuk menemukan pola yang membedakan customer yang akan churn atau yang tidak churn. Kemudian kita akan membangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi customer akan churn atau tidak.

## Metric Evaluation

Target:
- 0: customer tidak churn
- 1: customer churn

Cost FN (False Negative):
- Kekurangan
    - Kehilangan customer (alias churn)
    - Adanya cost customer acquistion untuk menggantikan customer yang telah churn   

Cost FP (False Positive):
- Kelebihan
    - Akibat dari salah treatment terhadap customer yang sebenarnya tidak churn tapi diprediksi churn, maka reputasi E-Commerce semakin baik (customer yang tidak churn akan mengira bahwa plaform E-Commerce murah hati untuk memberikan promo secara cuma-cuma)
    <br><br>
- Kekurangan
    - Salah target treatment untuk customer yang tidak churn (tapi diprediksi churn)
    - Sia-sianya biaya customer retention, waktu dan sumber daya

Berdasarkan konsekuensinya, maka sebisa mungkin yang akan kita lakukan adalah membuat model yang dapat mengurangi cost customer retention dari perusahaan tersebut tetapi tanpa harus ada customer yang churn dari website E-Commerce perusahaan. Oleh karena itu, kita memutuskan untuk menitikberatkan ke False Negative, tetapi juga tidak lupa dengan False Positive, dengan lebih menitikberatkan pada recall. Maka dari itu focus metric yang kita gunakan adalah **F2-Score**.

## Exploratory Data Analysis

Setelah dibuatkannya visualisasi atas distribusi data dan korelasi data antar variabel, selanjutnya akan dilakukan data analisis. Sebelum dilakukan analisis, kami memiliki asumsi-asumsi terkait analisis customer churn ini. Adapun asumsi kami akan dituangkan dalam beberapa pertanyaan sebagai berikut:
- Apakah customer yang berhenti menggunakan langganan ecommerce berhenti di awal bulan penggunaan layanan?
- Apakah customer yang mengajukan complain cenderung berhenti menggunakan layanan ecommerce?
- Apakah angka kepuasan yang rendah akan menunjukkan tingkat churn yang tinggi?
- Apakah customer yang keluar dari layanan ecommerce tidak lagi melakukan order pembelanjaan seminggu terakhir?
- Bagaimana pembelian produk dari customer yang churn? Apakah berpengaruh dari cashback yang didapatkan?
- Apakah ada metode pembayaran tertentu yang berhubungan dengan customer churn?
- Apakah customer yang login menggunakan handphone lebih banyak yang berhenti dari layanan ecommerce?
- Apakah customer laki-laki dan customer yang sudah menikah yang lebih banyak berhenti dari layanan ecommerce?

## Data Preprocessing

1. Drop duplicates.
2. Drop outlier menggunakan metode IQR.
3. Impute missing value.
4. Encoding untuk categorical data.

## Modeling

Proses modeling lebih lengkap terlampir pada notebook.

## Conclusion

Statistik Churn menggunakan y_test (20%): 
- 0: 430
- 1: 84
- **Total data**: 514

<u>**Tanpa model:**</u>

Tanpa model, kita sulit untuk mengetahui customer mana yang churn atau tidak, Maka perhitungannya:
- Total customer yang pasti churn setelah diberi promo: 84 orang,
- Acquisition cost untuk menggantikan customer yang churn:
    **84 * 450 USD = 37800 USD**
- Total Biaya: 37800 USD
- Jumlah penghematan: 0 USD

sehingga potensi biaya akuisisi yang dikeluarkan menjadi lebih banyak.
<br><br>

<u>**Dengan model (test set yakni 20%):**</u>

Total data: 514

Berdasarkan confusion matrix:
- Biaya untuk promosi: (76+11) * 100 USD = 8700 USD
- Acquisition cost untuk menggantikan customer yang churn: 8 * 450 USD = 3600 USD
- Total Biaya: 8700 USD + 3600 USD = **12300 USD**
- Jumlah penghematan: **37800 USD - 12300 USD = 25500 USD**

Berdasarkan perhitungan di atas, dengan menggunakan model machine learning yang telah dibuat, perusahaan bisa jauh lebih menghemat biaya yang dikeluarkan. Lebih baik mengeluarkan biaya untuk retention cost daripada lebih berpotensi untuk kehilangan customer (churn).

Setelah dibuat model machine learning untuk memprediksi customer churn, maka selanjutnya model dapat diimplementasi dalam business process di perusahaan e-commerce dengan setiap seminggu sekali. Model akan digunakan untuk melihat customer yang akan churn sehingga perusahaan dapat melakukan action kepada customer-customer yang akan churn (misal. pemberian cashback, pemberian promo discount, dll.)
