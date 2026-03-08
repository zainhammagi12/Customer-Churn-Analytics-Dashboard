# Customer Churn Analytics Dashboard

> Power BI · Power Query · Real-World Dataset · End-to-End Analytics

A fully interactive Power BI dashboard analysing customer churn behaviour, built on a real-world dataset and cleaned end-to-end using Power Query. Designed to give a retention team clear, actionable visibility into where churn is concentrated and why.

---

## Dashboard Preview

![Dashboard Overview](screenshots/01_overview_page.png)

---

## Problem Statement

Customer churn is one of the most costly and preventable problems in subscription and service businesses. This project answers three core business questions:

1. What is the overall churn rate and how has it changed over time?
2. Which customer segments are churning at the highest rate?
3. What are the key drivers of churn and where should retention efforts focus?

---

## Dashboard Pages

### Overview
High-level KPIs: overall churn rate, total customers, churned customers, and retained customers. Designed as an executive summary page for quick status checks.

![Overview](screenshots/01_overview_page.png)

### Churn by Segment
Breakdown of churn rate across key customer segments. Identifies the highest-risk groups to prioritise for retention campaigns.

![Churn by Segment](screenshots/02_churn_by_segment.png)

### Retention Trends
Time-series view of churn and retention rates over the available period. Highlights seasonal patterns and inflection points.

![Retention Trends](screenshots/03_retention_trends.png)

### Customer Demographics
Customer profile breakdown showing how churn varies across demographic dimensions.

![Demographics](screenshots/04_demographics.png)

### Revenue Impact
Financial impact of churn — estimated revenue at risk and retained revenue by segment.

![Revenue Impact](screenshots/05_revenue_impact.png)

---

## Key Findings

- Overall churn rate: **[X]%** — add your figure here
- Highest churn segment: **[segment name]** at **[X]%**
- Lowest churn segment: **[segment name]** at **[X]%**
- Primary churn driver: **[finding]** — add your insight here
- Estimated monthly revenue at risk: **[figure]** — if tracked

*(Update these with your actual figures from the dashboard)*

---

## Data Preparation — Power Query

The raw dataset was cleaned entirely within Power BI using Power Query before modelling. Steps applied:

**Data Cleaning**
- Removed duplicate customer records
- Handled missing values across key fields (imputation or exclusion depending on column)
- Standardised categorical fields (consistent casing, removed trailing whitespace)
- Corrected data type assignments (dates, numerics, booleans)

**Feature Engineering**
- Created tenure band column (0–6 months, 6–12 months, 1–2 years, 2 years+)
- Created churn flag as a calculated boolean column
- Built segment groupings for analysis

**Data Model**
- Fact table: customer transactions / events
- Dimension tables: customer demographics, product/contract details
- Relationships configured as star schema for clean DAX calculation

---

## Key DAX Measures

```dax
-- Churn Rate
Churn Rate = 
DIVIDE(
    COUNTROWS(FILTER(Customers, Customers[Churned] = "Yes")),
    COUNTROWS(Customers),
    0
)

-- Retained Customers
Retained Customers = 
COUNTROWS(FILTER(Customers, Customers[Churned] = "No"))

-- Churn Rate by Segment
Churn Rate Segment = 
DIVIDE(
    CALCULATE(COUNTROWS(Customers), Customers[Churned] = "Yes"),
    CALCULATE(COUNTROWS(Customers)),
    0
)
```

*(See `docs/dax_measures.md` for full measure documentation)*

---

## Project Structure

```
Customer-Churn-Analytics-Dashboard/
│
├── README.md
│
├── dashboard/
│   └── Customer_Churn_Dashboard.pbix
│
├── data/
│   ├── raw/
│   │   └── churn_data_raw.csv
│   └── processed/
│       └── churn_data_cleaned.csv
│
├── screenshots/
│   ├── 01_overview_page.png
│   ├── 02_churn_by_segment.png
│   ├── 03_retention_trends.png
│   ├── 04_demographics.png
│   └── 05_revenue_impact.png
│
├── docs/
│   ├── data_dictionary.md
│   └── dax_measures.md
│
└── requirements.txt
```

---

## How to Open

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Clone this repository
```bash
git clone https://github.com/zainhammagi12/Customer-Churn-Analytics-Dashboard
```
3. Open `dashboard/Customer_Churn_Dashboard.pbix` in Power BI Desktop
4. If prompted about data source paths, update to point to `data/processed/churn_data_cleaned.csv`

---

## Tools Used

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power_Query-217346?style=flat&logo=microsoft&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat&logo=microsoftazure&logoColor=white)

- Power BI Desktop
- Power Query (M language — data cleaning and transformation)
- DAX (measures and calculated columns)

---

## Business Recommendations

Based on the dashboard findings:

1. **Priority retention segment:** Focus outreach on [highest churn segment] — this group represents the highest revenue risk
2. **Early intervention:** Customers in the 0–6 month tenure band show elevated churn — a proactive onboarding programme could reduce early dropout
3. **Contract incentives:** [Contract type with highest churn] customers churn at significantly higher rates — targeted upgrade offers may improve retention
4. **Self-service improvements:** [Add insight based on your data]

*(Update these with your actual findings)*

---

## Author

**Zain Hammagi** — [linkedin.com/in/zain-hammagi](https://linkedin.com/in/zain-hammagi) · [zainhammagi.github.io](https://zainhammagi.github.io)
