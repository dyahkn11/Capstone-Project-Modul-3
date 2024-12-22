## **Dataset: Bank Marketing Campaign** ##

## **Business Problem & Data Understanding** ##

### Business Problem ### 
Bank ingin meningkatkan efektivitas kampanye pemasaran mereka untuk menawarkan produk deposito berjangka. Untuk itu, diperlukan prediksi nasabah yang kemungkinan besar akan membuka deposito berjangka berdasarkan data historis ini.

### Objective ###
Membangun model machine learning yang dapat memprediksi kemungkinan seorang nasabah membuka deposito berjangka berdasarkan data demografis dan interaksi kampanye sebelumnya.

### Data Understanding : ###
Dataset memiliki 7.813 baris dan 11 kolom yang mencakup informasi tentang nasabah bank yang telah dikumpulkan selama kampanye pemasaran untuk mempromosikan produk deposito berjangka. Berikut penjelasan kolom yang tersedia:
![image](https://github.com/user-attachments/assets/42065c00-c2f5-41a6-81fa-ffca2f90bd29)

**Kolom Numerik Data :**
1. age: Usia nasabah 
2. balance: Saldo rata-rata tahunan.
3. campaign: Jumlah kontak yang dilakukan dalam kampanye ini.
4. pdays: Jumlah hari sejak terakhir kali nasabah dihubungi (nilai -1 berarti belum pernah dihubungi).
**Kolom Kategorikal Data :**
1. job: Jenis pekerjaan nasabah.
2. housing: Apakah nasabah memiliki pinjaman perumahan (yes atau no).
3. loan: Apakah nasabah memiliki pinjaman pribadi (yes atau no).
4. contact: Jenis kontak (e.g., telepon seluler atau tetap).
5. month: Bulan saat kampanye berlangsung.
6. poutcome: Hasil dari kampanye pemasaran sebelumnya.
7. deposit: Target variabel, apakah nasabah membuka deposito berjangka (yes atau no).

### Deskriptif Analisis : ###
![image](https://github.com/user-attachments/assets/fd1d95e1-195a-4901-b8c6-9001352ffca2)
1. **Struktur Dataset**  
   - Jumlah data: 45.211 baris dan 17 kolom.  
   - Target: `deposit` ("yes"/"no").
2. **Data Numerik**  
   - **Umur**: Rata-rata 40 tahun, terdapat outliers pada umur ekstrem (>90 tahun).  
   - **Durasi**: Rata-rata 258 detik, sangat skewed, tidak cocok digunakan untuk prediksi.  
   - **Balance**: Saldo rata-rata 1360, terdapat nilai negatif (utang) dan outliers.
3. **Data Kategorikal**  
   - **Pekerjaan**: Mayoritas "blue-collar", "management", dan "technician".  
   - **Status Pernikahan**: Mayoritas married.  
   - **Pendidikan**: Didominasi lulusan "secondary education".  
   - **Metode Kontak**: Sebagian besar melalui "cellular".
4. **Korelasi**  
   - Korelasi moderat antara `balance` dengan variabel lainnya, tetapi tidak signifikan terhadap target.
5. **Distribusi Target (`deposit`)**  
   - Tidak seimbang:  
     - **Yes**: 11.7%  
     - **No**: 88.3%  
   - Perlu penanganan ketidakseimbangan data (oversampling/undersampling).
6. **Kesimpulan**  
   - Perlu menangani outliers dan missing values.  
   - Variabel `duration` dihapus untuk menghindari kebocoran data.  
   - Ketidakseimbangan target memerlukan strategi khusus.


## **Data Cleaning, Feature Selection, and Feature Engineering** ##

### Hasil Analisis Data : ###
**1. Transformasi Data Kolom pdays:**
  - Nilai -1 pada kolom pdays diubah menjadi NaN, membantu interpretasi sebagai "tidak pernah dihubungi sebelumnya".
**2. Identifikasi Variabel:**
  - Variabel numerik: age, balance, campaign, pdays.
  - Variabel kategorikal: job, housing, loan, contact, month, poutcome, deposit.
Pemisahan ini mempermudah langkah preprocessing berikutnya.
**3. Penghapusan Outlier:**
  - Metode IQR digunakan untuk mendeteksi dan menghapus outlier pada variabel numerik.
  - Visualisasi boxplot sebelum dan sesudah menunjukkan distribusi data menjadi lebih rapi setelah penghapusan outlier.
**4. Analisis Korelasi Variabel Numerik:**
  - Korelasi antar variabel numerik diperiksa untuk menghindari multikolinearitas.
  - Tidak ada korelasi yang sangat tinggi, menunjukkan variabel numerik cukup independen.
**5. Rekayasa Fitur (Feature Engineering):**
  - One-Hot Encoding: Variabel kategorikal diubah menjadi representasi biner untuk mendukung algoritma machine learning.
  - Transformasi Target Variable: Kolom deposit diubah menjadi nilai numerik biner (1 untuk "yes", 0 untuk "no").
  - Fitur numerik dan kategorikal yang telah dienkode digabungkan menjadi dataset akhir.
**6. Kesiapan Dataset:**
  - Dataset final bersih, tanpa outlier, dan telah disiapkan dalam format yang sesuai untuk pelatihan model machine learning.
**7. Visualisasi Data:**
  - Boxplot menunjukkan perbedaan distribusi variabel numerik sebelum dan sesudah penghapusan outlier, memberikan gambaran distribusi yang lebih rapi dan representatif.
![image](https://github.com/user-attachments/assets/fed27316-b3a0-4754-ba5c-89a75f46014c)


## **Analytics: Model Training & Evaluation Metrics** ##

### Hasil Analisis : ###
**Model Performance**:
1. Akurasi yang tinggi, precision, recall, dan F1-score yang seimbang menunjukkan model memiliki performa yang baik dan dapat diandalkan.
2. Model Random Forest mampu menangani data dengan baik dan menghasilkan prediksi yang akurat.
![image](https://github.com/user-attachments/assets/fa7a6f95-31e7-4297-9427-2f7df25df325)
![image](https://github.com/user-attachments/assets/ed803360-6858-4a15-86be-3ae7a03f3017)
**Analisis Confusion Matrix:**
1. Nilai diagonal yang tinggi (TP dan TN) menunjukkan model sering membuat prediksi yang benar.
2. Jika nilai FP atau FN tinggi, itu menunjukkan area untuk perbaikan, seperti memperbaiki bias kelas atau fitur yang tidak relevan.
![image](https://github.com/user-attachments/assets/dbeda9a7-e596-4ffd-bc80-b5352f6a54b2)


## **Conclusion** ##

Berikut beberapa kesimpulan yang didapatkan dari hasil analisis yang telah dilakukan:
**1. Kinerja Model**
- Model Random Forest memberikan akurasi tinggi (~85%), menunjukkan potensi yang baik dalam memprediksi nasabah yang akan membuka deposito berjangka.
**2. Kemampuan Prediksi**
- Model berhasil mengenali pola pada data historis seperti demografi, status keuangan, dan respons terhadap kampanye sebelumnya. Hal ini mendukung identifikasi target nasabah secara efektif. 
- Hasil prediksi:
  Nilai 1 dan 0 mengindikasikan kelas prediksi:
  - 1 kemungkinan mewakili nasabah yang diprediksi akan membuka deposito berjangka.
  - 0 kemungkinan mewakili nasabah yang diprediksi tidak akan membuka deposito berjangka.
- Secara visual, terlihat lebih banyak nilai 1 dibandingkan nilai 0 pada hasil prediksi. Hal ini menunjukkan bahwa model memprediksi lebih banyak nasabah yang kemungkinan besar akan membuka deposito berjangka.


## **Recommendation** ##

**1. Fokus pada Nasabah Potensial**
- Fokuskan kampanye pemasaran pada kelompok nasabah dengan skor prediksi tinggi untuk membuka deposito berjangka.
**2. Optimalkan Strategi Pemasaran**
- Gunakan data hasil prediksi untuk menyesuaikan penawaran, seperti waktu kampanye dan pendekatan komunikasi yang lebih personal.
