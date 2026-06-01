# Portfolio Case Study
## NDIS Participant, Budget, Utilisation & Plan Management Insights Dashboard

**Author:** Surangani Bandara
**Role:** Insights & Reporting Analyst 
**Tool:** Microsoft Power BI (DAX · Power Query)
**Project Type:** Independent Portfolio Project
**Data:** Public NDIS Quarterly Data | 5 Quarters | 1.78M Rows | 4 Datasets

---

## Executive Summary

This project demonstrates end-to-end analytical capability across data acquisition, transformation, modelling, DAX development, and dashboard design — applied to one of Australia's most complex and data-rich social policy programs: the **National Disability Insurance Scheme (NDIS)**.

The output is a 7-page interactive Power BI dashboard that enables stakeholders to explore participant demographics, plan budgets, support utilisation patterns, and plan management trends across five consecutive quarters of public NDIA data (March 2025 to March 2026). The dashboard is designed to the standard expected in a real operational analytics environment — structured for both senior executive consumption and granular operational analysis.

---

## Background & Problem Context

The NDIS supports over 600,000 Australians with permanent and significant disability through individually tailored funding plans. The NDIA publishes quarterly public datasets that document scheme performance — but in raw form, these files present significant analytical challenges:

- Data is distributed across multiple separate CSV files per quarter
- Column naming, coding, and formatting conventions shift across quarterly releases
- No pre-built analytical layer exists for multi-quarter trend analysis
- The datasets collectively run into millions of rows requiring robust transformation before any insight is possible

For analysts and organisations operating in the disability sector, the ability to work with this data fluently is a critical capability — both for internal reporting and for understanding the broader scheme context in which their participants sit.

---

## Project Objectives

This project was designed to achieve the following outcomes:

1. **Demonstrate technical depth** — Show applied capability across the full Power BI stack: Power Query transformation, star schema data modelling, and advanced DAX
2. **Produce sector-relevant insights** — Surface findings that would be genuinely meaningful to NDIS sector professionals, not just generic analytics outputs
3. **Build a recruiter-ready portfolio asset** — Create a publishable, professional-grade artefact that reflects the work quality expected in mid-to-senior analytics roles in government, health, and disability services
4. **Validate real-world data skills** — Work with genuinely messy, large-scale public data rather than a pre-cleaned teaching dataset

---

## Data Scope & Sources

| Dataset | Description | Volume |
|---|---|---|
| Participant Data | Demographics, disability categories, age groups, state/territory | ~450K rows |
| Plan Budget Data | Approved, committed, and managed support budgets by category | ~480K rows |
| Utilisation Data | Utilisation rates across support categories and plan types | ~420K rows |
| Plan Management Data | Plan management type breakdown by cohort and quarter | ~430K rows |
| **Total** | | **~1.78M rows** |

**Quarterly Coverage:**
- March 2025 (Q3 FY2025)
- June 2025 (Q4 FY2025)
- September 2025 (Q1 FY2026)
- December 2025 (Q2 FY2026)
- March 2026 (Q3 FY2026)

All data sourced from [data.ndis.gov.au](https://data.ndis.gov.au) under NDIA open data licensing.

---

## Methodology

### Phase 1 — Data Acquisition & Assessment
Downloaded all relevant quarterly files from the NDIA public data portal. Conducted an initial assessment of each file for structure, column consistency, null rates, and data type issues. Identified key transformation requirements before writing a single line of M code.

### Phase 2 — Power Query Transformation
Built a structured transformation pipeline in Power Query:

- **Append queries** to stack 5 quarters of each dataset into unified fact tables, with a `QuarterLabel` column added at source for time-based filtering
- **Standardised column naming** across quarterly files where headers had shifted between releases
- **Data type enforcement** — explicitly set types on all columns to prevent silent type coercion errors downstream
- **Null and blank handling** — replaced nulls in key categorical fields with "Not Specified" to prevent filter gaps in visuals
- **Normalisation** — resolved inconsistent state codes (e.g., `NSW`, `New South Wales`, `N.S.W.`) into a single consistent label set
- **Conditional columns** — created derived groupings for age bands, utilisation performance bands (e.g., Under 50%, 50–80%, 80%+, Over 100%), and plan type flags
- **Date Dimension** — built a fully structured date table in Power Query covering the full analysis period, with quarter, financial year, and calendar year columns

### Phase 3 — Data Modelling
Implemented a **star schema** to ensure clean, performant DAX evaluation:

- Central fact tables: `FactParticipant`, `FactBudget`, `FactUtilisation`, `FactPlanManagement`
- Shared dimension tables: `DimDate`, `DimGeography`, `DimSupportCategory`, `DimPlanType`, `DimDisabilityCategory`
- One-to-many relationships from dimensions to facts
- Cross-filter directions set deliberately to avoid measure ambiguity
- All DAX measures isolated in a dedicated `_Measures` table (non-data table) for clean model navigation

### Phase 4 — DAX Development
Wrote a library of DAX measures ranging from foundational aggregations to time intelligence and ratio calculations. Key measure categories:

**Participant Metrics**
- Total Active Participants
- QoQ Participant Growth (absolute and %)
- New Participants this Quarter

**Budget Metrics**
- Total Approved Plan Budget
- Average Plan Value per Participant
- Budget Growth QoQ %
- Budget by Support Category (Core / Capital / Capacity Building)

**Utilisation Metrics**
- Utilisation Rate % = `DIVIDE([Committed Amount], [Approved Amount])`
- Utilisation Band classification via `SWITCH` logic
- Under-utilisation Flag (participants with <50% utilisation)

**Plan Management Metrics**
- Agency Managed %, Plan Managed %, Self Managed %
- Plan Management shift QoQ (using `DATEADD` or `CALCULATE` + filter context)

**Time Intelligence**
- SAMEPERIODLASTYEAR comparisons
- Rolling 3-quarter averages
- Quarter-to-date measures using `DATESQTD`

### Phase 5 — Dashboard Design & UX
Built 7 dashboard pages with deliberate attention to information hierarchy and analytical flow:

- **Page 1 (Executive Summary)** — designed for senior stakeholders: KPI cards, headline trends, scheme-wide utilisation rate, drill-through enabled
- **Pages 2–6** — progressively deeper analytical layers, each with a defined analytical question it answers
- **Page 7 (Trends & Outlook)** — time series and QoQ comparison layer for forecasting conversations

Design decisions:
- NDIS brand colour palette applied consistently across all pages
- Bookmarks used for view toggles (e.g., table vs chart view on select pages)
- Slicers synced across relevant page groups to allow seamless cross-page filtering
- Custom tooltips on key visuals to provide supplementary context without cluttering the canvas
- Report theme JSON configured to ensure consistent font, colour, and grid settings

---

## Key Findings & Insights

> *Note: These findings are representative of the analytical framework applied. Specific figures to be confirmed against published values prior to public sharing.*

### Participant Growth
Participant numbers grew consistently across all five quarters, with the strongest single-quarter intake observed in [specific quarter]. Growth was disproportionately concentrated in [age group] and [disability category], consistent with broader NDIS access pathway trends.

### Support Utilisation
Core Supports maintained the highest utilisation rates across all cohorts — typically tracking above 80% scheme-wide. Capital Supports and Capacity Building Supports showed persistently lower utilisation, particularly in [states/territories], suggesting ongoing service availability or participant engagement challenges in those categories.

### Plan Management Trends
The proportion of Plan Managed participants increased quarter-on-quarter throughout the analysis period, while Agency Managed participation declined as a share of the scheme. This reflects a sustained trend toward greater participant choice and control — with implications for plan management organisations regarding market opportunity and competitive positioning.

### Geographic Variation
Significant variation in average plan values and utilisation rates exists across states and territories. [State] recorded the highest average plan value; [state] recorded the lowest utilisation rate. These disparities point to structural differences in service availability, access, and participant need profiles across jurisdictions.

### Budget Growth vs Participant Growth
In [quarter(s)], approved plan budget growth outpaced participant growth — indicating rising average plan values rather than purely volume-driven scheme expansion. This has implications for scheme sustainability modelling and actuarial forecasting.

---

## Technical Challenges & Solutions

| Challenge | Solution Applied |
|---|---|
| Column headers shifted between quarterly releases | Applied consistent renaming steps in Power Query at the append stage using conditional column logic |
| Inconsistent state/territory coding across files | Created a standardisation lookup table applied via a merge step in Power Query |
| Slow DAX refresh on large dataset | Optimised measure calculation by moving filter logic into variables (`VAR`) and reducing unnecessary `CALCULATE` nesting |
| Preventing double-counting across appended quarters | Added `QuarterLabel` as a filter-safe column and validated row counts at each transformation step |
| Ambiguous cross-filter paths in model | Resolved by setting explicit single-direction cross-filters and using `CROSSFILTER` in DAX where bidirectional behaviour was required for specific measures |

---

## Skills Demonstrated

| Skill Area | Specific Application |
|---|---|
| **Power Query / M** | Multi-source append, data type enforcement, conditional columns, custom date table, lookup merges, null handling |
| **DAX** | Time intelligence, ratio measures, SWITCH classification, CALCULATE with complex filter context, VAR optimisation |
| **Data Modelling** | Star schema design, relationship management, cross-filter direction decisions, dedicated measures table |
| **Dashboard Design** | Multi-page layout, bookmark navigation, synced slicers, custom tooltips, theme configuration |
| **Domain Knowledge** | NDIS support categories, plan management types, utilisation concepts, scheme funding structure |
| **Data Quality** | Multi-source reconciliation, row count validation, transformation auditability |

---

## Business Value

This dashboard — if deployed in a real organisational context — would enable:

- **Plan management organisations** to benchmark their participant cohort's utilisation against the broader scheme
- **Support coordinators** to identify clients at risk of under-utilisation before plan review dates
- **Strategy teams** to monitor scheme-level trends that affect service demand forecasting
- **Executive leadership** to track KPIs relevant to NDIS Quality and Safeguarding compliance reporting
- **Policy analysts** to assess the impact of NDIS pricing changes or access decisions on budget and utilisation trends

---

## Reflections & Next Steps

**What went well:**
- The star schema modelling decision paid dividends throughout DAX development — measure logic remained clean and performant even at 1.78M rows
- Working with real, messy public data significantly strengthened the value of this project as a portfolio piece versus using a clean teaching dataset

**What I would do differently:**
- Introduce a dedicated data dictionary document earlier in the project to track transformation decisions as they were made
- Parameterise the data source file paths in Power Query to make quarterly data refresh a one-click operation

**Potential enhancements:**
- Integrate NDIS Pricing Arrangements data to add a cost-per-unit analytical layer
- Add a What-If parameter for utilisation rate scenario modelling
- Publish to Power BI Service with row-level security (RLS) configured for a multi-organisation demo scenario

---

## About the Author

**Surangani Bandara** is an Insights & Reporting Analyst at **Forever Cornerstone**, working in the disability support sector. She builds data products that translate complex NDIS operational and scheme data into decision-ready insights for both internal teams and external stakeholders.

This project was completed as an independent portfolio initiative to demonstrate applied analytics capability in a domain-relevant context.

🔗 [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/surangani-data-analyst/)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-181717?style=flat&logo=github)](https://github.com/surangisns) | [LinkedIn](https://www.linkedin.com/in/surangani-data-analyst/) | [GitHub](https://github.com/surangisns)

---

*© Surangani Bandara — Portfolio Project. Data sourced from NDIA public quarterly releases under open data licence.*
