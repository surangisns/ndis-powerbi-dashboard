# 📊 NDIS Participant, Budget, Utilisation & Plan Management Insights Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft&logoColor=white)
![NDIS](https://img.shields.io/badge/Sector-NDIS%20%2F%20Disability-6A0DAD?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

> A 7-page interactive Power BI dashboard analysing 1.78 million rows of public NDIS data across 5 quarters (March 2025 – March 2026), surfacing trends in participant growth, plan budgets, support utilisation, and plan management types.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dashboard Pages](#dashboard-pages)
- [Data Sources](#data-sources)
- [Technical Implementation](#technical-implementation)
- [Key Insights](#key-insights)
- [Screenshots](#screenshots)
- [How to View](#how-to-view)
- [Folder Structure](#folder-structure)
- [Data Disclaimer](#data-disclaimer)
- [About the Author](#about-the-author)

---

## 🔍 Project Overview

The **National Disability Insurance Scheme (NDIS)** is one of Australia's largest social policy programs, supporting hundreds of thousands of Australians with permanent and significant disability. The NDIS Authority (NDIA) releases quarterly public datasets that provide transparency into scheme performance — but these datasets require significant transformation and analytical effort to extract meaningful insights.

This project transforms raw NDIA public data into a fully interactive, executive-ready Power BI dashboard designed for:

- **Scheme analysts and planners** tracking participant growth and budget trends
- **Plan managers and support coordinators** benchmarking utilisation patterns
- **Policy and strategy teams** monitoring quarter-on-quarter shifts in plan management types
- **Data professionals** demonstrating applied analytics in a complex government dataset context

| Metric | Detail |
|---|---|
| **Dashboard Pages** | 7 |
| **Data Rows** | 1,780,000+ |
| **Datasets** | 4 |
| **Time Period** | March 2025 – March 2026 (5 quarters) |
| **Data Source** | NDIA Public Quarterly Reports |
| **Tool** | Microsoft Power BI Desktop |
| **Skills** | DAX, Power Query (M), Data Modelling, UX Design |

---

## 📑 Dashboard Pages

### Page 1 — Executive Summary
High-level KPI overview across all quarters. Headline metrics include total active participants, total approved plan budgets, average plan value, and scheme-wide utilisation rate. Designed for senior stakeholder consumption with drill-through capability to supporting pages.

### Page 2 — Participant Overview
Demographic breakdown of active NDIS participants including age group distribution, primary disability category, state/territory coverage, and quarter-on-quarter participant growth. Includes trend sparklines and YOY comparison visuals.

### Page 3 — Budget Analysis
Approved plan budget analysis segmented by support category (Core, Capital, Capacity Building), state, and participant cohort. Highlights budget allocation shifts across quarters and identifies categories with the highest per-participant investment.

### Page 4 — Utilisation Insights
Deep-dive into support utilisation rates — the ratio of funds committed/spent versus approved plan budgets. Breaks down under- and over-utilisation patterns by support category, state, and plan management type, enabling identification of service delivery gaps.

### Page 5 — Plan Management Analysis
Comparative analysis of the three plan management types — **Agency Managed**, **Plan Managed**, and **Self Managed** — across participant cohorts, age groups, disability categories, and states. Tracks shifting preferences in plan management over the 5-quarter window.

### Page 6 — Geographic Insights
State and territory-level performance map showing participant volumes, average plan values, utilisation rates, and plan management mix. Includes choropleth map visualisation and ranked comparison tables.

### Page 7 — Quarterly Trends & Outlook
Time-series analysis of key metrics across all 5 quarters. Visualises growth trajectories, utilisation trends, and budget movement. Supports data-driven forecasting conversations for planning teams.

---

## 🗂️ Data Sources

All data used in this project is **publicly available** and sourced from the official NDIA Quarterly Report publications.

| Dataset | Description | Rows (approx.) |
|---|---|---|
| Participant Data | Active participants by demographics, disability, and state | ~450,000 |
| Plan Budget Data | Approved, committed, and managed budget amounts by support category | ~480,000 |
| Utilisation Data | Support utilisation rates by category, state, and plan type | ~420,000 |
| Plan Management Data | Plan management type breakdown by participant cohort and quarter | ~430,000 |

**Quarters covered:**
- Q3 FY2025 — March 2025
- Q4 FY2025 — June 2025
- Q1 FY2026 — September 2025
- Q2 FY2026 — December 2025
- Q3 FY2026 — March 2026

📎 Source: [NDIS Quarterly Reports — data.ndis.gov.au](https://data.ndis.gov.au)

---

## ⚙️ Technical Implementation

### Data Transformation — Power Query (M)
- Ingested 4 separate quarterly CSV datasets and appended across 5 quarters into unified fact tables
- Applied consistent column naming, data type enforcement, and null handling across all datasets
- Built a custom **Date Dimension Table** in Power Query to support time intelligence functions
- Normalised inconsistent state/territory codes and disability category labels across quarterly files
- Created conditional columns for age groupings, utilisation bands, and plan management flags

### Data Modelling
- Implemented a **star schema** with central fact tables and supporting dimension tables (Date, Geography, Support Category, Plan Type)
- Established one-to-many relationships with correct cross-filter directions to prevent ambiguous results
- Separated measures into a dedicated **_Measures Table** for clean model organisation

### DAX Measures (selected highlights)

```dax
-- Utilisation Rate %
Utilisation Rate % = 
DIVIDE(
    SUM(FactBudget[CommittedAmount]),
    SUM(FactBudget[ApprovedAmount]),
    0
)

-- Quarter-on-Quarter Participant Growth %
QoQ Participant Growth % = 
VAR CurrentQ = [Total Active Participants]
VAR PreviousQ = CALCULATE(
    [Total Active Participants],
    DATEADD('Date'[Date], -1, QUARTER)
)
RETURN DIVIDE(CurrentQ - PreviousQ, PreviousQ, BLANK())

-- Average Plan Value
Avg Plan Value = 
DIVIDE(
    SUM(FactBudget[ApprovedAmount]),
    DISTINCTCOUNT(FactParticipant[ParticipantID]),
    0
)

-- Plan Managed % Share
Plan Managed % = 
DIVIDE(
    CALCULATE([Total Active Participants], FactPlanMgmt[PlanType] = "Plan Managed"),
    [Total Active Participants],
    0
)
```

### Design Principles
- Consistent NDIS-aligned colour palette with accessibility contrast compliance
- Bookmarks used for toggle navigation between views on select pages
- Slicers synced across pages for seamless cross-filtering by quarter, state, and support category
- Tooltips customised with supplementary context on key visuals

---

## 💡 Key Insights

> *Specific figures to be updated with published values before sharing publicly.*

- **Participant growth** remained steady across all 5 quarters, with the strongest intake observed in [state] among the [age group] cohort
- **Utilisation rates** for Core Supports consistently outperformed Capital and Capacity Building supports, suggesting ongoing challenges in accessing funded supports in those categories
- **Plan Managed** participants grew as a proportion of the scheme over the period, while **Agency Managed** share declined — reflecting a broader shift in participant choice and control
- **Average plan values** were highest in the [disability category] cohort and lowest in [cohort], with significant state-level variation
- Quarter-on-quarter budget growth outpaced participant growth in several quarters, indicating rising **per-participant investment**

---

## 🖼️ Screenshots

> *Add dashboard screenshots here before publishing. Recommended: one image per page, plus a model diagram.*

| Page | Preview |
|---|---|
| Executive Summary | `screenshots/01_executive_summary.png` |
| Participant Overview | `screenshots/02_participant_overview.png` |
| Budget Analysis | `screenshots/03_budget_analysis.png` |
| Utilisation Insights | `screenshots/04_utilisation_insights.png` |
| Plan Management | `screenshots/05_plan_management.png` |
| Geographic Insights | `screenshots/06_geographic_insights.png` |
| Quarterly Trends | `screenshots/07_quarterly_trends.png` |

---

## 👁️ How to View

### Option A — Power BI Service (Recommended)
View the published dashboard directly in browser — no software required:
🔗 [View Live Dashboard](#) *(link to be added after publishing to Power BI Service)*

### Option B — Power BI Desktop
1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Clone or download this repository
3. Open `NDIS_Dashboard.pbix`
4. Data is embedded — no external connections required

### Option C — PDF Export
A static PDF export of all 7 pages is available in the `/exports` folder for quick viewing without any software.

---

## 📁 Folder Structure

```
ndis-powerbi-dashboard/
│
├── NDIS_Dashboard.pbix          # Main Power BI file
│
├── data/
│   ├── raw/                     # Original NDIA CSV downloads
│   └── processed/               # Cleaned/appended datasets (optional)
│
├── screenshots/                 # Dashboard page screenshots
│   ├── 01_executive_summary.png
│   ├── 02_participant_overview.png
│   └── ...
│
├── exports/
│   └── NDIS_Dashboard_Export.pdf
│
├── docs/
│   └── data_dictionary.md       # Column definitions and transformations
│
└── README.md
```

---

## ⚠️ Data Disclaimer

This dashboard uses **publicly available data** published by the National Disability Insurance Agency (NDIA). All data has been used in accordance with the NDIA's open data licensing terms. No personally identifiable information (PII) is included in any dataset. This project is independent and not affiliated with or endorsed by the NDIA or Australian Government.

---

## 👩‍💻 About the Author

**Surangani Bandara**
*Insights & Reporting Analyst — Forever Cornerstone*

An analyst working at the intersection of data and disability services, with hands-on experience translating complex NDIS scheme data into actionable insights for operational and strategic decision-making.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/[your-profile])
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-181717?style=flat&logo=github)](https://github.com/[your-handle])

---

*Built with Microsoft Power BI · DAX · Power Query · Public NDIS Data*

