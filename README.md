# Mapping AI Adoption in Indonesia

![Project Banner](https://via.placeholder.com/800x200?text=Mapping+AI+Adoption+in+Indonesia)  
*(Gambar banner placeholder; ganti dengan visualisasi aktual dari `assets/figures/sector_distribution.png` jika tersedia)*

## Title Project
Mapping AI Adoption in Indonesia Using IBM Granite for Data Classification, Summarization, and Sentiment Analysis

## Project Overview
This capstone project, part of the Student Development Initiative under Hactiv8, aims to analyze publicly available data to derive valuable insights using AI. The focus is on mapping AI adoption in Indonesia by analyzing news articles from public sources, addressing the lack of comprehensive understanding of AI distribution across sectors (e.g., fintech, healthtech, edutech, ecommerce, manufaktur, government, other), public sentiment, and temporal trends. The project seeks to provide actionable recommendations for stakeholders, including government bodies, industries, and startups, to foster AI-driven growth in a developing economy like Indonesia.

The approach follows a structured 5-day pipeline:
1. **Data Collection**: Scraping news articles from sources like Katadata, DailySocial, Kompas, and Tempo using the `newspaper3k` library, with `BeautifulSoup` as a fallback for custom scraping needs.
2. **Preprocessing & Labeling**: Text cleaning (lowercasing, removal of non-UTF8 characters, stemming with Sastrawi for Bahasa Indonesia), and manual labeling of a sample dataset (~61 articles) for validation.
3. **AI Inference**: Leveraging IBM Granite 3.3-8B via the Replicate API for sector classification, article summarization (using chunking for long texts), and sentiment analysis (via few-shot prompting).
4. **Analysis & Visualization**: Aggregating data (sector distribution, sentiment crosstab, time trends) and creating visualizations (bar charts, heatmaps, line charts, wordclouds) using Pandas, Matplotlib, and Seaborn.
5. **Reporting & Finalization**: Compiling insights, recommendations, and documentation (README.md, report.md, and presentation slides).

The project was executed on Google Colab with GPU support for model acceleration. The dataset comprises 61 articles from 8 unique sources, collected between April and October 2025. The primary tech stack includes:
- **AI/ML**: IBM Granite 3.3-8B accessed via Replicate API, utilizing few-shot inference.
- **Data Processing**: Python 3.9+, Pandas, NumPy, Sastrawi (for Bahasa Indonesia stemming), NLTK (optional for tokenization).
- **Data Collection**: `newspaper3k`, `requests`, `BeautifulSoup`.
- **Visualization**: Matplotlib, Seaborn, WordCloud.
- **Collaboration**: GitHub for repository management, Google Colab for notebooks.

Limitations include the relatively small dataset size (target 500-1200, actual 61 due to time constraints), mitigated by prioritizing quality scraping and manual validation. This project is open-source under the MIT License (see `LICENSE` file).

## Raw Dataset Link
The raw dataset is available in this GitHub repository. File: `data/raw/articles.csv`  
- **Description**: Contains 61 raw news articles with columns: `id`, `date`, `source`, `url`, `title`, `content`, `keywords`, `meta_description`. Total size: ~500 KB; encoded in UTF-8.
- **Direct Link**: [data/raw/articles.csv](https://github.com/[your-username]/mapping-ai-adoption-id/blob/main/data/raw/articles.csv)  
  (Replace `[your-username]` with your GitHub username.)
- **Data Sources**: Katadata.co.id, DailySocial.id, Tech blogs, Kompas, Tempo, etc. Search keywords: "AI Indonesia", "ChatGPT", "startup AI", "machine learning Indonesia", "IBM Granite".
- **Notes**: Processed datasets (cleaned and labeled) are available at `data/processed/articles_clean.csv` and `data/processed/labeled_sample.csv` for reference.

## Insight & Findings
Based on the analysis of 61 articles using IBM Granite via Replicate API:
- **Sector Distribution**: The "other" sector dominates (~40%, 24 articles), indicating broad but unfocused AI coverage. Other sectors include:
  | Sector       | Percentage (%) | Article Count |
  |--------------|----------------|----------------|
  | Other        | 40.0           | 24            |
  | Ecommerce    | 6.6            | 4             |
  | Fintech      | 4.9            | 3             |
  | Healthtech   | 4.9            | 3             |
  | Edutech      | 4.9            | 3             |
  | Manufaktur   | 4.9            | 3             |
  | Government   | 4.9            | 3             |
  - **Insight**: Healthtech and edutech appear under-reported, suggesting potential gaps in industry-specific AI adoption that warrant further investigation.

- **Sentiment Analysis**: Overall sentiment breakdown: 44.3% positive, 34.4% neutral, 21.3% negative. Positive sentiment is highest in fintech and ecommerce (68%), reflecting optimism for AI in SMEs and startups. The heatmap indicates higher negative sentiment in government-related articles (possibly due to regulatory issues).
  - **Insight**: Positive public sentiment supports AI adoption, but negative tones in sensitive sectors like healthtech (e.g., ethical concerns in global conflict contexts like Gaza) highlight areas for improvement.

- **Time Trends**: Article volume increased significantly (+3200% from the initial month), peaking in October 2025. This reflects growing AI momentum post-ChatGPT in Indonesia.
  - **Insight**: The upward trend suggests rising awareness, though monthly fluctuations indicate event-driven reporting (e.g., AI conferences or product launches).

- **Keyword Extraction**: Top overall keywords: "foto" (243), "gemini" (106), "jadi" (101) – indicating a focus on generative AI (e.g., image editing). Sector-specific keywords:
  - Fintech: "fintech", "usaha", "tingkat".
  - Healthtech: "gaza", "nilai", "teknologi" (possible misclassification from global news).
  - Wordcloud: Available at `assets/figures/wordcloud.png`.

- **Key Visualizations**:
  - Bar Chart: Sector distribution – [assets/figures/sector_distribution.png](https://github.com/[your-username]/mapping-ai-adoption-id/blob/main/assets/figures/sector_distribution.png)
  - Heatmap: Sentiment per sector – [assets/figures/sentiment_per_sector.png](https://github.com/[your-username]/mapping-ai-adoption-id/blob/main/assets/figures/sentiment_per_sector.png)
  - Line Chart: Time trends – [assets/figures/timeline_trends.png](https://github.com/[your-username]/mapping-ai-adoption-id/blob/main/assets/figures/timeline_trends.png)

**Unique Insight**: AI adoption in Indonesia is fragmented (dominance of "other"), with a gap between positive public sentiment and actual industry implementation. Findings are logically derived from Pandas aggregation and visualizations, though limited by the small dataset size—expansion is recommended for robustness.

## AI Support Explanation
AI is central to this project, utilizing the IBM Granite 3.3-8B model accessed via the Replicate API (replicate.com) for relevant analytical tasks:
- **Classification (Sector Classification)**: Employs few-shot prompting with 5 examples per label to classify articles into 7 categories (fintech, healthtech, edutech, ecommerce, manufaktur, government, other). Prompt template: "Classify the following news text into one category (must choose one): fintech, healthtech, ... Based on text: [article text]. Output only: sector". Accuracy was manually validated against a labeled sample (~61 articles, with a target of ~300 for ideal coverage due to time constraints).
- **Summarization**: Summarizes long articles using a chunking technique (dividing text into 512-token chunks, summarizing each, then summarizing the summaries). Prompt: "Summarize the following text briefly, objectively, and focus on key AI-related points: [chunk text]". This addresses the model’s token limit effectively.
- **Sentiment Analysis**: Uses few-shot prompting with positive/negative/neutral examples to classify opinions. Prompt: "Analyze the sentiment of the following text: positive (optimistic), negative (critical), or neutral (factual only). Based on text: [article text]. Output only: sentiment".

The model is invoked via the Replicate API with a provided API token, optimized for Colab’s GPU environment. Limitations include potential out-of-memory (OOM) issues on free Colab tiers, mitigated by adjusting batch sizes (e.g., 15 articles) and relying on Replicate’s cloud infrastructure. Potential bias exists due to the model’s English-dominant training, though prompts were tailored for Bahasa Indonesia. No fine-tuning was performed (LoRA/PEFT could enhance accuracy if time permitted); the focus remained on efficient inference. Results: 100% success rate on 61 articles, with outputs stored in `data/predictions/granite_predictions_complete.csv`.

## Cara Reproduksi Proyek
1. **Clone Repository**: `git clone https://github.com/[your-username]/mapping-ai-adoption-id.git`
2. **Open Notebook in Google Colab**: Access the main setup notebook at [notebooks/00_setup.ipynb](https://colab.research.google.com/github/[your-username]/mapping-ai-adoption-id/blob/main/notebooks/00_setup.ipynb).
3. **Run Notebooks Sequentially**: Execute in order:  
   - `Step 1 - data collection.ipynb`  
   - `Step 2 - preprocessing and labelling.ipynb`  
   - `Step 3 - Inference_Granite_(Classification,_Summarization,_Sentiment)`  
   - `Step 4 - Analysis_&_Visualization.ipynb`  
   - `Step 5 - Final_Report`
4. **Install Dependencies**: Install required libraries from `requirements.txt` using `pip install -r requirements.txt` (includes `replicate`, `sastrawi`, `matplotlib`, etc.).
5. **Configure Replicate API**: Obtain an API token from [replicate.com](https://replicate.com) and set it as an environment variable (`REPLICATE_API_TOKEN`) in Colab or a `.env` file.
6. **Run Inference**: Ensure GPU is enabled in Colab for optimal performance.


## Kontribusi & Kontak
This project was developed by Rafli as part of the Hactiv8 Student Development Initiative. Contributions are welcome via pull requests. For questions or feedback, contact fianzah43@gmail.com or open an issue on GitHub.

Last updated: October 04, 2025, 07:41 AM WIB.

