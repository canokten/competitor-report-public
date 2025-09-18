https://opendata.vancouver.ca/explore/dataset/local-area-boundary/export/?disjunctive.name - Geomap for Vancouver

# Competitor Analysis SaaS Prototype

*A data engineering + analytics project built on Databricks with Google Maps data integration*

---

## 📌 Overview
This project is a **Competitor Analysis SaaS prototype** designed to help local businesses understand their competitive landscape.  
The demo case focuses on **hair salons in Vancouver**, but the system is **sector-agnostic** (extendable to restaurants, tattoo shops, bars, etc.).

The solution combines **data extraction, ETL pipelines, analytics modeling, and interactive dashboards**, all embedded into a shareable **HTML report** for end users.

---

## 🛠️ Tools & Technologies
- **Data Extraction**: [Apify](https://apify.com/) (Google Maps scraper),  [Google Maps API](https://developers.google.com/maps/documentation/places/web-service/overview)
- **Data Engineering**: [Databricks](https://www.databricks.com/)  
  - Delta Lake  
  - SQL Warehouses  
  - Python Notebooks  
  - Medallion Architecture (Bronze → Silver → Gold)
- **Analytics & Modeling**:
  - Custom KPIs (`rating_score = rating × log(reviews)`)
  - LLM-based sentiment analysis (praise/complaint categories)
- **Visualization**: Databricks **Lakeview Dashboards**
- **Reporting**: Custom **HTML embedding** of dashboards
- **Other Skills**: ETL, JSON handling, data cleaning, review normalization, competitor mapping

---

## 📂 Project Structure
```text
competitor-analysis/
│
├── data/                         # Example raw data (sample JSONs)
│   └── hair-salons-merged.json
│
├── notebooks/                    # Databricks notebooks (Python + SQL)
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_silver_transformations.sql
│   ├── 03_gold_kpis_and_sentiment.ipynb
│   └── 04_visualization_prep.ipynb
│
├── dashboards/                   # Lakeview dashboard configs
│   ├── competitor_density.json
│   ├── review_sentiment.json
│   └── service_distribution.json
│
├── html_report/                  # Frontend embedding
│   ├── index.html
│   └── config.json               # Dashboard URLs & service principal
│
├── scripts/                      # Helper scripts (local runs)
│   ├── apify_scraper.py          # Apify Google Maps scraping
│   ├── google_api_fetch.py       # Google Maps API integration
│   └── sentiment_labeller.py     # LLM review sentiment labeling
│
└── README.md                     # Project documentation
```

---

## 🔄 Data Pipeline (Medallion Architecture)

1. **Bronze Layer**  
   - Ingest raw Google Maps JSON (places, reviews, services).
   - Minimal processing; raw history preserved.

2. **Silver Layer**  
   - Normalize entities: `places_info`, `places_base`, `reviews_norm`, `services_bridge`.  
   - Handle missing values, deduplicate records, standardize coordinates.

3. **Gold Layer**  
   - Create **analytics-ready tables**.  
   - KPIs:
     - Average rating by neighborhood  
     - Competitor density maps  
     - Review sentiment breakdown (praise vs complaint categories)  
     - Service coverage distribution  
     - **Weighted score metric** (`rating × log(1 + reviews)`)

---

## 📊 Visuals & Reporting
All visuals were built in **Databricks Lakeview** and embedded into an **HTML report** for easy sharing.  

Key sections of the report:
- **Executive Summary**: KPIs & weighted scores
- **Competitor Density**: By neighborhood and map-based
- **Ratings & Reviews**: Distributions, averages, and trends
- **Sentiment Analysis**: Top complaint/praise categories
- **Service Coverage**: Which services are most common, where

---

## 🚀 Key Features
- **End-to-End Pipeline**: From raw Google Maps data → insights in a dashboard  
- **Sector-Agnostic**: Works for salons, restaurants, tattoo shops, and more  
- **Custom Metrics**: Weighted scores, density calculations, LLM sentiment categories  
- **Interactive Dashboards**: Embedded directly into a shareable HTML report  
- **Scalable**: Built on Databricks medallion architecture and Delta Lake  

---

## 📈 Example Insights
- Downtown neighborhoods had the **highest competitor density**, but also **lower average ratings**.  
- Service distribution revealed **underserved categories** (e.g., salons with no men’s cut specialization in certain areas).  
- Sentiment analysis showed **“rushed/careless cuts”** as a top complaint category, highlighting actionable improvement areas.  

---

## 🔒 Access & Limitations
- Data was collected using **Apify Google Maps scrapers** (limited by free-tier quota).  
- **Lakeview dashboards** require proper **service principal permissions** if replicated.  
- Demo HTML report contains **publicly shareable dashboards** (links redacted in this repo).  

---

## 🧭 Future Improvements
- Add **scheduled ingestion** (Airflow/Databricks Jobs).  
- Extend to **multi-city, multi-sector monitoring**.  
- Enhance **review sentiment model** with fine-tuned LLM.  
- Integrate **customer segmentation dashboards** for deeper insights.  

---

## 📬 Contact
Created by Can Okten  
- 💼 [LinkedIn]([https://www.linkedin.com/](https://www.linkedin.com/in/canokten/))
- 📧 canokten.job@gmail.com 

If you’d like to explore extending this SaaS for your sector or region, feel free to connect!

---
