# Week 3: Data Preprocessing & Sentiment Analysis

## Ringkasan

Week ini mencakup dua tugas utama:

1. **Tugas 1:** Re-run pipeline preprocessing (referensi: Week2-Scrapping Apps Review MobileJKN) dengan dataset GoPay reviews, beserta analisa sederhana.
2. **Tugas 2:** Menambahkan kata-kata dari most frequent words yang tidak memiliki arti penting ke list Indonesian stopwords.

Kedua tugas ini dikerjakan dalam notebook Preprocessing (NB 3), yang merupakan versi jauh lebih lengkap dari referensi MobileJKN. Selain itu, terdapat notebook Sentiment Analysis (NB 6) yang menambahkan skor sentimen menggunakan TextBlob sebagai persiapan data untuk tahap selanjutnya.

## Notebook

### 3. Preprocessing (`Gopay_Review_Preprocessing_v3.ipynb`)

Pipeline preprocessing 16 langkah yang mengubah data review mentah menjadi dataset bersih siap analisis.

| Step | Task | Tool |
|------|------|------|
| 1 | Drop unnecessary columns | pandas |
| 2 | Handle missing & empty values | pandas |
| 3 | Remove duplicates | pandas |
| 4 | Sentiment labeling | Rule-based (score 1-2 = negative, 3 = neutral, 4-5 = positive) |
| 5 | Case folding | `.str.lower()` |
| 6 | Slang normalization | **kamus-alay** (5,700 entry Indonesian slang corpus) |
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

#### Tugas 1: Re-run Preprocessing

Notebook ini mencakup seluruh pipeline yang ada di referensi MobileJKN (load data, stopwords list, hapus stopwords, hitung frequent words, visualisasi), ditambah 12 langkah preprocessing lainnya yang lebih komprehensif.

#### Tugas 2: Menambahkan Kata ke Stopwords

Dilakukan di **Section 13.1 (Feedback Loop: Tambah Noise Words ke Stopwords)**. Setelah menganalisis TOP 100 kata paling sering, kata-kata berikut yang tidak membawa sinyal sentimen ditambahkan ke stopword list:

- Singkatan dan simbol: `rp`, `tf`, `wdp`, `cs`, `min`
- Varian kata yang sudah dicakup: `terimakasih`, `aplikasinya`, `gue`, `gua`, `ku`, `hp`
- Filler dan partikel: `pokoknya`, `mulu`, `oke`
- Kata konteks netral: `apk`, `up`, `kali`, `bintang`

Total 19 noise words ditambahkan secara data-driven berdasarkan hasil analisis frekuensi.

Pendekatan stopword removal menggunakan 3 layer:
- **Layer 1:** NLTK Indonesian (758 kata baku)
- **Layer 2:** Sastrawi (stemmer-based stopwords)
- **Layer 3:** Domain-specific untuk GoPay (`gopay`, `gojek`, `aplikasi`, `app`, `nya`, `sih`, `deh`, `loh`, `nih`, `lah`, `kok`, `yah`, `wah`, `tuh`, `gitu`, `gini`, dll.)

### 6. Sentiment Analysis (`6-Gopay-Review-Sentiment-Analysis.ipynb`)

Notebook pendukung yang menambahkan skor sentimen pada dataset hasil preprocessing menggunakan TextBlob.

Langkah-langkah:
- Load `gopay_reviews_cleandata.csv`
- Hitung `sentiment_polarity` dan `sentiment_subjectivity` via TextBlob
- EDA sentimen: scatter plot polarity vs subjectivity, word cloud (all/positive/negative), review count per tahun, distribusi rating, sentiment trend over time
- Simpan sebagai `gopay_reviews_sentiment.csv`

**Input:** `gopay_reviews_cleandata.csv` (209,311 rows x 8 kolom)
**Output:** `gopay_reviews_sentiment.csv` (209,311 rows x 11 kolom, ditambah polarity, subjectivity, year)

## Images

Visualisasi yang dihasilkan dari notebook di week ini:

### Preprocessing (NB 3)

1. **Top 30 Most Frequent Words (setelah stopword removal)**
   Menampilkan 30 kata yang paling sering muncul setelah stopwords dihapus. Digunakan untuk mengidentifikasi noise words yang perlu ditambahkan ke stopword list (feedback loop). Kata-kata seperti "gopay", "aplikasi" yang terlalu umum dan tidak informatif teridentifikasi di sini.

2. **Final Word Count Distribution**
   Dua panel: histogram distribusi jumlah kata per review setelah preprocessing selesai, dan boxplot sebagai ringkasan statistik. Menunjukkan bahwa mayoritas review memiliki 1-10 kata setelah dibersihkan.

### Sentiment Analysis (NB 6)

3. **Scatter Plot: Polarity vs Subjectivity**
   Menampilkan hubungan antara polarity (positif/negatif) dan subjectivity (objektif/subjektif) dari TextBlob. Titik-titik diwarnai berdasarkan label sentimen (positive/neutral/negative).

4. **Word Cloud (All Reviews)**
   Visualisasi kata-kata paling dominan di seluruh review dalam bentuk word cloud.

5. **Word Cloud (Positive vs Negative)**
   Dua word cloud berdampingan: satu untuk review positif dan satu untuk review negatif. Menunjukkan perbedaan kosakata antara pengguna yang puas vs tidak puas.

6. **Review Count by Year**
   Bar chart jumlah review per tahun, menunjukkan tren pertumbuhan jumlah review GoPay dari waktu ke waktu.

7. **Distribution of Ratings**
   Distribusi rating 1-5 dari seluruh review GoPay.

8. **Sentiment Trend Over Time**
   Tren jumlah review positif, netral, dan negatif per tahun, menunjukkan bagaimana sentimen pengguna berubah seiring waktu.

## Dataset

| File | Deskripsi | Baris | Kolom |
|------|-----------|-------|-------|
| `gopay_reviews_raw.csv` | Input: data mentah dari scraping | 367,195 | 11 |
| `gopay_reviews_cleandata.csv` | Output NB 3: data setelah preprocessing | 209,311 | 8 |
| `gopay_reviews_sentiment.csv` | Output NB 6: data dengan skor sentimen | 209,311 | 11 |

## Tools & Library

- `Sastrawi` -- stemmer Bahasa Indonesia (ECS algorithm)
- `nlp-id` -- lemmatizer Bahasa Indonesia (Kumparan)
- `autocorrect` -- spelling correction (statistical model)
- `kamus-alay` -- slang normalization corpus (5,700 entries)
- `NLTK` -- tokenization, stopwords
- `TextBlob` -- sentiment scoring (polarity, subjectivity)
- `emoji` -- emoji removal
- `pandas`, `numpy` -- manipulasi data
- `matplotlib`, `seaborn`, `wordcloud` -- visualisasi

## Referensi

- Week2-Scrapping Apps Review MobileJKN (referensi colab dari dosen)
- Salsabila et al. (2018) -- kamus-alay Indonesian slang corpus