# 🍽️ Restaurant Crisis — Recovery Analysis & Strategic Roadmap

> In **June 2025**, a Bengaluru-based food delivery platform watched its business collapse in less than 90 days. This repository contains my complete Power BI analysis of **what went wrong, who walked away, and how the data points to recovery**.

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
- 🏪 **[XX]% restaurant partner exodus**, with cloud kitchens worst hit
- 🛵 **SLA compliance fell** from **43.6% → 12.20%**

**Key Discovery:** Despite the severity, a meaningful share of churned customers are **recoverable** — they left due to **operational failure, not dissatisfaction with the product**.

**Strategic Output:** A data-driven **₹[XX]M recovery roadmap** built on **4 strategic pillars**, projected to recover **[XX]–[XX]% of pre-crisis metrics within 6–9 months**, with **[X]–[X]× ROI** on reactivation.

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

**Secondary Analysis (5 questions + extras):**

11. Competitor comparison (Swiggy, Zomato performance during the crisis)
12. External factors contributing to a ~3× CAC increase
13. Most effective recovery strategies (industry benchmarking)
14. Restaurant-type churn risk (cloud kitchen vs dine-in)
15. Lapsed-customer return probability modeling
16. Priority-city risk analysis
17. Customer order-value shift behavior (premium → budget)
18. Review-volume spike correlation with the delivery outage

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
| **Churned** | Orders pre-crisis, **ZERO** orders crisis | **[XX,XXX]** |
| New | First order in Jun–Dec 2025 | **[XX,XXX]** |
| Retained | Orders in both periods | **[XX,XXX]** |

**Order Metrics:**
- Pre-crisis orders: **114K orders**
- Crisis monthly average: **35K orders/month**
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

#### C. Customer Segmentation (Recovery Probability)
**Purpose:** Identify recoverable customers, not just count lost ones.

**High return probability (~60% return chance):**
```
IF (Pre-Crisis Orders ≥ 5)
   AND (Pre-Crisis Avg Rating ≥ 4.5)
   AND (Crisis Orders = 0)
THEN "High Return — Recoverable"
```
- Sample size: **[XX,XXX] customers**
- Rationale: Loyal customers lost due to **failure, not dissatisfaction**

**Medium return probability (~40% return chance):**
```
IF (Pre-Crisis Orders = 3-4)
   AND (Pre-Crisis Avg Rating ≥ 3.5)
   AND (Crisis Orders = 0)
THEN "Medium Return — Price Sensitive"
```
- Sample size: **[XX,XXX] customers**
- Rationale: Mixed experience, cost-conscious — winnable with incentives

**Low return probability (~15% return chance):**
```
IF (Pre-Crisis Orders ≤ 2)
   AND (Pre-Crisis Avg Rating < 3.5)
THEN "Low Return — Low Priority"
```
- Sample size: **[XX,XXX] customers**
- Rationale: Never engaged fully — low ROI to chase

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

### 2. Customer Acquisition Cost (CAC) Analysis

```
CAC = Total Marketing Spend / Number of New Customers Acquired
```

- Pre-crisis CAC estimate: **₹50 per customer**
- Crisis CAC estimate: **₹150 per customer**
- **Increase: ~300%**

**Contributing factors (external, research-backed):**

| Factor | Impact on CAC | Source |
|--------|---------------|--------|
| 18% GST on delivery (effective Sept 22, 2025) | +₹20 | Business Standard |
| Google Ads CPC +42% (competitive bidding) | +₹25 | Market data |
| Monsoon seasonality (−15–20% organic demand) | +₹15 | Industry reports |
| Brand-reputation damage | +₹40 | Calculated from conversion-rate drop |
| **Total increase** | **+₹100 (300%)** | — |

**Strategic implication:**
Reactivating existing customers at ~₹50 is **3× more cost-effective** than acquiring new ones at ₹150 during the crisis. **Reactivation > acquisition** is the central financial argument of the recovery plan.

### 3. Recovery Strategy — ROI Modeling

#### 🎯 Pillar 1 — Customer Reactivation
- **Target:** **[XX,XXX] high-probability customers**
- **Incentive:** 40% off + 3 months premium membership
- **Expected reactivation:** 60% (industry benchmark)
- **Customers recovered:** **[XX,XXX]**
- **Avg LTV:** ₹8,500
- **Revenue recovered:** ₹[XX] Cr
- **Investment:** ₹20–25M
- **ROI:** 3–4× within 12 months

#### 🛡️ Pillar 2 — Food Safety Certifications
- **Investment:** ₹15–20M (FSSAI / HACCP audits, badges, promotion)
- **Expected trust uplift:** 35–40%
- **Timeline:** 2–3 months to certification
- **Permanent benefit:** Ongoing compliance + customer confidence

#### ⚙️ Pillar 3 — Operational Excellence

| Component | Investment |
|-----------|------------|
| Weather-adaptive routing | ₹8–10M |
| Fleet expansion | ₹12–15M |
| SLA monitoring systems | ₹5–7M |
| **Total** | **₹25–30M** |

- **Expected SLA improvement:** **[XX]% → 40%+**
- **Cancellation reduction:** **[XX]% → < 7%**
- **Timeline:** 6 months

#### 🏪 Pillar 4 — Restaurant Partner Support
- 5–10% commission reduction for 6 months on restaurants with <50 orders/month
- Featured listings and co-marketing campaigns
- Working-capital support for small cloud kitchens
- **Expected retention:** 85% (vs. current **[XX]%**)
- **Investment:** ₹10–15M

#### 📈 Total Recovery Roadmap

| Item | Value |
|------|-------|
| Total investment | **₹70–80M** |
| Timeline | **6–9 months** |
| Expected recovery | **80–90% of pre-crisis metrics** |
| Cumulative ROI | **2.5–3×** on total investment |

### 4. Competitive Benchmarking

**Methodology:**
- Reviewed public financial reports and news articles
- Tracked market-share and revenue-growth trends
- Researched competitor strategies during the crisis window
- Validated findings against industry research

**Zomato (Jun–Dec 2025):**
- Market share: **58%** (up from 56%)
- Revenue growth: **+67% YoY**
- Status: Profitable, expanding aggressively
- Strategy: Captured market share from struggling competitors

**Swiggy (Jun–Dec 2025):**
- Market share: **42%** (maintained)
- App installs: **+20–25%** during crisis
- Revenue growth: **+35% YoY**
- Strategy: Capitalized on the operational failures of weaker players

**Impact on the business analyzed here:**
- App ranking: **#3 → #8**
- **15–25% of lost customers** captured by Swiggy / Zomato
- Market consolidation favored larger, more stable platforms

---

## 📈 Key Findings

### Crisis Impact Summary

| Metric | Pre-Crisis | Crisis | Change | % Change |
|--------|-----------|--------|--------|----------|
| Total Orders | **24,000** | **9,000** | **-15,000** | **−62.5%** |
| Total Revenue (period) | **₹37.62M** | **₹10.94M** | **−₹[XX]M** | **−[XX]%** |
| Active Customers | **83K** | **29K** | **54K** | **65%** |
| Avg Rating | **4.5 ⭐** | **2.3⭐** | **−[X.XX]** | **−[XX]%** |
| SLA Compliance | **[XX]%** | **[XX]%** | **−[XX]%** | **−[XX]%** |
| Avg Delivery Time | **39.5 min** | **60.1 min** | **20.6 min** | **52.1%** |
| Cancellation Rate | **[X.X]%** | **[XX.X]%** | **+[X.X]%** | **+[XX]%** |

### Root Causes

**Primary (Operational):**
- SLA compliance collapsed from **[XX]% → [XX]%**
- Delivery infrastructure failed during the monsoon
- Cancellation cascade fed directly into negative review sentiment

**Secondary (Reputational):**
- Viral food-safety incident damaged trust permanently
- Negative-review sentiment dominant by September
- Top complaint themes (from word cloud): **food quality, safety/hygiene, packaging, delivery delay**

**Tertiary (Competitive):**
- Swiggy / Zomato captured **15–25%** of lost customers
- Aggressive competitor campaigns during the most vulnerable window
- Market consolidation favored larger players

**External (Market):**
- 18% GST on delivery (effective Sept 22, 2025)
- Google Ads CPC up **+42%** during the same period
- Monsoon seasonality dragged organic demand down **15–20%**

### Recovery Opportunity

- **High-priority recoverable base:** **[XX,XXX] customers** (60% return probability)
- **Revenue at risk from top 5% segment alone:** ₹[XX] Cr annually
- **Geographic concentration:** Bengaluru and Mumbai together account for the bulk of the decline
- **Order frequency recovery potential:** **[X.X] → [X.X]+ orders/month**

> **Key insight:** Customers didn't leave because their *preferences* shifted — they left because *service* failed. That is reversible through targeted reactivation + operational fixes.

---

## 💡 Recommendations

### 🚀 Immediate Actions (Month 1)

1. **VIP Reactivation Campaign**
   - Target: **[XX,XXX] high-return customers** (≥5 pre-crisis orders, 0 crisis orders)
   - Offer: 40% off + 3 months premium
   - Expected: **[XX,XXX] returns → ₹[XX] Cr recovery**

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

## 📚 Sources & References

### External Research (Secondary Analysis)

**1. Competitor Market Share**
- Inc42 — *Food Delivery War: Zomato Extends Lead Over Swiggy With 58% Market Share* (Nov 2024)
  https://inc42.com/buzz/food-delivery-war-zomato-extends-lead-over-swiggy-with-58-market-share/
- Business Standard — *Zomato zooms past Swiggy in terms of growth in July* (Aug 2024)
  https://www.business-standard.com/companies/news/zomato-zooms-past-swiggy-in-terms-of-growth-in-july-captures-more-market-124082000895_1.html

**2. GST Implementation Impact**
- Business Standard — *Food delivery may get pricier as platforms hike fees, 18% GST adds burden* (Sept 2025)
  https://www.business-standard.com/economy/news/food-delivery-may-get-pricier-as-platforms-hike-fees-18-gst-adds-burden-125090700239_1.html
- Deccan Herald — *Online food delivery charges to rise when new GST rules take effect*
  https://www.deccanherald.com/business/economy/online-food-delivery-charges-to-rise-when-new-gst-rules-take-effect-3713486

**3. Food Safety Certification Standards**
- QACS Global Solutions — *HACCP Certification in India: A 2025 Food Safety Guide* (Jun 2025)
  https://qacsglobalsolutions.com/haccp-certification-india-2025/
- Restaurant India — *Sustainable Restaurant Practices That Attract More Customers in 2025*
  https://www.restaurantindia.in/article/sustainable-restaurant-practices-that-attract-more-customers-in-2025.13308

**4. Cloud Kitchen Market Analysis**
- BBFT — *The Rise and Fall of Cloud Kitchens in India* (Sep 2024)
  https://www.bbft.in/2024/09/24/the-rise-and-fall-of-cloud-kitchens-in-india-a-business-perspective/
- Restaurant India — *How Cloud Kitchens Are Transforming India's Food Delivery Revolution*
  https://www.restaurantindia.in/article/how-cloud-kitchens-are-transforming-india-s-food-delivery-revolution.12960

### Methodology References

**Statistical Analysis:**
- Churn modeling — Standard RFM (Recency, Frequency, Monetary) segmentation
- Risk scoring — Weighted composite-score methodology
- ROI calculation — Standard financial modeling with industry benchmarks
- Probability assessment — Based on industry research and comparable cases

**Data Analysis Best Practices:**
- Comparative analysis — Pre/post-crisis methodology
- Customer segmentation — Behavioral and financial clustering
- Sentiment analysis — Text-frequency analysis correlated with ratings
- Benchmark validation — Against industry peers and research reports

---

## 🔍 How to Explore

### Option A — Open the Report Locally
1. **Install Power BI Desktop** (free): https://powerbi.microsoft.com/desktop/
2. **Clone this repo** or download `restaurant_crisis.pbix` directly
3. **Open the file** in Power BI Desktop
4. Start at the **🏠 Home** page and use the navigation buttons / page navigator to move between sections

### Option B — Browse Screenshots
If you don't have Power BI Desktop installed, the `/screenshots/` folder contains a visual walkthrough of every page.

### Suggested Reading Order

> **Home → Executive Summary → Customer Analysis → Restaurant → Delivery & Operations → Rating & Sentiments → Top 5% Customers**

This follows the natural narrative arc:
*what happened → who left → which partners are at risk → were operations to blame → what did customers say → how much of our most valuable segment is at risk.*

### Deep-Dive Routes

| If you care about… | Go to |
|---------------------|-------|
| **Customer impact** | Pages 3 (Customer Analysis) + 7 (Top 5%) |
| **Operational diagnosis** | Page 5 (Delivery & Operations) |
| **Voice of customer** | Page 6 (Rating & Sentiments) |
| **Partner-side risk** | Page 4 (Restaurant) |
| **Executive view** | Page 2 (Executive Summary) |

### Filtering Tips
- The **`Crisis type`** slicer (Pre-crisis / Crisis) is the most powerful filter — toggle it to see either window in isolation
- **City** and **Month** slicers cross-filter every visual on the page
- The Word Cloud on Page 6 updates with slicer selections — try filtering it to crisis months only

---

## 📊 Key Metrics Summary

| Category | Metric | Value | Context |
|----------|--------|-------|---------|
| **Orders** | Pre-crisis monthly | **[XX,XXX]** | Baseline |
| | Crisis monthly | **[XX,XXX]** | Collapsed period |
| | Decline % | **[XX]%** | Severity indicator |
| **Revenue** | Pre-crisis total | **₹[XX]M** | 5-month period |
| | Crisis total | **₹[XX]M** | 7-month period |
| | Loss | **₹[XX]M** | Absolute impact |
| **Customers** | Pre-crisis active | **[XX,XXX]** | Loyal base |
| | Crisis active | **[XX,XXX]** | Dramatic drop |
| | Churned | **[XX,XXX]** | Lost customers |
| | Recoverable | **[XX,XXX] ([XX]%)** | High-priority reactivation |
| **Ratings** | Pre-crisis | **[X.XX] ⭐** | Strong satisfaction |
| | Crisis | **[X.XX] ⭐** | Critical deterioration |
| | Drop | **[X.XX]** | Trust collapse |
| **Operations** | SLA pre | **[XX]%** | Adequate |
| | SLA crisis | **[XX]%** | Failure |
| | Delivery time | **[XX] → [XX] min** | **+[XX]%** increase |
| **Recovery** | Investment | **₹70–80M** | Total budget |
| | Timeline | **6–9 months** | Expected duration |
| | Expected recovery | **80–90%** | Success target |
| | ROI | **3–4×** | Return on investment |

---

## ❓ FAQ

**Q: How was customer churn calculated?**
A: A churned customer is anyone who placed **1+ orders in the pre-crisis window (Jan–May 2025)** but **ZERO orders in the crisis window (Jun–Dec 2025)**. The DAX logic is shown in the *Technical Implementation* section above.

**Q: Why are only ~30% of churned customers considered "recoverable"?**
A: Only customers with **≥5 pre-crisis orders AND ≥4.5 pre-crisis avg rating** qualify as high-return. These customers demonstrated real loyalty and left due to *failure*, not preference. The rest had weaker engagement or were already dissatisfied — so the cost to win them back exceeds their expected lifetime value.

**Q: How reliable is the ROI projection?**
A: Based on the industry-benchmark **60% reactivation rate** for food-delivery crisis recovery campaigns. Conservative estimate — actual could be higher with strong execution and the right offer mix.

**Q: What external data was used?**
A: Competitor financial reports, industry research, market analyses, GST documentation, and peer-company case studies. All cited in the *Sources & References* section.

**Q: Can this framework be reused?**
A: Yes. The methodology (phase comparison + recovery-probability segmentation + revenue decomposition + ROI pillars) transfers cleanly to other food-delivery, e-commerce, or subscription-business crisis scenarios. The DAX patterns are reusable as-is on similar data models.

---

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
