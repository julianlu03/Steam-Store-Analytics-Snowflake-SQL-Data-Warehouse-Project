# Steam Store Analytics - Snowflake SQL Data Warehouse Project
Built an end-to-end Snowflake data warehouse for 27K+ Steam games using medallion architecture (Bronze/Silver/Gold), dimensional modeling, and Snowflake-native AI features.

## Overview

This project implements an end-to-end analytics pipeline in **Snowflake** using a medallion architecture (Bronze / Silver / Gold) to analyze the Steam game marketplace. The pipeline is built entirely with Snowflake-native SQL notebooks, emphasizing clean data modeling, incremental processing, and analytics-ready outputs. The final datasets power exploratory analysis and dashboards across categories, genres, publishers, reviews, and sentiment.

**Primary goal:** demonstrate production-style SQL, Snowflake fundamentals, and analytics engineering best practices

---

## Tech Stack

* **Snowflake SQL (Notebooks)**
* Medallion Architecture (Bronze / Silver / Gold)
* Star Schema & Bridge Tables
* Snowflake Streams & MERGE (Incremental Loads)
* Snowflake Cortex (Sentiment, Summarization, Semantic Enrichment)
* Streamlit (Dashboards)

---

## Repository Structure

```
steam-snowflake-analytics/
│
├── notebooks/
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_silver_cleaning.ipynb
│   ├── 03_gold_modeling.ipynb
│   ├── 04_incremental_streams.ipynb
│   ├── 05_ai_enrichment.ipynb
│   └── full_pipeline.ipynb
│
├── diagrams/
│   └── star_schema_design.png
│
├── dashboards/
│   ├── category_dashboard.png
│   ├── genre_dashboard.png
│   └── publisher_dashboard.png
│
└── README.md
```

---

## Execution Environment

All transformations were implemented using **Snowflake SQL notebooks**, executing directly within Snowflake’s compute environment. This mirrors real-world Snowflake workflows where notebooks are used for pipeline prototyping, analytics development, and iterative modeling without external orchestration frameworks.

Some functionalities of the project aren't able to be demonstrated (ie. Cortex Analyst using SnowFlake UI Playground) due to the GitHub environment.

The `full_pipeline.ipynb` notebook provides a linear, end-to-end execution path, while the numbered notebooks modularize each layer of the pipeline.

---

## Data Pipeline Walkthrough

### 1. Bronze Layer — Raw Ingestion

**Notebook:** `01_bronze_ingestion.ipynb`

* Ingests raw Steam game data into Snowflake
* Minimal transformations
* Preserves source fidelity
* Performs basic sanity checks (row counts, nulls)

**Purpose:** establish a stable, auditable raw data foundation.

---

### 2. Silver Layer — Cleaning & Normalization

**Notebook:** `02_silver_cleaning.ipynb`

* Deduplicates records
* Normalizes text fields (names, descriptions)
* Type casting and validation
* Constructs bridge tables for many-to-many relationships (e.g., games ↔ genres)

**Purpose:** prepare clean, consistent, analysis-ready data.

---

### 3. Gold Layer — Analytics Modeling

**Notebook:** `03_gold_modeling.ipynb`

* Builds fact and dimension tables
* Implements star schema design
* Produces aggregated metrics for dashboards and analysis

**Purpose:** deliver analytics-ready datasets aligned with business questions.

---

### 4. Incremental Processing

**Notebook:** `04_incremental_streams.ipynb`

* Uses Snowflake Streams to capture changes
* Applies **MERGE / UPSERT** logic
* Simulates ongoing ingestion and downstream refreshes

**Purpose:** demonstrate production realism and efficient data refresh strategies.

---

### 5. AI Enrichment (Snowflake Cortex)

**Notebook:** `05_ai_enrichment.ipynb`

* Applies `CORTEX.SENTIMENT` to user reviews
* Uses `CORTEX.SUMMARIZE` for text abstraction
* Demonstrates semantic enrichment directly in SQL

**Purpose:** enrich structured data with ML-powered insights using Snowflake-native tooling.

---

## Dashboards

Streamlit dashboards visualize insights across:

* Game categories
* Genres
* Publishers

These dashboards consume Gold-layer tables and demonstrate how the warehouse supports downstream analytics and visualization.

---

## Key Design Decisions

* **Notebooks over raw SQL files:** preserves execution context, documentation, and sequencing
* **Medallion architecture:** enforces clean separation of concerns
* **Incremental loading:** avoids full refreshes and supports scale
* **AI enrichment post-cleaning:** ensures models operate on normalized data
