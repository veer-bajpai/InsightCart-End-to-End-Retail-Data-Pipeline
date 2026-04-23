# 🛒 InsightCart: End-to-End Retail Data Pipeline

> **Transforming 3,900 retail transactions into actionable business intelligence — from raw CSV to interactive Power BI dashboard — using Python, PostgreSQL, and SQL analytics.**

---

## 📌 Table of Contents

- [Business Problem](#-business-problem)
- [Pipeline Architecture](#-pipeline-architecture)
- [Tech Stack](#-tech-stack)
- [Dataset Overview](#-dataset-overview)
- [Project Workflow](#-project-workflow)
- [Key Insights](#-key-insights)
- [Business Impact](#-business-impact)
- [Folder Structure](#-folder-structure)
- [How to Run](#-how-to-run)
- [Dashboard Preview](#-dashboard-preview)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🧩 Business Problem

A leading retail company observed shifts in purchasing behavior across customer demographics, product categories, and sales channels. The management team needed data-driven answers to optimize marketing strategy, improve customer retention, and maximize revenue.

**Core business question:**
> *"How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"*

---

## 🏗️ Pipeline Architecture

```
Raw CSV Dataset (3,900 rows × 18 columns)
         │
         ▼
┌─────────────────────┐
│  Python (Pandas)    │  ← Data Cleaning, Feature Engineering,
│  Data Preparation   │    Missing Value Imputation, Column Standardization
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  PostgreSQL         │  ← Structured Storage, Schema Design,
│  Data Warehouse     │    Business Transaction Simulation
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  SQL Analytics      │  ← Revenue Queries, Customer Segmentation,
│  (10+ Queries)      │    Discount Analysis, Cohort Logic
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  Power BI           │  ← Interactive Dashboard, KPI Cards,
│  Dashboard          │    Drill-down Visuals, Stakeholder Reports
└────────┬────────────┘
         │
         ▼
  Business Insights & Strategic Recommendations
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Data Ingestion | Python (Pandas) | Load, explore, and validate raw data |
| Data Cleaning | Python (Pandas, NumPy) | Handle nulls, standardize schema, engineer features |
| Data Storage | PostgreSQL | Relational database for structured querying |
| ORM / Connector | SQLAlchemy + Psycopg2 | Python-to-PostgreSQL integration |
| Analytics | SQL (PostgreSQL) | Business queries, KPIs, segmentation logic |
| Visualization | Power BI | Interactive dashboard for stakeholders |
| Environment | Jupyter Notebook | Exploratory analysis and documentation |
| Version Control | Git + GitHub | Project tracking and portfolio hosting |

---

## 📊 Dataset Overview

| Attribute | Detail |
|---|---|
| **Source** | Consumer shopping behavior dataset |
| **Rows** | 3,900 transactions |
| **Columns** | 18 features |
| **Missing Values** | 37 nulls in `Review Rating` (imputed via category median) |

**Feature Groups:**

- **Demographics** — `Customer ID`, `Age`, `Gender`, `Location`
- **Purchase Details** — `Item Purchased`, `Category`, `Purchase Amount (USD)`, `Season`, `Size`, `Color`
- **Behavior Signals** — `Discount Applied`, `Previous Purchases`, `Frequency of Purchases`, `Review Rating`, `Shipping Type`, `Subscription Status`, `Payment Method`

---

## 🔄 Project Workflow

### Step 1 — Data Preparation (Python)
- Loaded dataset using `pandas`
- Conducted initial EDA: `.info()`, `.describe()`, null audit
- Imputed missing `Review Rating` values using **per-category median** to preserve statistical integrity
- Renamed all columns to `snake_case` for SQL compatibility
- Verified and resolved redundancy between `discount_applied` and `promo_code_used` — dropped the latter
- Exported cleaned DataFrame to PostgreSQL

### Step 2 — Feature Engineering (Python)
- `age_group` — Binned customer ages into: `Young Adult`, `Adult`, `Middle-aged`, `Senior`
- `purchase_frequency_days` — Derived numeric frequency metric from categorical purchase cadence

### Step 3 — Database Integration (PostgreSQL)
- Connected Python to PostgreSQL using `SQLAlchemy` + `psycopg2`
- Loaded cleaned DataFrame into a structured relational table
- Validated data integrity post-load

### Step 4 — SQL Business Analysis (10 Queries)
Ran structured SQL queries to answer key business questions:

| # | Query | Business Question |
|---|---|---|
| 1 | Revenue by Gender | Which gender drives more revenue? |
| 2 | High-Spending Discount Users | Do discount users still spend above average? |
| 3 | Top 5 Products by Rating | Which products have the highest satisfaction? |
| 4 | Shipping Type Comparison | Does shipping speed affect spending? |
| 5 | Subscribers vs Non-Subscribers | How does subscription impact revenue? |
| 6 | Discount-Dependent Products | Which products rely most on discounts? |
| 7 | Customer Segmentation | How are customers distributed across loyalty tiers? |
| 8 | Top 3 Products per Category | What sells most in each category? |
| 9 | Repeat Buyers & Subscriptions | Do repeat buyers convert to subscribers? |
| 10 | Revenue by Age Group | Which age group contributes most to revenue? |

### Step 5 — Dashboard (Power BI)
- Built interactive Customer Behavior Dashboard with:
  - KPI cards: Total Customers, Avg Purchase Amount, Avg Review Rating
  - Donut chart: Subscription status distribution
  - Bar charts: Revenue & Sales by Category, Revenue & Sales by Age Group
  - Slicers: Gender, Category, Subscription Status, Shipping Type

### Step 6 — Insights & Recommendations
- Synthesized findings into actionable business strategies (see [`insights.md`](./insights.md))

---

## 💡 Key Insights

- 📊 **Male customers** account for ~67% of total revenue ($157,890 vs $75,191), driven by higher transaction volume
- 🚚 **Express shipping users** spend ~$60.48 on average vs $58.46 for Standard — a premium segment worth targeting
- 🔖 **27% of customers** are subscribers, yet they exhibit comparable per-transaction spend to non-subscribers — loyalty program ROI is strong
- 💸 **839 customers** used discounts but still spent above average — discounts are not eroding high-value behavior
- ⭐ **Gloves, Sandals, and Boots** are the top-rated products — ideal candidates for featured placement
- 🛍️ **Loyal customers** (3,116 of 3,900) dominate the base — retention is more valuable than acquisition
- 👔 **Young Adults** lead all age groups in revenue ($62,143), followed closely by Middle-aged ($59,197)
- 🎯 **Hat and Sneakers** have the highest discount dependency (~50%) — pricing strategy review needed

---

## 📈 Business Impact

| Recommendation | Estimated Opportunity |
|---|---|
| Expand subscription program | Unlock higher revenue per customer through loyalty perks |
| Optimize discount strategy for Hat & Sneakers | Protect margin while maintaining conversion rates |
| Target Young Adult segment with personalized campaigns | Capitalize on highest revenue-generating cohort |
| Feature top-rated products in homepage/campaigns | Leverage social proof to drive higher-AOV purchases |
| Convert Returning → Loyal customers via loyalty points | Reduce churn, increase LTV across 701 returning customers |

---

## 📁 Folder Structure

```
InsightCart-Retail-Pipeline/
│
├── data/
│   ├── raw/
│   │   └── shopping_behavior.csv          # Original dataset
│   └── processed/
│       └── cleaned_shopping_data.csv      # Cleaned & engineered dataset
│
├── notebooks/
│   └── InsightCart_End-to-End_Retail_Data_Pipeline.ipynb  # Full EDA + pipeline
│
├── sql/
│   └── business_queries.sql              # All 10 SQL business analysis queries
│
├── dashboard/
│   └── InsightCart_Dashboard.pbix        # Power BI dashboard file
│
├── reports/
│   ├── Business_Report.pdf               # Final project report
│   └── Business_Problem_Document.pdf     # Problem statement
│
├── insights.md                           # Business insights document
├── requirements.txt                      # Python dependencies
├── .gitignore                            # Git exclusion rules
└── README.md                             # Project documentation (this file)
```

---

## ⚙️ How to Run

### Prerequisites
- Python 3.9+
- PostgreSQL 14+ (running locally or via Docker)
- Power BI Desktop (for dashboard)

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/InsightCart-Retail-Pipeline.git
cd InsightCart-Retail-Pipeline
```

### 2. Set Up Python Environment
```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Configure Database Connection
Create a `.env` file in the root directory:
```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=insightcart
DB_USER=your_postgres_user
DB_PASSWORD=your_postgres_password
```

### 4. Set Up PostgreSQL Database
```bash
psql -U your_postgres_user -c "CREATE DATABASE insightcart;"
```

### 5. Run the Jupyter Notebook
```bash
jupyter notebook notebooks/InsightCart_End-to-End_Retail_Data_Pipeline.ipynb
```
> Run all cells sequentially. The notebook will clean the data, engineer features, and load everything into PostgreSQL automatically.

### 6. Run SQL Queries
Open `sql/business_queries.sql` in pgAdmin, DBeaver, or any PostgreSQL client and execute the queries against the `insightcart` database.

### 7. Open Power BI Dashboard
Open `dashboard/InsightCart_Dashboard.pbix` in **Power BI Desktop** and refresh the data source to point to your local PostgreSQL instance.

---

## 🖼️ Dashboard Preview

> *Screenshots to be added after final dashboard export.*

| View | Description |
|---|---|
| `screenshots/dashboard_overview.png` | Full dashboard with KPI cards and all charts |
| `screenshots/revenue_by_category.png` | Revenue breakdown by product category |
| `screenshots/age_group_analysis.png` | Revenue and sales by customer age group |
| `screenshots/subscription_donut.png` | Subscriber vs non-subscriber distribution |

---

## 🔭 Future Improvements

- [ ] **Predictive Modeling** — Build a churn prediction model using logistic regression or XGBoost on customer behavior signals
- [ ] **RFM Analysis** — Implement Recency-Frequency-Monetary scoring for advanced customer segmentation
- [ ] **Automated ETL Pipeline** — Orchestrate the pipeline using Apache Airflow for scheduled data refresh
- [ ] **Real-time Dashboard** — Migrate Power BI to a Streamlit or Dash web app for browser-based access
- [ ] **A/B Test Simulation** — Model the revenue impact of different discount thresholds using simulation
- [ ] **API Layer** — Expose key insights via a FastAPI endpoint for integration with business tools
- [ ] **Docker Compose** — Containerize the PostgreSQL + Jupyter environment for one-command setup

---

## 👤 Author

**[Your Name]**
Data Engineer | Data Analyst | Python & SQL

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/yourprofile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/yourusername)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-green?style=flat&logo=globe)](https://yourportfolio.com)

---

> ⭐ *If you found this project useful or insightful, consider giving it a star — it helps others discover it too.*
