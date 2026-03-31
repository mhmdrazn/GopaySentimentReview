# Week 2: Data Scraping & Exploratory Data Analysis

## Ringkasan

Week ini mencakup proses pengumpulan data review GoPay dari Google Play Store dan analisis eksploratif awal untuk memahami karakteristik dataset sebelum masuk ke tahap preprocessing.

## Notebook

### 1. Scraping (`1-Gopay-Review-Scraping.ipynb`)

Mengumpulkan seluruh review GoPay dari Google Play Store menggunakan library `google-play-scraper`.

- **App ID:** `com.gojek.gopay`
- **Bahasa:** Indonesia (`lang='id'`)
- **Sorting:** Terbaru (`Sort.NEWEST`)
- **Hasil:** 367,195 review dengan 11 kolom (reviewId, userName, content, score, thumbsUpCount, reviewCreatedVersion, at, replyContent, repliedAt, appVersion, dll.)
- **Output:** `gopay_reviews_raw.csv`

### 2. EDA (`2-Gopay-Review-EDA.ipynb`)

Analisis eksploratif untuk memahami pola dan distribusi data sebelum preprocessing.

Analisis yang dilakukan:
- Data overview dan quality check (missing values, tipe data, duplikat)
- Distribusi skor/rating
- Analisis temporal (tren review per bulan/tahun)
- Analisis teks (panjang review, kata paling sering)
- Analisis per versi aplikasi

## Images

### Distribution-of-Reviews-Scores.png
![Distribution of Reviews Scores](Week 2 - Data Scrapping & EDA/Images/Distribution-of-Reviews-Scores.png)
Distribusi rating 1-5 dari seluruh review GoPay. Menunjukkan proporsi review per skor, mengindikasikan apakah dataset cenderung positif, negatif, atau seimbang. Umumnya review aplikasi memiliki distribusi U-shape (banyak di skor 1 dan 5).
---

### Monthly-Review-Volume-and-Average-Score-Over-Time.png
![Monthly Review Volume and Average Score Over Time](Week 2 - Data Scrapping & EDA/Images/Monthly-Review-Volume-and-Average-Score-Over-Time.png)
Dua panel: volume review per bulan (bar chart) dan rata-rata skor per bulan (line chart). Menunjukkan tren pertumbuhan jumlah review dan fluktuasi kepuasan pengguna dari waktu ke waktu.
---

### Score-Composition-Over-Time.png
![Score Composition Over Time](Week 2 - Data Scrapping & EDA/Images/Score-Composition-Over-Time.png)
Stacked area chart yang menampilkan komposisi skor 1-5 dari waktu ke waktu.
---

### Most-Frequent-Words-Raw.png
![Most Frequent Words Raw](Week 2 - Data Scrapping & EDA/Images/Most-Frequent-Words-Raw.png)
Bar chart kata-kata paling sering muncul di review mentah (sebelum preprocessing).
---

### Top-15-Words-by-Sentiment-Group-Raw.png
![Top 15 Words by Sentiment Group Raw](Week 2 - Data Scrapping & EDA/Images/Top-15-Words-by-Sentiment-Group-Raw.png)
Perbandingan 15 kata paling sering antara review positif vs negatif.
---

### Word-Count-Distribution-by-Score-and-Review-Length-Distribution.png
![Word Count Distribution by Score and Review Length Distribution](Week 2 - Data Scrapping & EDA/Images/Word-Count-Distribution-by-Score-and-Review-Length-Distribution.png)
Distribusi panjang review per skor rating.
---

### Average-Score-per-Top-App-Version.png
![Average Score per Top App Version](Week 2 - Data Scrapping & EDA/Images/Average-Score-per-Top-App-Version.png)
Rata-rata skor review per versi aplikasi.
---

### Top-20-App-Versions-by-Review-Count.png
![Top 20 App Versions by Review Count](Week 2 - Data Scrapping & EDA/Images/Top-20-App-Versions-by-Review-Count.png)
Versi aplikasi dengan jumlah review terbanyak.

## Dataset

| File | Deskripsi | Baris | Kolom |
|------|-----------|-------|-------|
| `gopay_reviews_raw.csv` | Hasil scraping mentah dari Google Play | 367,195 | 11 |

## Tools & Library

- `google-play-scraper` - scraping review dari Google Play Store
- `pandas`, `numpy` - manipulasi data
- `matplotlib`, `seaborn` - visualisasi
- `collections.Counter` - analisis frekuensi kata
