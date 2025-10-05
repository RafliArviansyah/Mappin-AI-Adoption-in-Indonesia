# Mapping AI Adoption in Indonesia

![Project Banner](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sentiment_heatmap.png?raw=true)

## Title Project
Pemetaan Penggunaan AI di Indonesia dengan IBM Granite untuk Data Classification, Summarization, dan Sentiment Analysis

## Project Overview
Proyek ini dibuat oleh Rafli sebagai bagian dari inisiatif Hactiv8 & IBMSkillsBuild untuk klasifikasi dan ringkasan data menggunakan IBM Granite. Tujuannya adalah menganalisis data publik untuk mendapatkan wawasan berharga dengan bantuan AI. Proyek ini fokus pada pemetaan penggunaan AI di Indonesia dengan menganalisis artikel berita dari sumber publik, untuk memahami sebaran AI di berbagai sektor (seperti fintech, healthtech, edutech, ecommerce, manufaktur, pemerintahan, pangan, dan lainnya), sentimen publik, serta tren waktu. Proyek ini ingin memberikan rekomendasi yang bermanfaat bagi pemerintah, industri, dan startup untuk mendukung pertumbuhan berbasis AI di Indonesia, sebagai negara berkembang.

The approach follows a structured 5-day pipeline:
1. **Data Collection**: Mengambil artikel berita dari sumber seperti Katadata, DailySocial, Kompas, dan Tempo menggunakan pustaka `newspaper3k` library, dengan `BeautifulSoup` sebagai cadangan untuk kebutuhan pengambilan data khusus.
2. **Preprocessing & Labeling**: Membersihkan teks (mengubah ke huruf kecil, menghapus karakter non-UTF8, dan stemming menggunakan Sastrawi untuk Bahasa Indonesia), serta memberi label manual pada sampel data (~61 artikel) untuk validasi.
3. **AI Inference**: Menggunakan IBM Granite 3.3-8B melalui Replicate API untuk mengklasifikasi sektor, meringkas artikel (dengan teknik chunking untuk teks panjang), dan menganalisis sentimen (menggunakan pendekatan few-shot prompting).
4. **Analysis & Visualization**: Menggabungkan data (sebaran sektor, tabel silang sentimen, tren waktu) dan membuat visualisasi (diagram batang, heatmap, diagram garis, wordcloud) menggunakan Pandas, Matplotlib, dan Seaborn.
5. **Reporting & Finalization**: enyusun wawasan, rekomendasi, dan dokumentasi (README.md dan slide presentasi).

Proyek ini dijalankan di Google Colab dengan dukungan GPU untuk mempercepat model. Dataset terdiri dari 61 artikel dari 8 sumber berbeda, dikumpulkan antara 29 April 2025 dan 1 Oktober 2025. Teknologi utama yang digunakan meliputi:
- **AI/ML**: IBM Granite 3.3-8B diakses melalui Replicate API dengan metode few-shot inference.
- **Data Processing**: Python 3.9+, Pandas, NumPy, Sastrawi (for Bahasa Indonesia stemming), NLTK (opsional untuk tokenization).
- **Data Collection**: `newspaper3k`, `requests`, `BeautifulSoup`.
- **Visualization**: Matplotlib, Seaborn, WordCloud.
- **Collaboration**: GitHub for repository management, Google Colab for notebooks.

Keterbatasan proyek ini adalah ukuran dataset yang kecil (target 500-1200 artikel, tetapi hanya 61 artikel karena keterbatasan waktu). Hal ini diatasi dengan fokus pada pengambilan data berkualitas tinggi dan validasi manual.

## Raw Dataset Link
The raw dataset is available in this GitHub repository. File: `data/raw/articles_raw.csv`  
- **Description**: Berisi 61 artikel berita mentah dengan kolom: `id`, `date`, `source`, `url`, `title`, `content`, `keywords`, `meta_description`. Total size: ~500 KB; encoded in UTF-8.
- **Direct Link**: [data/raw/articles.csv](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/data/raw/articles_raw_cleaned.csv)  
- **Data Sources**: Katadata.co.id, DailySocial.id, Tech blogs, Kompas, Tempo, etc. Search keywords: "AI Indonesia", "ChatGPT", "startup AI", "machine learning Indonesia", "IBM Granite".
- **Notes**: Dataset yang sudah diproses (dibersihkan dan diberi label) tersedia di `data/processed/articles_clean.csv` and `data/processed/labeled_sample.csv` for reference.

## Insight & Findings
Berdasarkan analisis 61 artikel menggunakan IBM Granite melalui Replicate API:
- **Sector Distribution**: Sektor "lainnya" mendominasi (~37,7%, 23 artikel), menunjukkan liputan AI yang luas tetapi kurang terfokus. Sektor lain meliputi:
  | Sector       | Percentage (%) | Article Count |
  |--------------|----------------|----------------|
  | Other        | 37.7           | 23            |
  | Ecommerce    | 6.6            | 4             |
  | Fintech      | 6.6            | 4             |
  | Healthtech   | 6.6            | 4             |
  | Edutech      | 6.6            | 4             |
  | Manufaktur   | 6.6            | 4             |
  | Government   | 6.6            | 4             |
  | Pangan       | 6.6            | 4             |
  - **Insight**: Sektor "other" yang mendominasi (37,7%) menunjukkan penggunaan AI yang luas tetapi kurang terarah. Sektor edutech sangat optimistis (100% sentimen positif), sedangkan healthtech dan pangan kurang mendapat perhatian, menunjukkan adanya celah untuk pengembangan.

- **Sentiment Analysis**: Secara keseluruhan, sentimen terbagi menjadi 44,3% positif, 34,4% netral, dan 21,3% negatif. Sentimen positif sangat tinggi di edutech (100%) dan fintech, mencerminkan optimisme terhadap AI di sektor pendidikan dan keuangan. Sentimen negatif lebih banyak muncul di artikel terkait pemerintahan, kemungkinan karena kekhawatiran tentang regulasi.
  - **Insight**: Dominasi sentimen positif (44,3%) menciptakan suasana yang mendukung adopsi AI lebih luas, tetapi nada negatif di sektor strategis menunjukkan area yang perlu diperbaiki.

- **Time Trends**: Jumlah artikel meningkat signifikan dengan laju pertumbuhan +15,0% selama periode analisis (29 April 2025 hingga 1 Oktober 2025), dengan puncaknya pada Oktober 2025.
  - **Insight**: Pertumbuhan ini menunjukkan kesadaran dan momentum AI yang meningkat, meskipun fluktuasi menandakan pelaporan yang dipicu oleh peristiwa (misalnya, konferensi atau pengumuman kebijakan).

- **Keyword Extraction**: Kata kunci teratas secara keseluruhan meliputi "foto" (243), "gemini" (106), and "jadi" (101), pointing to a focus on generative AI (e.g., image editing). Sector-specific keywords:
  - Edutech: "edukasi", "belajar", "teknologi".
  - Fintech: "fintech", "usaha", "transaksi".
  - Healthtech: "kesehatan", "teknologi", "gaza" (possible misclassification).
  - Wordcloud: Available at `assets/wordcloud_fintech.png`, `assets/wordcloud_government.png`, `assets/wordcloud_other.png`
- **Key Visualizations**:
  - Bar Chart: Sector distribution – [assets/sector_distribution.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sector_distribution.png)
  - Heatmap: Sentiment per sector – [assets/sentiment_heatmap.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sentiment_heatmap.png)
  - Line Chart: Time trends – [assets/timeline_trends.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/timeline_trends.png)

**Unique Insight**: Adopsi AI di Indonesia masih terpecah dengan kehadiran sektor "lainnya" yang kuat (37,7%), sementara edutech memimpin dalam optimisme (100% positif). Pertumbuhan +15,0% dan sentimen positif 44,3% menunjukkan prospek yang menjanjikan namun tidak merata, dengan potensi untuk pengembangan sektor yang lebih terarah.

## AI Support Explanation
AI menjadi bagian utama dalam proyek ini, menggunakan model IBM Granite 3.3-8B yang diakses melalui Replicate API (replicate.com) untuk tugas analisis yang relevan:
- **Classification (Sector Classification)**: Menggunakan teknik few-shot prompting dengan 5 contoh per label untuk mengklasifikasikan artikel ke dalam 8 kategori (fintech, healthtech, edutech, ecommerce, manufaktur, pemerintahan, lainnya, pangan). Template prompt: "Klasifikasikan teks berita berikut ke salah satu kategori (harus pilih satu): fintech, healthtech, ... Berdasarkan teks: [teks artikel]. Keluarkan hanya: sektor". Akurasi divalidasi secara manual terhadap sampel yang diberi label (~61 artikel).
- **Summarization**: Meringkas artikel panjang dengan teknik chunking (memecah teks menjadi potongan 512 token, meringkas masing-masing, lalu meringkas ringkasan tersebut). Prompt: "Ringkas teks berikut secara singkat, objektif, dan fokus pada poin utama terkait AI: [teks chunk]". Ini mengatasi batas token model dengan efektif.
- **Sentiment Analysis**: Menggunakan few-shot prompting dengan contoh positif/negatif/netral untuk mengklasifikasikan opini. Prompt: "Analisis sentimen teks berikut: positif (optimistis), negatif (kritis), atau netral (hanya fakta). Berdasarkan teks: [teks artikel]. Keluarkan hanya: sentimen".

Model dipanggil melalui Replicate API dengan token API yang disediakan, dioptimalkan untuk lingkungan GPU di Colab. Keterbatasan termasuk masalah kehabisan memori (OOM) pada tier gratis Colab, diatasi dengan menyesuaikan ukuran batch (misalnya, 15 artikel) dan mengandalkan infrastruktur cloud Replicate. Potensi bias ada karena pelatihan model yang didominasi bahasa Inggris, meskipun prompt disesuaikan untuk Bahasa Indonesia. Tidak ada fine-tuning yang dilakukan; fokus pada inferensi yang efisien. Hasil: Tingkat keberhasilan 100% pada 61 artikel, dengan output disimpan di `data/predictions/granite_predictions_complete_20251003_094126.csv`.

## How to Run the Project
1. **Konfigurasi Replicate API:**: Dapatkan token API dari [replicate.com](https://replicate.com) dan atur sebagai variabel lingkungan (`REPLICATE_API_TOKEN`) di Colab.
2. **Buka Notebook di Google Colab**: Akses notebook pengaturan utama di [notebooks/Step 1 data collection.ipynb](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%201%20-%20data%20collection.ipynb).
3. **Run Inference**: Pastikan GPU diaktifkan di Colab untuk performa optimal.
4. **Run Notebooks Sequentially**: Eksekusi sesuai urutan:
   - [Step 1 - data collection.ipynb](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%201%20-%20data%20collection.ipynb)  
   - [Step 2 - preprocessing and labelling.ipynb](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%202%20-%20preprocessing%20and%20labelling.ipynb) 
   - [Step 3 - Inference_Granite_Classification,_Summarization,_Sentiment](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%203%20-%20Inference_Granite_(Classification%2C_Summarization%2C_Sentiment).ipynb)
   - [Step 4 - Analysis_&_Visualization.ipynb](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%204%20-%20Analysis_%26_Visualization.ipynb)  
   - [Step 5 - Final_Report](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%205%20-%20Final_Report.ipynb)

## Contact
Contributions are welcome via pull requests. For questions or feedback, contact fianzah43@gmail.com or open an issue on GitHub.
