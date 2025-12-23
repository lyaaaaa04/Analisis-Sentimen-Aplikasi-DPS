# Analisis Sentimen Ulasan Aplikasi DPS (Denpasar Prama Sewaka)

## Deskripsi Proyek
Proyek ini merupakan **analisis sentimen ulasan pengguna aplikasi DPS (Denpasar Prama Sewaka)** yang diambil dari **Google Play Store**.  
Tujuan utama dari proyek ini adalah untuk **mengetahui persepsi dan kepuasan pengguna** terhadap aplikasi layanan publik digital Kota Denpasar berdasarkan ulasan yang diberikan.

Dalam proyek ini, dilakukan **perbandingan performa empat algoritma machine learning**, yaitu:
- Multinomial Naive Bayes (MNB)
- Support Vector Machine (SVM)
- Logistic Regression (LR)
- XGBoost

---

## Dataset
- **Sumber Data**: Google Play Store (hasil crawling)
- **Jumlah Data**: 154 ulasan
- **Label Sentimen**:
  - Positif
  - Negatif
- **Atribut Dataset**:
  - `ulasan` : teks komentar pengguna
  - `rating` : rating bintang (1–5)
  - `sentiment` : label sentimen (positif / negatif)

### Distribusi Awal Sentimen Setelah Penghapusan Duplikat dan Null
- Positif: 84 data  
- Negatif: 64 data  

---

## Alur Implementasi
Tahapan utama yang dilakukan dalam proyek ini adalah:

1. Crawling ulasan dari Google Play Store  
2. Text cleaning (hapus simbol, URL, karakter khusus)
3. Normalisasi kata tidak baku dan slang
4. Stopword removal (Bahasa Indonesia – Sastrawi)
5. Stemming Bahasa Indonesia
6. Representasi fitur menggunakan TF-IDF
7. Penanganan data tidak seimbang dengan SMOTE
8. Training dan evaluasi model:
   - MNB
   - SVM
   - Logistic Regression
   - XGBoost
9. Visualisasi hasil (confusion matrix, wordcloud)
10. Analisis insight dari hasil klasifikasi

---

## Preprocessing Teks
Tahapan preprocessing yang diterapkan pada data ulasan meliputi:

- **Case folding** (mengubah teks ke huruf kecil)
- **Pembersihan teks** dari simbol, URL, angka berlebih
- **Normalisasi kata** 
- **Stopword removal**
- **Tokenisasi**
- **Stemming** Bahasa Indonesia

Preprocessing bertujuan untuk menghasilkan teks yang lebih bersih dan representatif sebelum dilakukan ekstraksi fitur.

---

## Ekstraksi Fitur
- Metode: **TF-IDF (Term Frequency – Inverse Document Frequency)**
- Jumlah fitur yang dihasilkan: **467 fitur kata**
- TF-IDF digunakan untuk merepresentasikan pentingnya kata dalam suatu ulasan dibandingkan keseluruhan dokumen.

---

## Penanganan Data Tidak Seimbang
Karena distribusi sentimen tidak seimbang, dilakukan **oversampling menggunakan SMOTE** sehingga diperoleh:
- Positif: 84 data
- Negatif: 84 data

Hal ini bertujuan agar model tidak bias terhadap kelas mayoritas.

---

## Model dan Performa
Empat algoritma machine learning digunakan dan dibandingkan performanya:

| Model | Akurasi |
|------|--------|
| Multinomial Naive Bayes (MNB) | **100%** |
| Support Vector Machine (SVM) | **97%** |
| Logistic Regression (LR) | **97%** |
| XGBoost | **85%** |


### Catatan Evaluasi
Meskipun beberapa model menunjukkan nilai akurasi yang sangat tinggi, hasil ini **perlu diinterpretasikan secara hati-hati** karena berpotensi mengalami **overfitting**, terutama pada kondisi berikut:

- Jumlah data relatif terbatas
- Penerapan teknik oversampling (SMOTE)
- Evaluasi masih berfokus pada metrik akurasi

Model **Multinomial Naive Bayes (MNB)** memperoleh akurasi tertinggi (100%), namun terdapat indikasi bahwa model ini **menyesuaikan diri terlalu baik terhadap data training atau disebut juga dengan overfitting**, sehingga performanya perlu diuji lebih lanjut menggunakan teknik validasi silang (cross-validation).

Model **Logistic Regression dan SVM** menunjukkan performa yang **lebih stabil dan konsisten**, sehingga dinilai lebih representatif untuk diterapkan pada data baru.

Model **XGBoost** memiliki akurasi yang lebih rendah, kemungkinan dipengaruhi oleh:
- Jumlah data yang terbatas
- Karakteristik data teks yang lebih cocok untuk model linear

---

## Evaluasi Model
Evaluasi dilakukan menggunakan:
- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix (data training dan testing)

Hasil evaluasi menunjukkan bahwa model mampu membedakan sentimen positif dan negatif dengan baik.

---

## Visualisasi Hasil
Sebagai visualisasi, digunakan WordCloud untuk memahami kata-kata dominan pada masing-masing kategori sentimen.

### Sentimen Positif
**Kata kunci utama**:
<img width="795" height="820" alt="image" src="https://github.com/user-attachments/assets/838187d1-8d2e-4c81-8490-ecaf33b217b6" />

**Insight**:
- Pengguna merasa aplikasi DPS **bermanfaat dan membantu masyarakat**.
- Kecepatan layanan dan inovasi digital menjadi poin utama kepuasan.
- Aplikasi dinilai sebagai solusi layanan publik yang relevan.

---

### Sentimen Negatif
**Kata kunci utama**:
<img width="795" height="820" alt="image" src="https://github.com/user-attachments/assets/da5168ef-5d2f-41c6-9170-507ab3d0bd4e" />

**Insight**:
- Keluhan utama berkaitan dengan **masalah teknis aplikasi**.
- Kendala sering terjadi pada proses login dan pendaftaran.
- Fitur CCTV dan kestabilan server menjadi sumber ketidakpuasan.

---

### WordCloud Umum (Semua Komentar)
**Kata dominan**:
<img width="795" height="820" alt="image" src="https://github.com/user-attachments/assets/6642cbbd-10c8-4677-926b-354a8a186ad0" />

**Insight**:
- Diskusi secara umum berfokus pada fungsi aplikasi sebagai **layanan publik digital Kota Denpasar**.
- Aplikasi dianggap penting, namun masih memerlukan peningkatan stabilitas.

---

## Kesimpulan
Berdasarkan hasil analisis sentimen terhadap ulasan aplikasi DPS, dapat disimpulkan bahwa:

1. **Mayoritas pengguna memberikan respons positif**, terutama terkait manfaat dan kemudahan layanan.
2. **Masalah teknis** seperti login, pendaftaran, dan error sistem menjadi faktor utama sentimen negatif.
3. **Multinomial Naive Bayes** terbukti sangat efektif untuk klasifikasi teks pada dataset ini.
4. Analisis sentimen dapat menjadi **alat evaluasi penting** bagi pemerintah daerah untuk meningkatkan kualitas aplikasi layanan publik.
5. Insight dari WordCloud membantu mengidentifikasi **prioritas perbaikan sistem** secara langsung dari sudut pandang pengguna.

---
