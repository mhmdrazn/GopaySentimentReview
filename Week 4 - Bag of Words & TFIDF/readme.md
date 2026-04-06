# Week 4: Bag of Words, TF-IDF & Klasifikasi Sentimen

## Ringkasan

Week ini mencakup feature extraction dan klasifikasi sentimen:

- **Bag of Words (BoW):** mengubah teks menjadi matriks angka mentah (frekuensi kata), termasuk analisis regex untuk insights positive/negative
- **TF-IDF + Classifier:** menerapkan bobot TF-IDF di atas BoW, kemudian melatih 13 kombinasi model klasifikasi sentimen
- **Tugas 1A, 1B, 1C:** memahami TF-IDF secara mendalam melalui perhitungan manual dan perbandingan dengan scikit-learn

---

## Notebook

### 4. Bag of Words (`4-Gopay-Review-BoW.ipynb`)

Mengubah teks review yang sudah dipreprocessing menjadi representasi numerik menggunakan CountVectorizer.

Langkah-langkah:
- Load `gopay_reviews_sentiment.csv`
- Eksplorasi teks bersih (word count distribution, sample review)
- Build BoW model: `CountVectorizer(max_features=5000, min_df=2, max_df=0.95)`
- Inspeksi vocabulary dan term frequency
- Visualisasi top terms (keseluruhan dan per sentimen)
- Analisis regex
- Export matriks BoW dan vocabulary

---

### 5. TF-IDF + Classifier (`5-Gopay-Review-TFIDF.ipynb`)

Feature extraction dan klasifikasi sentimen menggunakan berbagai model.

Pipeline:
1. Load dataset dan subsampling
2. BoW (CountVectorizer)
3. TF-IDF (TfidfTransformer)
4. Training classifier
5. Evaluasi performa model

---

## Tugas

### Tugas 1A (`Tugas-1A-TFIDF-Danantara.ipynb`)

Memahami TF-IDF secara mendalam dengan menghitung TF, IDF, dan TF-IDF secara manual (tanpa library) pada corpus bertema Danantara/investasi Indonesia.

Langkah-langkah:
- Menyiapkan kumpulan kalimat (sentence-level corpus)
- Preprocessing teks (case folding, cleaning)
- Menghitung **Term Frequency (TF)** secara manual
- Menghitung **Inverse Document Frequency (IDF)** secara manual
- Menghitung **TF-IDF**
- Membandingkan hasil dengan `scikit-learn`

---

### Tugas 1B (`Tugas-1B-TFIDF-Sentence-Manchester.ipynb`)

Memahami TF-IDF secara mendalam dengan menghitung TF, IDF, dan TF-IDF secara manual (tanpa library) pada corpus bertema Manchester.

Langkah-langkah:
- Menyiapkan kumpulan kalimat (sentence-level corpus)
- Preprocessing teks (case folding, cleaning)
- Menghitung **Term Frequency (TF)** secara manual
- Menghitung **Inverse Document Frequency (IDF)** secara manual
- Menghitung **TF-IDF**
- Membandingkan hasil dengan `scikit-learn`

---

### Tugas 1C (`Tugas-1C-TFIDF-Artikel-News.ipynb`)

Memahami TF-IDF secara mendalam dengan menghitung TF, IDF, dan TF-IDF secara manual (tanpa library) pada corpus artikel berita.

Langkah-langkah:
- Menyiapkan kumpulan kalimat dari artikel (sentence-level corpus)
- Preprocessing teks (case folding, cleaning)
- Menghitung **Term Frequency (TF)** secara manual
- Menghitung **Inverse Document Frequency (IDF)** secara manual
- Menghitung **TF-IDF**
- Membandingkan hasil dengan `scikit-learn`

Sumber:  
[BBC Indonesia - China peringatkan negara yang buat kesepakatan dengan AS](https://www.bbc.com/indonesia/articles/c1wdzeyr9wyo)

---

## Tools & Library

- `scikit-learn`
- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `scipy`
- `TensorFlow Hub`

---

## Temuan Utama

1. TF-IDF efektif untuk representasi teks berbasis frekuensi dan pentingnya kata.
2. Perhitungan manual membantu memahami cara kerja TF-IDF secara fundamental.
3. Kata yang sering muncul di semua dokumen memiliki bobot lebih rendah dibanding kata spesifik.
4. TF-IDF cocok untuk data teks berdimensi tinggi dan sparse.