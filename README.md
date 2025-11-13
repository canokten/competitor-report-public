---

## 📊 [Access the demo report here.](https://canokten.github.io/competitor-report-public/)

---

# Competitor Analysis SaaS Prototype (Hair Salons in Vancouver)

*A data engineering + analytics project built on Databricks with Google Maps data integration*

---

## Overview
This project is a **Competitor Analysis SaaS prototype** designed to help local businesses understand their competitive landscape.  
The demo case focuses on **hair salons in Vancouver**, but the system is **sector-agnostic** (extendable to restaurants, tattoo shops, bars, etc.).

The solution combines **data extraction, ETL pipelines, analytics modeling, and interactive dashboards**, all embedded into a shareable **HTML report** for end users.

---

## Tools & Technologies
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

## Project Structure
```text
competitor-analysis/
│
├── data/                              # Data artifacts
│   ├── raw/                           # Raw Apify + Google Maps API JSONs
│   │   ├── apify_places.json
│   │   ├── apify_ratings.json
│   │   └── apify_reviews.json
│   ├── staged/                        # Cleaned & merged exports
│   │   └── places_info.csv
│   │   └── places_reviews.csv
│   │   └── places_ratings.csv
│   └── outputs/                       # Aggregated exports for visuals
│       ├── top_complaints.csv
│       ├── top_praises.csv
│       ├── neighborhood.csv
│       └── kpis.csv
│
├── notebooks/                         # Databricks notebooks (Python + SQL)
│   ├── 01_ingest_raw_bronze.ipynb     # Ingest Apify/API JSON → bronze tables
│   ├── 02_clean_merge_silver.ipynb    # Flatten JSON for reviews, clean, transform and merge → silver tables
│   ├── 03_llm_sentiment.ipynb         # Run LLM on reviews → df_events (complaints/praises)
│   ├── 04_taxonomy_normalize.ipynb    # Normalize categories & shorten aspect/detail labels
│   ├── 05_aggregations_gold.sql       # Aggregations and KPIs (viz-ready for Lakeview dashboards) → gold tables
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
│   └── geomap_correction.py           # Geomap Correcting Neighborhoods [Geomap for Vancouver]
│
└── README.md                          # Project documentation
```
---

## Data Pipeline (Medallion Architecture)

1. **Bronze Layer**  
   - Ingest raw Google Maps JSON (places, reviews, services) and Apify reviews JSON.

2. **Silver Layer**  
   - Normalize entities: `places_info`, `places_ratings`, `places_reviews`.  
   - Handle missing values, deduplicate records, standardize coordinates using geomap data.

3. **Gold Layer**  
   - Create **analytics-ready tables**.  
   - KPIs:
     - Average rating and densities by neighborhood  
     - Competitor density maps 
     - Review sentiment breakdown (praise vs complaint categories)  
     - **Weighted score metric** (`rating × log(1 + reviews)`)

---

## Visualizations & Reporting
All visuals are built in **Databricks Lakeview** and embedded into an **HTML report** for easy sharing, with appropriate Service Principal authorizations saved in Vercel environment. 

---

## Key Features
- End-to-end pipeline with dynamic data ingestion - from raw Google Maps data (can be triggered periodically) to insights in a dashboard.
- Custom metrics such as weighted scores and normalized taxonomies of LLM sentiment categories
- Interactive dashboards embedded directly into the shareable HTML report with dropdown features, filters and map navigation. 

---

## Access & Limitations
- Google Maps places can be extracted using Google Places API (names, coordinates, ratings, contact information, etc.) within the free credit limit with ease.
- Customer review data, on the other hand, was collected using **Apify Google Maps scrapers** (limited by free-tier quota).  
- **Lakeview dashboards** require proper **service principal permissions** if replicated.

---

## Future Improvements
- Add **scheduled ingestion** to keep data up-to-date (Airflow/Databricks Jobs).  
- Extend to **multi-city, multi-sector monitoring** using paid-tier accounts for tools.
- Enhance **review sentiment model** with fine-tuned LLM (more insights can be generated depending on client needs). 

---

## Contact Info
Created by Can Okten  
- 💼 [LinkedIn](https://www.linkedin.com/in/canokten/)
- 📧 canokten.job@gmail.com 

If you’d like to explore extending this SaaS for your sector or region, feel free to connect!

---
