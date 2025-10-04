# Mapping AI Adoption in Indonesia

![Project Banner](([https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sector_distribution.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/4767b10b65e21f974199c76d1f0e3bcc401866f9/assets/insights_summary.png)))

## Title Project
Mapping AI Adoption in Indonesia Using IBM Granite for Data Classification, Summarization, and Sentiment Analysis

## Project Overview
This capstone project, part of the Student Development Initiative under Hactiv8, aims to analyze publicly available data to derive valuable insights using AI. The focus is on mapping AI adoption in Indonesia by analyzing news articles from public sources, addressing the lack of comprehensive understanding of AI distribution across sectors (e.g., fintech, healthtech, edutech, ecommerce, manufaktur, government, other, pangan), public sentiment, and temporal trends. The project seeks to provide actionable recommendations for stakeholders, including government bodies, industries, and startups, to foster AI-driven growth in a developing economy like Indonesia.

The approach follows a structured 5-day pipeline:
1. **Data Collection**: Scraping news articles from sources like Katadata, DailySocial, Kompas, and Tempo using the `newspaper3k` library, with `BeautifulSoup` as a fallback for custom scraping needs.
2. **Preprocessing & Labeling**: Text cleaning (lowercasing, removal of non-UTF8 characters, stemming with Sastrawi for Bahasa Indonesia), and manual labeling of a sample dataset (~61 articles) for validation.
3. **AI Inference**: Leveraging IBM Granite 3.3-8B via the Replicate API for sector classification, article summarization (using chunking for long texts), and sentiment analysis (via few-shot prompting).
4. **Analysis & Visualization**: Aggregating data (sector distribution, sentiment crosstab, time trends) and creating visualizations (bar charts, heatmaps, line charts, wordclouds) using Pandas, Matplotlib, and Seaborn.
5. **Reporting & Finalization**: Compiling insights, recommendations, and documentation (README.md, report.md, and presentation slides).

The project was executed on Google Colab with GPU support for model acceleration. The dataset comprises 61 articles from 8 unique sources, collected between April 29, 2025, and October 1, 2025. The primary tech stack includes:
- **AI/ML**: IBM Granite 3.3-8B accessed via Replicate API, utilizing few-shot inference.
- **Data Processing**: Python 3.9+, Pandas, NumPy, Sastrawi (for Bahasa Indonesia stemming), NLTK (optional for tokenization).
- **Data Collection**: `newspaper3k`, `requests`, `BeautifulSoup`.
- **Visualization**: Matplotlib, Seaborn, WordCloud.
- **Collaboration**: GitHub for repository management, Google Colab for notebooks.

Limitations include the relatively small dataset size (target 500-1200, actual 61 due to time constraints), mitigated by prioritizing quality scraping and manual validation. This project is open-source under the MIT License (see `LICENSE` file).

## Raw Dataset Link
The raw dataset is available in this GitHub repository. File: `data/raw/articles_raw.csv`  
- **Description**: Contains 61 raw news articles with columns: `id`, `date`, `source`, `url`, `title`, `content`, `keywords`, `meta_description`. Total size: ~500 KB; encoded in UTF-8.
- **Direct Link**: [data/raw/articles.csv](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/data/raw/articles_raw_cleaned.csv)  
- **Data Sources**: Katadata.co.id, DailySocial.id, Tech blogs, Kompas, Tempo, etc. Search keywords: "AI Indonesia", "ChatGPT", "startup AI", "machine learning Indonesia", "IBM Granite".
- **Notes**: Processed datasets (cleaned and labeled) are available at `data/processed/articles_clean.csv` and `data/processed/labeled_sample.csv` for reference.

## Insight & Findings
Based on the analysis of 61 articles using IBM Granite via Replicate API:
- **Sector Distribution**: The "other" sector dominates (~37.7%, 23 articles), indicating broad but unfocused AI coverage. Other sectors include:
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
  - **Insight**: The dominance of the "other" sector (37.7%) suggests a wide but unfocused adoption of AI, while sectors like edutech show high optimism (100% positive sentiment). Healthtech and pangan appear underrepresented, indicating potential gaps.

- **Sentiment Analysis**: Overall sentiment breakdown: 44.3% positive, 34.4% neutral, 21.3% negative. Positive sentiment is notably high in edutech (100%) and fintech, reflecting optimism for AI in education and financial sectors. Negative sentiment is more prevalent in government-related articles, possibly due to regulatory concerns.
  - **Insight**: The positive dominance (44.3%) creates a conducive environment for broader AI adoption, though negative tones in strategic sectors highlight areas for improvement.

- **Time Trends**: Article volume increased significantly with a growth rate of +15.0% over the analysis period (April 29, 2025, to October 1, 2025), peaking in October 2025.
  - **Insight**: This moderate growth indicates rising awareness and momentum for AI, though fluctuations suggest event-driven reporting (e.g., conferences or policy announcements).

- **Keyword Extraction**: Top overall keywords include "foto" (243), "gemini" (106), and "jadi" (101), pointing to a focus on generative AI (e.g., image editing). Sector-specific keywords:
  - Edutech: "edukasi", "belajar", "teknologi".
  - Fintech: "fintech", "usaha", "transaksi".
  - Healthtech: "kesehatan", "teknologi", "gaza" (possible misclassification).
  - Wordcloud: Available at `assets/wordcloud.png`.

- **Key Visualizations**:
  - Bar Chart: Sector distribution – [assets/sector_distribution.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sector_distribution.png)
  - Heatmap: Sentiment per sector – [assets/sentiment_per_sector.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/sentiment_heatmap.png)
  - Line Chart: Time trends – [assets/timeline_trends.png](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/assets/timeline_trends.png)

**Unique Insight**: AI adoption in Indonesia is fragmented with a strong "other" presence (37.7%), while edutech leads in optimism (100% positive). The +15.0% growth and 44.3% positive sentiment suggest a promising yet uneven landscape, with potential for strategic sector development.

## AI Support Explanation
AI is central to this project, utilizing the IBM Granite 3.3-8B model accessed via the Replicate API (replicate.com) for relevant analytical tasks:
- **Classification (Sector Classification)**: Employs few-shot prompting with 5 examples per label to classify articles into 8 categories (fintech, healthtech, edutech, ecommerce, manufaktur, government, other, pangan). Prompt template: "Classify the following news text into one category (must choose one): fintech, healthtech, ... Based on text: [article text]. Output only: sector". Accuracy was manually validated against a labeled sample (~61 articles).
- **Summarization**: Summarizes long articles using a chunking technique (dividing text into 512-token chunks, summarizing each, then summarizing the summaries). Prompt: "Summarize the following text briefly, objectively, and focus on key AI-related points: [chunk text]". This addresses the model’s token limit effectively.
- **Sentiment Analysis**: Uses few-shot prompting with positive/negative/neutral examples to classify opinions. Prompt: "Analyze the sentiment of the following text: positive (optimistic), negative (critical), or neutral (factual only). Based on text: [article text]. Output only: sentiment".

The model is invoked via the Replicate API with a provided API token, optimized for Colab’s GPU environment. Limitations include potential out-of-memory (OOM) issues on free Colab tiers, mitigated by adjusting batch sizes (e.g., 15 articles) and relying on Replicate’s cloud infrastructure. Potential bias exists due to the model’s English-dominant training, though prompts were tailored for Bahasa Indonesia. No fine-tuning was performed; the focus remained on efficient inference. Results: 100% success rate on 61 articles, with outputs stored in `data/predictions/granite_predictions_complete.csv`.

## How to Run the Project
1. **Clone Repository**: `git clone https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia.git`
2. **Open Notebook in Google Colab**: Access the main setup notebook at [notebooks/Step 1 data collection.ipynb](https://github.com/RafliArviansyah/Mapping-AI-Adoption-in-Indonesia/blob/main/Notebooks/Step%201%20-%20data%20collection.ipynb).
3. **Run Notebooks Sequentially**: Execute in order:  
   - `Step 1 - data collection.ipynb`  
   - `Step 2 - preprocessing and labelling.ipynb`  
   - `Step 3 - Inference_Granite_(Classification,_Summarization,_Sentiment)`  
   - `Step 4 - Analysis_&_Visualization.ipynb`  
   - `Step 5 - Final_Report`
4. **Configure Replicate API**: Obtain an API token from [replicate.com](https://replicate.com) and set it as an environment variable (`REPLICATE_API_TOKEN`) in Colab or a `.env` file.
5. **Run Inference**: Ensure GPU is enabled in Colab for optimal performance.

## Contact
This project was developed by Rafli as part of the Hactiv8 Student Development Initiative. Contributions are welcome via pull requests. For questions or feedback, contact fianzah43@gmail.com or open an issue on GitHub.
