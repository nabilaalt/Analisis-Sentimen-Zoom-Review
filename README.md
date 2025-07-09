# Analisis Sentimen Zoom Review

Proyek ini bertujuan untuk membandingkan performa tiga algoritma machine learning dalam menganalisis sentimen ulasan pengguna aplikasi **Zoom Cloud Meetings** dari Google Play Store. Algoritma yang diuji meliputi **Logistic Regression**, **Support Vector Machine (SVM)**, dan **Artificial Neural Network (ANN)** berbasis TensorFlow. Untuk artikel ilmiahnya dapat diakses pada link berikut [Paper](https://docs.google.com/document/d/1ur9lMuywQiMUux1i80-0qn90jYri9N3_/edit?usp=sharing&ouid=110558818401459735760&rtpof=true&sd=true)


## Dataset

- Sumber: [Google Play Store](https://play.google.com/)
- Aplikasi: Zoom Cloud Meetings (`us.zoom.videomeetings`)
- Jumlah data awal: ±797.000 ulasan berbahasa Inggris
- Format: CSV dengan kolom `Review` dan `Rating`

## Alur Proses

1. **Scraping Data**
   - Menggunakan library `google-play-scraper`
   - Hanya mengambil review terbaru (`Sort.NEWEST`)

2. **Pra-pemrosesan Teks**
   - Pembersihan: URL, emoji, angka, simbol, stopwords
   - Normalisasi kata slang (berbasis kamus eksternal)
   - Tokenisasi dan lemmatisasi (dengan POS tagging)
   - Hasil akhir disimpan sebagai `Review_Final`

3. **Pelabelan Sentimen**
   - **Rating-based**:  
     - 1–2 → Negative  
     - 3 → Neutral  
     - 4–5 → Positive  
   - **Lexicon-based**: berdasarkan kamus kata positif/negatif  
   - **Kombinasi**: rating + skor lexicon

4. **Balancing Data**
   - Downsampling agar setiap kelas (positif, netral, negatif) seimbang: 80.055 data per kelas

5. **Modeling**
   - Logistic Regression (TF-IDF)
   - SVM LinearSVC (TF-IDF)
   - ANN (Embedding + Dense dengan TensorFlow)
   - Evaluasi: Accuracy, Precision, Recall, F1-Score, Confusion Matrix

6. **Inferensi**
   - Pengujian pada 7 teks ulasan baru untuk melihat perbedaan klasifikasi antar model

## Hasil Akurasi

| Model               | Akurasi |
|--------------------|---------|
| TensorFlow (ANN)   | 96.61%  |
| SVM (LinearSVC)    | 92.90%  |
| Logistic Regression| 91.44%  |

> Model ANN menunjukkan performa terbaik, terutama dalam menangani teks ambigu dan bernuansa netral.

