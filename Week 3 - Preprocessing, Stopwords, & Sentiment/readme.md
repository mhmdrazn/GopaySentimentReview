# Week 3: Preprocessing, Stopwords Analysis & Sentiment Analysis

## Ringkasan

Week ini mencakup tiga tugas:

1. **Tugas 1:** Re-run pipeline preprocessing (referensi: Week2-Scrapping Apps Review MobileJKN) dengan dataset GoPay reviews, beserta analisa sederhana.
2. **Tugas 2:** Menambahkan kata-kata dari most frequent words yang tidak memiliki arti penting ke list Indonesian stopwords.
3. **Tambahan:** Sentiment scoring menggunakan TextBlob sebagai persiapan data untuk Week 4.

## Notebook

### 3. Preprocessing (`3-Gopay-Review-Preprocessing.ipynb`)

Pipeline preprocessing 16 langkah yang mengubah data review mentah menjadi dataset bersih siap analisis. Notebook ini mencakup Tugas 1 (re-run pipeline preprocessing) dengan cakupan yang jauh lebih komprehensif dari referensi MobileJKN.

| Step | Task | Tool |
|------|------|------|
| 1 | Drop unnecessary columns | pandas |
| 2 | Handle missing & empty values | pandas |
| 3 | Remove duplicates | pandas |
| 4 | Sentiment labeling | Rule-based (score 1-2 = negative, 3 = neutral, 4-5 = positive) |
| 5 | Case folding | `.str.lower()` |
| 6 | Slang normalization | **kamus-alay** (5,700 entry Indonesian slang corpus, Salsabila et al. 2018) |
| 7 | Text cleaning | `re`, `emoji` (hapus URL, emoji, tanda baca, angka) |
| 8 | Spelling correction | `autocorrect` (statistical model untuk Bahasa Indonesia) |
| 9 | Tokenization | NLTK `word_tokenize` |
| 10 | Stopword removal | 3-layer: NLTK Indonesian (758 kata) + Sastrawi + domain custom |
| 11 | Frequent words analysis | `Counter` (TOP 50/100/1000) |
| 12 | Lemmatization | `nlp-id` (Kumparan) |
| 13 | Stemming | PySastrawi (ECS algorithm) |
| 14 | Rare words removal | Corpus frequency threshold (freq <= 2) |
| 15 | Common words removal | Document frequency threshold (doc freq > 50%) |
| 16 | Reconstruct text & save | pandas |

**Input:** `gopay_reviews_raw.csv` (367,195 rows)  
**Output:** `gopay_reviews_cleandata.csv` (209,311 rows x 8 kolom)

### 3b. Stopwords Analysis (`3b-Gopay-Review-Stopwords-Analysis.ipynb`)

Notebook terpisah yang mendokumentasikan proses analisis dan penambahan stopwords secara mendalam. Menjawab **Tugas 2** secara eksplisit.

Langkah-langkah:
- Eksplorasi default Indonesian stopwords dari NLTK (758 kata) dan Sastrawi, termasuk analisis overlap antara keduanya
- Analisis TOP 50 kata sebelum stopword removal, dengan penandaan mana yang sudah tercakup dan mana yang belum
- Implementasi 3-layer stopword removal (NLTK + Sastrawi + domain custom)
- Frequent words analysis sesudah stopword removal (TOP 100)
- Identifikasi 19 noise words dari frequent words yang tidak membawa sinyal sentimen
- Penambahan noise words ke stopword list
- Evaluasi perbandingan sebelum vs sesudah penambahan

Kata-kata noise yang ditambahkan:
- Singkatan dan simbol: `rp`, `tf`, `wdp`, `cs`, `min`
- Varian kata: `terimakasih`, `aplikasinya`, `gue`, `gua`, `ku`, `hp`
- Filler dan partikel: `pokoknya`, `mulu`, `oke`
- Kata konteks netral: `apk`, `up`, `kali`, `bintang`

Pendekatan stopword 3+1 layer:
- **Layer 1:** NLTK Indonesian (758 kata baku)
- **Layer 2:** Sastrawi (stemmer-based stopwords)
- **Layer 3:** Domain custom (`gopay`, `gojek`, `aplikasi`, `app`, `nya`, `sih`, `deh`, `loh`, `nih`, `lah`, `kok`, `yah`, `wah`, `tuh`, `gitu`, `gini`)
- **Layer 4:** Noise words dari frequent words analysis (19 kata, data-driven)

### 6. Sentiment Analysis (`6-Gopay-Review-Sentiment-Analysis.ipynb`)

Menambahkan skor sentimen pada dataset hasil preprocessing menggunakan TextBlob. Output notebook ini menjadi input untuk Week 4 (BoW dan TF-IDF).

Langkah-langkah:
- Load `gopay_reviews_cleandata.csv`
- Hitung `sentiment_polarity` dan `sentiment_subjectivity` via TextBlob
- EDA sentimen: scatter plot, word cloud, review count per tahun, distribusi rating, sentiment trend
- Simpan sebagai `gopay_reviews_sentiment.csv`

**Input:** `gopay_reviews_cleandata.csv` (209,311 rows x 8 kolom)  
**Output:** `gopay_reviews_sentiment.csv` (209,311 rows x 11 kolom)

## Images

### Distribution-Final-Length-and-Top-20-Words-Final.png
![Distribution Final Length and Top 20 Words Final](Week 3 - Preprocessing/Images/Distribution-Final-Length-and-Top-20-Words-Final.png)
Dua panel dari output akhir preprocessing. Kiri: distribusi panjang review setelah cleaning. Kanan: 20 kata paling sering yang sudah lebih bermakna.
---

### Top-30-Most-Frequent-Words.png
![Top 30 Most Frequent Words](Week 3 - Preprocessing/Images/Top-30-Most-Frequent-Words.png)
30 kata paling sering sebelum stopword removal, masih didominasi kata fungsi.
---

### Top-30-Words-Before-Stopwords-Removal.png
![Top 30 Words Before Stopwords Removal](Week 3 - Preprocessing/Images/Top-30-Words-Before-Stopwords-Removal.png)
Visualisasi sebelum stopwords dihapus, menunjukkan gap pada stopword list default.
---

### Top-30-Words-After-Stopwords-Removal.png
![Top 30 Words After Stopwords Removal](Week 3 - Preprocessing/Images/Top-30-Words-After-Stopwords-Removal.png)
Kata-kata paling sering setelah stopword removal, lebih relevan untuk analisis.
---

### Perbandingan-Stopwords-List-NLTK-vs-Sastrawi.png
![Perbandingan Stopwords List NLTK vs Sastrawi](Week 3 - Preprocessing/Images/Perbandingan-Stopwords-List-NLTK-vs-Sastrawi.png)
Perbandingan cakupan stopwords antara NLTK dan Sastrawi.
---

### Sentiment-Analysis-Polarity-vs-Subjectivity.png
![Sentiment Analysis Polarity vs Subjectivity](Week 3 - Preprocessing/Images/Sentiment-Analysis-Polarity-vs-Subjectivity.png)
Scatter plot polarity vs subjectivity dari TextBlob.
---

### Distribution-Ratings.png
![Distribution Ratings](Week 3 - Preprocessing/Images/Distribution-Ratings.png)
Distribusi rating setelah preprocessing.
---

### Number-of-Reviews-by-Year.png
![Number of Reviews by Year](Week 3 - Preprocessing/Images/Number-of-Reviews-by-Year.png)
Jumlah review per tahun.
---

### Sentiment-Distribution-Overtime.png
![Sentiment Distribution Overtime](Week 3 - Preprocessing/Images/Sentiment-Distribution-Overtime.png)
Tren sentimen dari waktu ke waktu.
---

### Word-Cloud-Positive-Sentiment.png
![Word Cloud Positive Sentiment](Week 3 - Preprocessing/Images/Word-Cloud-Positive-Sentiment.png)
Word cloud keseluruhan dataset.
---

### Word-Cloud-Sentiment-Positive-and-Negative.png
![Word Cloud Sentiment Positive and Negative](Week 3 - Preprocessing/Images/Word-Cloud-Sentiment-Positive-and-Negative.png)
Perbandingan word cloud positif vs negatif.

## Dataset

| File | Deskripsi | Baris | Kolom |
|------|-----------|-------|-------|
| `gopay_reviews_raw.csv` | Input: data mentah dari scraping | 367,195 | 11 |
| `gopay_reviews_cleandata.csv` | Output NB 3: data setelah preprocessing | 209,311 | 8 |
| `gopay_reviews_sentiment.csv` | Output NB 6: data dengan skor sentimen | 209,311 | 11 |

## Tools & Library

- `Sastrawi` - stemmer Bahasa Indonesia (ECS algorithm)
- `nlp-id` - lemmatizer Bahasa Indonesia (Kumparan)
- `autocorrect` - spelling correction (statistical model)
- `kamus-alay` - slang normalization corpus (5,700 entries)
- `NLTK` - tokenization, stopwords
- `TextBlob` - sentiment scoring (polarity, subjectivity)
- `emoji` - emoji removal
- `pandas`, `numpy` - manipulasi data
- `matplotlib`, `seaborn`, `wordcloud` - visualisasi

## Referensi

- Week2-Scrapping Apps Review MobileJKN (referensi colab dari dosen)
- Salsabila et al. (2018) - kamus-alay Indonesian slang corpus
