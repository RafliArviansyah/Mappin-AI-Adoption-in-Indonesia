````markdown
# Pemetaan Adopsi AI di Indonesia

![Project Banner](https://via.placeholder.com/800x200?text=Mapping+AI+Adoption+in+Indonesia)  
*(Gambar banner placeholder; ganti dengan visualisasi aktual dari `assets/figures/sector_distribution.png` jika tersedia)*

## Judul Proyek
Pemetaan Adopsi AI di Indonesia Menggunakan IBM Granite untuk Klasifikasi Data, Ringkasan, dan Analisis Sentimen

## Proyek Overview
Proyek capstone ini, bagian dari Inisiatif Pengembangan Mahasiswa di bawah Hactiv8, bertujuan untuk menganalisis data publik yang tersedia untuk mendapatkan wawasan berharga menggunakan AI. Fokusnya adalah memetakan adopsi AI di Indonesia dengan menganalisis artikel berita dari sumber publik, mengatasi kurangnya pemahaman komprehensif tentang distribusi AI di berbagai sektor (misalnya, fintech, healthtech, edutech, ecommerce, manufaktur, pemerintahan, lainnya, pangan), sentimen publik, dan tren temporal. Proyek ini bertujuan memberikan rekomendasi yang dapat ditindaklanjuti bagi pemangku kepentingan, termasuk badan pemerintahan, industri, dan startup, untuk mendorong pertumbuhan berbasis AI di ekonomi berkembang seperti Indonesia.

### Pendekatan Proyek
Proyek ini mengikuti alur kerja selama 5 hari:

1. **Pengumpulan Data**: Mengambil artikel berita dari sumber seperti Katadata, DailySocial, Kompas, dan Tempo menggunakan pustaka `newspaper3k`, dengan `BeautifulSoup` sebagai cadangan untuk kebutuhan scraping khusus.
2. **Pra-pemrosesan & Pelabelan**: Pembersihan teks (konversi ke huruf kecil, penghapusan karakter non-UTF8, stemming dengan `Sastrawi` untuk Bahasa Indonesia), dan pelabelan manual pada sampel dataset (~61 artikel) untuk validasi.
3. **Inferensi AI**: Memanfaatkan IBM Granite 3.3-8B melalui Replicate API untuk klasifikasi sektor, ringkasan artikel (menggunakan teknik chunking untuk teks panjang), dan analisis sentimen (melalui pendekatan few-shot prompting).
4. **Analisis & Visualisasi**: Mengagregasi data (distribusi sektor, crosstab sentimen, tren waktu) dan membuat visualisasi (diagram batang, heatmap, diagram garis, wordcloud) menggunakan Pandas, Matplotlib, dan Seaborn.
5. **Pelaporan & Finalisasi**: Menyusun wawasan, rekomendasi, dan dokumentasi (README.md, report.md, dan slide presentasi).

Proyek ini dijalankan di Google Colab dengan dukungan GPU untuk akselerasi model. Dataset terdiri dari 61 artikel dari 8 sumber unik, dikumpulkan antara 29 April 2025 dan 1 Oktober 2025.

### Teknologi yang Digunakan
- **AI/ML**: IBM Granite 3.3-8B diakses melalui Replicate API, menggunakan inferensi few-shot.
- **Pemrosesan Data**: Python 3.9+, Pandas, NumPy, Sastrawi (untuk stemming Bahasa Indonesia), NLTK (opsional untuk tokenisasi).
- **Pengumpulan Data**: newspaper3k, requests, BeautifulSoup.
- **Visualisasi**: Matplotlib, Seaborn, WordCloud.
- **Kolaborasi**: GitHub untuk manajemen repositori, Google Colab untuk notebook.

### Keterbatasan
Dataset yang digunakan relatif kecil (61 artikel) karena keterbatasan waktu. Namun, kualitas scraping dan validasi manual diprioritaskan.

## Tautan Dataset Mentah
Dataset mentah tersedia di repositori GitHub ini. File: `data/raw/articles.csv`

- **Deskripsi**: Berisi 61 artikel berita mentah dengan kolom: id, date, source, url, title, content, keywords, meta_description.
- **Ukuran**: ~500 KB; dikodekan dalam UTF-8.
- **Sumber Data**: Katadata.co.id, DailySocial.id, blog teknologi, Kompas, Tempo, dll.
- **Catatan**: Dataset yang telah diproses tersedia di `data/processed/articles_clean.csv` dan `data/processed/labeled_sample.csv` untuk referensi.

## Wawasan & Temuan
### Distribusi Sektor
Sektor "lainnya" mendominasi (~37,7%, 23 artikel), menunjukkan cakupan AI yang luas namun tidak terfokus. Sektor lain meliputi:

| Sektor       | Persentase (%) | Jumlah Artikel |
|--------------|----------------|----------------|
| Lainnya      | 37,7           | 23             |
| Ecommerce    | 6,6            | 4              |
| Fintech      | 6,6            | 4              |
| Healthtech   | 6,6            | 4              |
| Edutech      | 6,6            | 4              |
| Manufaktur   | 6,6            | 4              |
| Pemerintahan | 6,6            | 4              |
| Pangan       | 6,6            | 4              |

### Analisis Sentimen
Rincian sentimen keseluruhan: 44,3% positif, 34,4% netral, 21,3% negatif.

### Tren Waktu
Volume artikel meningkat dengan laju pertumbuhan +15,0% selama periode analisis (29 April 2025 hingga 1 Oktober 2025).

### Ekstraksi Kata Kunci
Kata kunci utama termasuk "foto" (243), "gemini" (106), dan "jadi" (101), dengan fokus pada AI generatif.

## Visualisasi Utama
- **Diagram Batang**: Distribusi sektor – `assets/figures/sector_distribution.png`
- **Heatmap**: Sentimen per sektor – `assets/figures/sentiment_per_sector.png`
- **Diagram Garis**: Tren waktu – `assets/figures/timeline_trends.png`

## Penjelasan Dukungan AI
AI menjadi inti proyek ini, menggunakan model IBM Granite 3.3-8B yang diakses melalui Replicate API untuk tugas analitis yang relevan:

1. **Klasifikasi**: Menggunakan pendekatan few-shot prompting untuk mengklasifikasikan artikel ke dalam 8 kategori (fintech, healthtech, edutech, ecommerce, manufaktur, pemerintahan, lainnya, pangan).
2. **Ringkasan**: Merangkum artikel panjang dengan teknik chunking untuk mengatasi batas token model.
3. **Analisis Sentimen**: Mengklasifikasikan opini ke dalam kategori positif, negatif, atau netral menggunakan pendekatan few-shot.

Model dipanggil melalui Replicate API dengan token API yang disediakan, dioptimalkan untuk lingkungan GPU Colab.

## Cara Mereproduksi Proyek
1. **Kloning Repositori**: 
   ```bash
   git clone https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia.git
````

2. **Buka Notebook di Google Colab**:
   Akses notebook pengaturan utama di `notebooks/Step 1 data collection.ipynb`.

3. **Jalankan Notebook Secara Berurutan**: Eksekusi sesuai urutan:

   * Step 1 - data collection.ipynb
   * Step 2 - preprocessing and labelling.ipynb
   * Step 3 - Inference_Granite_(Classification,_Summarization,_Sentiment)
   * Step 4 - Analysis_&_Visualization.ipynb
   * Step 5 - Final_Report

4. **Instal Dependensi**:
   Instal pustaka yang diperlukan dari `requirements.txt`:

   ```bash
   pip install -r requirements.txt
   ```

5. **Konfigurasi Replicate API**:
   Dapatkan token API dari replicate.com dan atur sebagai variabel lingkungan (`REPLICATE_API_TOKEN`) di Colab atau file `.env`.

6. **Jalankan Inferensi**:
   Pastikan GPU diaktifkan di Colab untuk performa optimal.

## Kontribusi & Kontak

Proyek ini dikembangkan oleh Rafli sebagai bagian dari Inisiatif Pengembangan Mahasiswa Hactiv8. Kontribusi diterima melalui pull request. Untuk pertanyaan atau umpan balik, hubungi [fianzah43@gmail.com](mailto:fianzah43@gmail.com) atau buka isu di GitHub.
