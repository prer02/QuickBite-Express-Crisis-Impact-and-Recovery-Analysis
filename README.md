# 🍽️ Restaurant Crisis — Recovery Analysis & Strategic Roadmap

> In **June 2025**, a Bengaluru-based food delivery platform watched its business collapse in less than 90 days. This repository contains my complete Power BI analysis of what went wrong.
> 

A comprehensive, data-driven diagnosis of a food-delivery startup's crisis — and an evidence-based turnaround strategy.

![Tool](https://img.shields.io/badge/Tool-Power%20BI-F2C811?logo=powerbi&logoColor=black)
![Modeling](https://img.shields.io/badge/Modeling-Star%20Schema-blue)
![Language](https://img.shields.io/badge/Language-DAX-1f6feb)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Domain](https://img.shields.io/badge/Domain-Food%20Delivery%20Analytics-orange)

---

## 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Problem Statement](#-problem-statement)
3. [Dataset Description](#-dataset-description)
4. [Methodology](#-methodology)
5. [Key Findings](#-key-findings)
6. [Recommendations](#-recommendations)
7. [Technical Implementation](#️-technical-implementation)
8. [Deliverables](#-deliverables)
9. [Sources & References](#-sources--references)
10. [How to Explore](#-how-to-explore)

---

## 🎯 Project Overview

**Project Type:** Business Case Analysis | Data Analytics | Strategic Consulting
**Domain:** Food Delivery & Consumer Analytics
**Time Period Analyzed:** January – December 2025
**Focus:** Crisis Diagnosis & Recovery Strategy Development
**Tools Used:** Power BI, DAX, Power Query, Statistical Analysis
**Audience:** Data Analysts, Business Strategists, Recruiters

### Executive Summary

A Bengaluru-based food-delivery startup faced a critical crisis starting **June 2025**, triggered by a combination of:

- 🦠 A **viral food-safety incident** involving partner restaurants
- 🌧️ A **week-long delivery infrastructure outage** during monsoon season
- 📉 **Aggressive competitor campaigns** capitalizing on operational failures
- 💸 **18% GST on delivery** (effective Sept 22, 2025) further squeezing margins

**Crisis Impact (Pre-crisis Jan–May vs Crisis Jun–Dec 2025):**

- 🚨 **70K customers churned** — roughly **70%** of the active base
- 💰 **₹26.68M revenue lost** across the crisis window
- ⭐ **Average rating collapsed** from **4.6 → 2.3 stars**
- 🛵 **SLA compliance fell** from **43.6% → 12.20%**
---

## 💼 Problem Statement

### Business Challenge

The business required a comprehensive analysis of its **June–December 2025 crisis** to:

1. **Understand crisis severity** — Quantify the impact across every business metric
2. **Identify root causes** — Determine what triggered the cascade of failures
3. **Customer impact analysis** — Segment churned customers by recovery probability
4. **Competitive context** — Benchmark against Swiggy / Zomato performance during the same window
5. **Recovery strategy** — Design a data-backed turnaround plan with timelines and ROI
6. **Operational insights** — Identify systemic vulnerabilities to prevent recurrence

### Analysis Questions Addressed

**Primary Analysis (10 questions):**

1. Monthly order decline comparison (pre-crisis vs crisis)
2. Top 5 cities by order decline percentage
3. Top 10 high-volume restaurants with the largest decline
4. Cancellation rate trend and its geographic concentration
5. Delivery SLA performance degradation by month, vehicle, and time-bucket
6. Monthly customer rating fluctuations
7. Negative-keyword sentiment analysis from review text
8. Revenue impact quantification (subtotal vs delivery fee vs discount)
9. Loyalty impact on customers with 5+ orders and 4.5+ ratings
10. High-value (top 5%) customer decline patterns
---

## 📊 Dataset Description

### Data Sources

| Data Type | Source | Time Period | Key Fields |
|-----------|--------|-------------|------------|
| **Orders** | Transactional DB | Jan–Dec 2025 | order_id, customer_id, order_date, order_total, is_cancelled |
| **Customers** | CRM | Jan–Dec 2025 | customer_id, acquisition_date, city, customer_status |
| **Reviews & Ratings** | Review system | Jan–Dec 2025 | rating, sentiment_score, review_text, date |
| **Restaurants** | Partner DB | Jan–Dec 2025 | restaurant_id, cuisine_type, city, cloud_kitchen flag |
| **Delivery / Operations** | Delivery DB | Jan–Dec 2025 | delivery_time, sla_compliance, vehicle_type, delays |

### Data Model (Star Schema)

**Fact tables:**
- `fact_orders` — one row per order (orders, revenue, cancellations)
- `fact_ratings` — one row per review (rating, sentiment, review text)
- `fact_delivery_performance` — one row per delivery (SLA, delay, distance)

**Dimension tables:**
- `dim_customer` — customer master (status: Active / Churned / New / Loyal / Retained, city, VIP flag)
- `dim_restaurant` — restaurant master (cuisine, city, cloud-kitchen flag, risk level)
- `dim_delivery_partner` — partner master (vehicle type, active status, SLA metrics)
- `date` — date dimension with `Month`, `Month_name`, and a **`Crisis type`** flag (Pre-crisis / Crisis)

**Derived tables:**
- `Components` — revenue decomposition (subtotal / delivery fee / discounts → shortfall + % decrease)
- `Loyal_Churned_Customers` — customers with ≥5 pre-crisis orders and 0 crisis orders
- `Restaurant_Risk_Table` — risk-level classification of restaurants based on order decline

### Key Fields & Definitions

**Phase Classification:**
- 🟢 **Pre-crisis:** January – May 2025 (5-month baseline)
- 🔴 **Crisis:** June – December 2025 (7 months of operational failure)

**Customer Segmentation:**

| Segment | Definition | Count |
|---------|-----------|-------|
| Total Customers | All unique customers | **105K** |
| Active Customers(Pre-crisis) | ≥1 order Jan–May 2025 | **100K** |
| Active Customers(Crisis) | ≥1 order Jun–Dec 2025 | **29K** |
| **Churned** | Orders pre-crisis, **ZERO** orders crisis | **70K** |
| New | First order in Jun–Dec 2025 | **17K** |
| Retained | Orders in both periods | **12K** |

**Order Metrics:**
- Pre-crisis orders: **114K orders**
- Crisis monthly average: **35K orders**
- Decline: **69.29%**

**Revenue Metrics:**
- Pre-crisis total: **₹3.762Cr** (5 months)
- Crisis total: **₹1.094Cr** (7 months)
- Difference: **₹2.668Cr lost**
- Decline: **70.9**

> ⚠️ Raw source data is not redistributed in this repository for confidentiality reasons. The `.pbix` file contains the data model embedded, so the report is fully explorable on its own.

---

## 🔬 Methodology

### 1. Data Analysis Framework

#### A. Descriptive Analysis
**Purpose:** Understand current state and crisis severity.

**Metrics calculated:**
- Order volume by month, city, cuisine
- Revenue by component (subtotal, delivery fee, discounts)
- Customer counts by status (Active / Churned / New / Retained / Loyal)
- Cancellation rates and SLA-compliance trends
- Average ratings and sentiment scores

**Tools:** Power BI aggregations, DAX measures, statistical functions

#### B. Comparative Analysis
**Purpose:** Quantify pre-crisis vs crisis changes.

```
Decline % = (Pre-Crisis Value − Crisis Value) / Pre-Crisis Value × 100
```

Applied to orders, revenue, ratings, cancellations, and SLA compliance.

#### D. Revenue Impact Analysis
**Purpose:** Quantify financial loss across revenue components.

```
Total Revenue = Subtotal Amount + Delivery Fee − Discounts Applied
```

| Component | Pre-Crisis | Crisis | Decline % |
|-----------|-----------|--------|-----------|
| Subtotal | ₹3.61Cr | ₹1.07Cr | 70.12% |
| Delivery Fee | ₹34.51 Lacs | 10.33 Lacs| 70.05% |
| Discounts | ₹21.77 Lacs | ₹6.40 Lacs| 70.58% |
| **Net Revenue Lost** | — | — | **₹2.62 Cr (70.12% decline)** |

#### E. Sentiment Analysis
**Purpose:** Understand customer-perception changes.

**Rating-based sentiment scoring:**

| Rating Range | Label | Score |
|--------------|-------|-------|
| 4.5 – 5.0 | Positive | +1.0 |
| 3.5 – 4.4 | Neutral | +0.5 |
| 2.5 – 3.4 | Mixed | −0.5 |
| < 2.5 | Negative | −1.0 |

- Pre-crisis avg rating: **4.5** → Positive sentiment
- Crisis avg rating: **2.5** → Negative sentiment


**Keyword analysis:**- Text parsing on **68,482 reviews**
- Frequency analysis of negative keywords
- Clustering by issue category (food quality, delivery delay, packaging, hygiene)
- Crisis-vs-pre-crisis comparison surfaces what changed


---


### Root Causes

**Primary (Operational):**
- SLA compliance collapsed from **43.6% → 12.2%**
- Delivery infrastructure failed during the monsoon
- Cancellation cascade fed directly into negative review sentiment

**Secondary (Reputational):**
- Viral food-safety incident damaged trust permanently
- Negative-review sentiment dominant by September
- Top complaint themes (from word cloud): **food quality, safety/hygiene, packaging, delivery delay*
*

---

## 💡 Recommendations

### 🚀 Immediate Actions (Month 1)

1. **VIP Reactivation Campaign**
   - Target: ** high-return customers** (≥5 pre-crisis orders, 0 crisis orders)
   - Offer: 40% off + 3 months premium


2. **Food Safety Certification Push**
   - FSSAI + HACCP audits for all partners
   - Visible hygiene badges on the app and listing pages
   - Expected: 35–40% trust improvement

3. **Restaurant Partner Support Program**
   - 5–10% commission reduction for small partners (<50 orders/month)
   - Marketing support for vulnerable cuisines (e.g., North Indian / Biryani — the most at-risk cohort)

### 🛠️ Medium-Term (Months 2–6)

4. **Operational Infrastructure Overhaul**
   - Weather-adaptive routing
   - Fleet expansion in monsoon-heavy zones
   - Real-time SLA monitoring

5. **Customer Retention Program**
   - Tiered loyalty benefits
   - Regular engagement campaigns
   - Continuous-feedback loop

### 📈 Long-Term (Months 6–9)

6. **Market Repositioning**
   - Differentiate on **reliability**, not price
   - Recover the premium segment first
   - Geographic expansion from the recovered base

---

## 🛠️ Technical Implementation

### Tools & Technologies

| Layer | Tool / Technique |
|-------|------------------|
| **Platform** | Microsoft Power BI Desktop |
| **Data Modeling** | Star schema (3 fact + 4 dim + 3 derived tables) |
| **Transformation** | Power Query (M) |
| **Calculation Engine** | DAX |
| **Custom Visuals** | Word Cloud (for negative-review text mining) |
| **Visualization Mix** | Cards, clustered column/bar/line-combo charts, donut, area chart, pivot tables, word cloud |
| **Interactivity** | Slicers for city, month, and crisis type + cross-filtering across all visuals |
| **Navigation** | Page navigator + action buttons on every page |

### Dashboard Structure (7 Pages)

#### 🏠 Page 1 — Home
Landing page with navigation to every analysis section.

#### 📊 Page 2 — Executive Summary
- KPI cards: Total orders, total revenue, average rating, cancellation rate, pre vs crisis revenue
- Monthly revenue trend
- Total orders & cancellation rate by month
- **Top 5 cities with order decline** (pivot)
- **Revenue % decline by component** (subtotal / delivery fee / discounts)

#### 👥 Page 3 — Customer Analysis
- Cards: Total customers, Active, Loyal, Churned, New, Retained
- Customer count by city (donut)
- Customer count by city × status (clustered column)
- **Customers with ≥5 pre-crisis and 0 crisis orders** (pivot — the loyal-but-lost table)

#### 🏪 Page 4 — Restaurant Analysis
- Cards: Total partners, cloud-kitchen count, restaurant count, partner retention rate, active in both periods
- Restaurant count and city retention rate (combo chart)
- **Order comparison by cuisine type** (pre vs crisis)
- Active restaurants by month (line)
- **Top restaurants with ≥50 pre-crisis orders & % decline** (pivot)
- **Restaurants by risk level** (donut)

#### 🛵 Page 5 — Delivery & Operations
- Cards: SLA compliance rate, avg SLA delay, SLA drop, active delivery partners, delay increase, avg deliveries per partner
- SLA compliance and avg distance by vehicle, by month
- Monthly SLA delay × cancellation table
- SLA compliance by vehicle type
- Cancellation rate by city, split by phase
- SLA compliance by time-bucket, split by phase

#### ⭐ Page 6 — Rating & Sentiments
- Average rating by month
- Sentiment score by month (area)
- **Top negative reviews during crisis** (pivot)
- **Negative-word word cloud** (custom visual)
- Review count by month × sentiment category

#### 💎 Page 7 — Top 5% Customers (VIPs)
- Cards: VIP total count, **VIP revenue at risk**, VIP cancellation rate, VIP avg decline, VIP churned avg delay
- VIP customers by cuisine (clustered bar)
- **VIP monthly avg spend** (line)
- VIP avg order frequency — pre vs crisis (clustered column)
- VIP customer count by city (donut)

### Repository Structure

```
restaurant-crisis-analysis/
├── README.md                         ← this file
├── restaurant_crisis.pbix            ← the Power BI report
├── /screenshots/                     ← page-by-page PNG previews
│   ├── 01_home.png
│   ├── 02_executive_summary.png
│   ├── 03_customer_analysis.png
│   ├── 04_restaurant.png
│   ├── 05_delivery_operations.png
│   ├── 06_ratings_sentiments.png
│   └── 07_top_5_percent.png
└── /docs/
    ├── data_dictionary.md            ← (optional) field definitions
    └── measures.md                   ← (optional) full DAX measure list
```

### Example DAX — Defining a Churned Loyal Customer

This is the core measure that operationalizes "**loyal-but-lost**" — customers with ≥5 pre-crisis orders and 0 crisis orders:

```dax
Churned_Customers =
COUNTROWS(
    FILTER(
        ADDCOLUMNS(
            SUMMARIZE(fact_orders, fact_orders[customer_id]),
            "Pre-crisis",
                CALCULATE(
                    COUNT(fact_orders[customer_id]),
                    fact_orders[Order Date] >= DATE(2025, 1, 1),
                    fact_orders[Order Date] <= DATE(2025, 5, 31),
                    fact_orders[is_cancelled] = "N"
                ),
            "crisis",
                CALCULATE(
                    COUNT(fact_orders[customer_id]),
                    fact_orders[Order Date] >= DATE(2025, 6, 1),
                    fact_orders[Order Date] <= DATE(2025, 12, 31),
                    fact_orders[is_cancelled] = "N"
                )
        ),
        [Pre-crisis] >= 5 && [crisis] = 0
    )
)
```

---

## 📦 Deliverables

- ✅ **`restaurant_crisis.pbix`** — fully interactive 7-page Power BI report with embedded data model
- ✅ **Star-schema data model** with documented relationships
- ✅ **30+ DAX measures** covering KPIs, crisis comparisons, customer segmentation, VIP analytics, and operations
- ✅ **Executive Summary page** as a one-screen decision view
- ✅ **VIP / Top 5% page** as a focused revenue-at-risk view
- ✅ **Negative-review word cloud** for qualitative voice-of-customer insight
- ✅ **Recovery roadmap** with quantified ROI across 4 strategic pillars
- ✅ **README** (this document) describing the project end-to-end

---


## 📊 Key Metrics Summary

| Category | Metric | Value | Context |
|----------|--------|-------|---------|
| **Orders** | Pre-crisis monthly | **114K** | Baseline |
| | Crisis monthly | **35K** | Collapsed period |
| | Decline % | **-69.2%** | Severity indicator |
| **Revenue** | Pre-crisis total | **₹37.62M** | 5-month period |
| | Crisis total | **₹10.94M** | 7-month period |
| | Loss | **₹[XX]M** | Absolute impact |
| **Customers** | Pre-crisis active | **83K** | Loyal base |
| | Crisis active | **29K** | Dramatic drop |
| | Churned | **70K** | Lost customers |
| **Ratings** | Pre-crisis | **4.5 ⭐** | Strong satisfaction |
| | Crisis | **2.3 ⭐** | Critical deterioration |
| | Drop | **2.2** | Trust collapse |
| **Operations** | SLA pre | **43.6** | Adequate |
| | SLA crisis | **12.20%** | Failure |
| | Delivery time | **39 → 60 min** | **35%** increase |

## 👤 Author

**Prerna Gautam**
- 💼 LinkedIn: [your-linkedin-url]
- 📧 Email: gautamprerna02@gmail.com
- 🐙 GitHub: [@your-handle]
- 📊 Live Power BI Report: [your-published-link]

> ⭐ If this project was useful, consider starring the repository.

---

## 📜 License

Released for **portfolio and educational purposes**. Underlying business data is not included or redistributed.
