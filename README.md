---

## 📊 [Access the report here.](https://canokten.github.io/competitor-report-public/)

---

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
├── data/                              # Data artifacts
│   ├── raw/                           # Raw Apify + Google Maps API JSONs
│   │   ├── apify_places.json
│   │   ├── apify_ratings.json
│   │   └── apify_reviews.json
│   ├── staged/                        # Cleaned & merged exports
│   │   └── hair-salons-merged.json
│   └── outputs/                       # Aggregated exports for visuals
│       ├── top_complaints.csv
│       ├── top_praises.csv
│       └── kpis.csv
│
├── notebooks/                         # Databricks notebooks (Python + SQL)
│   ├── 01_ingest_raw_bronze.ipynb     # Ingest Apify/API JSON → bronze tables
│   ├── 02_clean_merge_silver.ipynb    # Filter hair salons, clean & merge → silver tables
│   ├── 03_flatten_model.ipynb         # Flatten JSON → places_base, places_info, places_reviews
│   ├── 04_llm_sentiment.ipynb         # Run LLM on reviews → df_events (complaints/praises)
│   ├── 05_taxonomy_normalize.ipynb    # Normalize categories & shorten aspect/detail labels
│   ├── 06_aggregations_gold.sql       # Aggregations & KPIs → gold tables
│   └── 07_visualization_prep.ipynb    # Prep viz-ready wide tables for Lakeview dashboards
│
├── dashboards/                        # Lakeview dashboard configs
│   ├── Business Density by Neighborhood
│   ├── Neighborhood Performance Score
│   ├── Competitor Locations & Densities
│   ├── Review Categories Summary
│   ├── Top 25 Salons (Weighted Score)
│   └── Bottom 25 Salons (Weighted Score)
│
├── html_report/                       # Frontend embedding
│   ├── index.html
│   └── config.json                    # Dashboard URLs & service principal
│
├── scripts/                           # Helper scripts (local runs / API calls)
│   ├── googlemaps-api.ipynb           # Google Maps API integration
│   └── google_api_fetch.py            # Geomap Correcting Neighborhoods [Geomap for Vancouver](https://opendata.vancouver.ca/explore/dataset/local-area-boundary/export/?disjunctive.name))
│
└── README.md                          # Project documentation
```
---

## 🔄 Data Pipeline (Medallion Architecture)

1. **Bronze Layer**  
   - Ingest raw Google Maps JSON (places, reviews, services) and Apify reviews JSON.
   - Minimal processing; raw history preserved.

2. **Silver Layer**  
   - Normalize entities: `places_info`, `places_base`, `reviews_norm`.  
   - Handle missing values, deduplicate records, standardize coordinates using geomap data.

3. **Gold Layer**  
   - Create **analytics-ready tables**.  
   - KPIs:
     - Average rating and densities by neighborhood  
     - Competitor density maps 
     - Review sentiment breakdown (praise vs complaint categories)  
     - **Weighted score metric** (`rating × log(1 + reviews)`)

---

## 📊 Visuals & Reporting
All visuals were built in **Databricks Lakeview** and embedded into an **HTML report** for easy sharing.  

Key sections of the report:
- **Executive Summary**: KPIs & weighted scores
- **Competitor Density**: By neighborhood and map-based
- **Ratings & Reviews**: Distributions, averages, and trends
- **Sentiment Analysis**: Top complaint/praise categories

---

## 🚀 Key Features
- **End-to-End Pipeline**: From raw Google Maps data → insights in a dashboard  
- **Sector-Agnostic**: Works for salons, restaurants, tattoo shops, and more  
- **Custom Metrics**: Weighted scores, density calculations, LLM sentiment categories  
- **Interactive Dashboards**: Embedded directly into a shareable HTML report  
- **Scalable**: Built on Databricks medallion architecture and Delta Lake  

---

## 🔒 Access & Limitations
- Review data was collected using **Apify Google Maps scrapers** (limited by free-tier quota).  
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
- 💼 [LinkedIn](https://www.linkedin.com/](https://www.linkedin.com/in/canokten/)
- 📧 canokten.job@gmail.com 

If you’d like to explore extending this SaaS for your sector or region, feel free to connect!

---
