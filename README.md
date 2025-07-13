# Ethiomed Data Platform

## Overview

This project is a modern end-to-end ELT data platform designed to generate insights about Ethiopian medical businesses using data scraped from public Telegram channels. We built this pipeline to extract, store, transform, and enrich both text and image-based content for analytical purposes.

The platform helps answer business questions such as:

- What are the top 10 most frequently mentioned medical products or drugs?
- How does the price or availability of specific products vary across channels?
- Which channels post the most visual content (e.g., pills, creams)?
- What are the daily and weekly trends in health-related Telegram posts?

---

## Key Features

- **Telegram Scraping**: Collects raw messages and media from selected public channels.
- **Data Lake**: Stores raw data in a partitioned, organized format.
- **PostgreSQL Warehouse**: Stores structured, query-optimized data using a dimensional star schema.
- **dbt Transformation**: Cleans, models, and validates data in layers (staging → marts).
- **YOLOv8 Enrichment**: Detects objects in images to enhance the analytical context.
- **FastAPI**: Exposes insights through a REST API for dashboards and reporting.
- **Dagster**: Orchestrates and schedules the end-to-end data pipeline.

---

## Tech Stack

- Python, Pandas, SQLAlchemy, Telethon
- PostgreSQL
- dbt (Data Build Tool)
- FastAPI + Uvicorn
- YOLOv8 (Ultralytics)
- Dagster
- Docker

---

## Directory Structure

ethiomed-data-platform/

├── data/raw/telegram_messages/ # Raw JSON data from Telegram

├── src/

│ ├── scraping/ # Telegram scraping logic

│ ├── loading/ # Load raw data into PostgreSQL

│ └── enrichment/ # YOLO image analysis

├── dbt_project/ # dbt models and configs

├── api/ # FastAPI application

├── .env # Environment variables (not committed)

├── .gitignore

├── requirements.txt

├── README.md



---

## Tasks Summary

### 🛠️ Setup & Configuration
- Project initialized using Git and Docker.
- Dependencies managed with `requirements.txt`.
- Secrets stored in `.env` and excluded from version control.

###  Extract & Load
- Scrape Telegram messages and images using Telethon.
- Store raw data as JSON in the `data/raw` directory.

###  Transform (dbt)
- Load raw JSON into PostgreSQL.
- Use dbt to clean, validate, and build:
  - `dim_channels`
  - `dim_dates`
  - `fct_messages`
  - `fct_image_detections`

###  Enrichment (YOLO)
- Apply YOLOv8 for object detection in images.
- Integrate results with message data for analytics.

###  API (FastAPI)
- Provide endpoints for common queries:
  - `/api/reports/top-products`
  - `/api/channels/{channel}/activity`
  - `/api/search/messages`

### Orchestration (Dagster)
- Define jobs and schedules to automate the pipeline.

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/Dagi2730/ethiomed-data-platform.git
   cd ethiomed-data-platform
