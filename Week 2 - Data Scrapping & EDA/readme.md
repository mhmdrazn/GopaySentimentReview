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
- **Data Overview & Quality Check:** cek missing values, tipe data, duplikat
- **Score Distribution:** distribusi rating 1-5 (bar chart + pie chart)
- **Temporal Analysis:** volume review per bulan, tren rata-rata skor, komposisi skor dari waktu ke waktu (stacked area chart)
- **Text Analysis:** distribusi panjang review per skor, kata-kata paling sering muncul (raw), perbandingan kata umum antara review positif vs negatif
- **App Version Analysis:** jumlah review dan rata-rata skor per versi aplikasi

## Dataset

| File | Deskripsi | Baris | Kolom |
|------|-----------|-------|-------|
| `gopay_reviews_raw.csv` | Hasil scraping mentah dari Google Play | 367,195 | 11 |

## Tools & Library

- `google-play-scraper` -- scraping review dari Google Play Store
- `pandas`, `numpy` -- manipulasi data
- `matplotlib`, `seaborn` -- visualisasi
- `collections.Counter` -- analisis frekuensi kata

## Catatan

- Dataset yang di-scrape mencakup review dari berbagai tahun hingga Februari 2026
- Data mentah ini akan menjadi input untuk notebook preprocessing di Week 3
- Beberapa kolom seperti `replyContent` memiliki banyak missing values karena tidak semua review dibalas oleh developer