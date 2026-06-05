# Customer Purchase Behaviour Analytics (Python, SQL, Power BI)

An end-to-end data analytics project that walks through the complete analytics pipeline — from raw data to an interactive Power BI dashboard — using **Python**, **MySQL**, and **Power BI**.

---

## Project Overview

This project analyses customer shopping behaviour to uncover patterns around revenue, product preferences, discount usage, subscription status, and demographic segmentation. The workflow follows a three-stage pipeline:

```
Raw CSV Data → Python (Cleaning & Feature Engineering) → MySQL (Analysis) → Power BI (Dashboard)
```

---

## Tech Stack

| Layer | Tool | Purpose |
|---|---|---|
| Data Preparation | Python (Pandas) | Cleaning, feature engineering, DB upload |
| Data Storage | MySQL | Structured storage and SQL analysis |
| Visualisation | Power BI | Interactive business dashboard |

---

## Stage 1 — Python: Data Cleaning & Feature Engineering

The raw dataset (`customer_shopping_behavior.csv`) was loaded into a Pandas DataFrame and processed through the following steps:

### Data Cleaning
- **Null handling:** Missing values in `Review Rating` were imputed using the **median rating per product category** (group-wise median imputation) to preserve category-level rating patterns.
- **Column standardisation:** All column names were lowercased and spaces replaced with underscores for SQL compatibility.
- **Column renaming:** `purchase_amount_(usd)` renamed to `purchase_amount` for cleaner querying.
- **Redundant column removal:** `promo_code_used` was found to be perfectly correlated with `discount_applied` (100% match verified with `.all()`) and was dropped to eliminate duplication.

### Feature Engineering
- **Age Grouping:** A new categorical column `age_groups` was engineered using the following bins and labels:

  | Group | Age Range |
  |---|---|
  | 18–25 | Young Adults |
  | 25–35 | Early Career |
  | 35–45 | Mid Career |
  | 45–55 | Senior Adults |
  | 55+ | Older Adults |

### MySQL Upload
- The cleaned DataFrame was pushed directly to a MySQL database (`projects`) using **SQLAlchemy** + **PyMySQL**:

---

## Stage 2 — MySQL: Business Analysis

With the cleaned data loaded in MySQL, the following business questions were answered using SQL:

1. Revenue by Gender
2. Discount Users Who Still Spent Above Average
4. Average Spend: Express vs Standard Shipping
5. Subscribed vs Non-Subscribed Customers
6. Products with Highest Discount Rate
7. Loyal Customers (5+ Previous Purchases) by Subscription Status
8. Revenue by Age Group

---

## Stage 3 — Power BI: Interactive Dashboard

Power BI was connected directly to the MySQL database to pull the analysed data and build an interactive dashboard. The dashboard visualises:

- Total revenue breakdown by **gender** and **age group**
- **Top-rated products** and discount penetration by item
- **Subscription vs non-subscription** customer comparison (count, average spend, total revenue)
- **Shipping preference** analysis (Express vs Standard spend)
- Customer loyalty segmentation based on purchase history

---

## Key Insights

- Discount users who spend above average represent a high-value segment worth targeted retention.
- Subscription customers show significantly higher lifetime spend compared to non-subscribers.
- Age group segmentation reveals which demographics drive the most revenue.
- Certain products attract disproportionately high discount rates, indicating potential margin leakage.

---
