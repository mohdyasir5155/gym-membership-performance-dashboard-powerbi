# Gym Membership Performance Dashboard (Power BI)

**An interactive Power BI dashboard that turns gym membership data into clear answers on member growth, retention, revenue, and branch performance, so management can decide where to act.**

| | |
|---|---|
| **Role demonstrated** | Data Analyst / BI Analyst (entry level) |
| **Core skills** | Power BI, DAX, Power Query, Data Modeling, KPI Design, Data Storytelling |
| **Domain** | Fitness and Membership Analytics |
| **Tools** | Power BI Desktop, DAX, Power Query, Git |
| **Author** | Yasir Sheikh |

> **Dashboard preview:** `![Dashboard Overview](images/cover.png`

---

## 30-Second Summary (for Recruiters)

| Question | Answer |
|---|---|
| **What problem does it solve?** | Gym management needs a fast, reliable view of memberships, retention, and revenue to decide where to focus marketing and operations. |
| **What did I build?** | A multi-page Power BI dashboard with KPI cards, trend analysis, segment breakdowns, and interactive filters. |
| **What can it answer?** | How many members are active, who is churning, which plans and branches perform best, and how revenue trends over time. |
| **What does it prove about me?** | I can clean data, build a data model, write DAX, and present insights visually in a way that supports business decisions. |

---

## Table of Contents

1. [Business Problem](#business-problem)
2. [Objectives](#objectives)
3. [Dataset](#dataset)
4. [Key Insights and Recommendations](#key-insights-and-recommendations)
5. [Dashboard Pages](#dashboard-pages)
6. [KPIs and Metrics](#kpis-and-metrics)
7. [Data Preparation](#data-preparation)
8. [Data Model](#data-model)
9. [DAX Measures](#dax-measures)
10. [Design Decisions](#design-decisions)
11. [Skills Demonstrated](#skills-demonstrated)
12. [Repository Structure](#repository-structure)
13. [How to Use](#how-to-use)
14. [Future Improvements](#future-improvements)
15. [About the Author](#about-the-author)

---

## Business Problem

A gym business collects large amounts of member data but lacks a single view of how it is performing.

| Challenge | Business Impact |
|---|---|
| Membership data is hard to summarize quickly | Slow decisions on pricing and promotions |
| Retention and churn are not tracked clearly | Revenue loss goes unnoticed |
| No comparison across plans, branches, or segments | Resources are not directed where they matter most |
| Reporting is manual and static | Time spent preparing reports instead of acting on them |

---

## Objectives

| # | Objective | Outcome |
|---|---|---|
| 1 | Track membership size and growth | Active, new, and cancelled member KPIs |
| 2 | Measure retention and churn | Retention and churn rate with trends |
| 3 | Understand revenue drivers | Revenue by plan, segment, and period |
| 4 | Compare performance | Branch, plan, and demographic comparisons |
| 5 | Support decisions | Insights and recommendations for management |

---

## Dataset

| Attribute | Details |
|---|---|
| Source | [add source, e.g., Kaggle / challenge dataset / simulated data] |
| Records | [X,XXX] members |
| Time period | [start date] to [end date] |
| Key fields | [e.g., member ID, join date, plan type, age, gender, branch, visits, monthly fee, status] |

---

## Key Insights and Recommendations

> Replace the bracketed values with your real findings. This is the most important section for a hiring manager. Specific numbers show you can find and communicate insight, not only build charts.

| # | Insight | Evidence | Recommended Action |
|---|---|---|---|
| 1 | [e.g., Churn is highest among members on Plan X] | [X% churn vs Y% average] | [e.g., Offer upgrade or loyalty incentive] |
| 2 | [e.g., Branch A leads on visits and retention] | [X visits per member vs Y] | [e.g., Use as benchmark for other branches] |
| 3 | [e.g., Most new members join in month X] | [X% of annual joins] | [e.g., Time campaigns before that window] |
| 4 | [e.g., Age group Y generates the most revenue] | [X% of total revenue] | [e.g., Target marketing at this segment] |

---

## Dashboard Pages

| Page | Purpose | Main Visuals |
|---|---|---|
| **Executive Overview** | High-level health of the business | KPI cards, membership trend, revenue trend |
| **Membership Analysis** | Who the members are and how they behave | Demographics, plan distribution, tenure |
| **Retention and Churn** | Why and where members leave | Churn rate trend, churn by segment |
| **Revenue Analysis** | Where revenue comes from | Revenue by plan, branch, and period |
| **Branch / Segment Comparison** | Relative performance | Ranked bar charts, matrix, drill-through |

> Add a screenshot for each page, for example `![Retention](images/retention_page.png)`.
> Update this table to match the pages you actually built.

---

## KPIs and Metrics

| KPI | Definition | Why It Matters |
|---|---|---|
| Total Members | Count of unique members | Size of the member base |
| Active Members | Members with an active status | Current business health |
| New Members | Members joined in the period | Growth |
| Churn Rate | Cancelled members divided by total members | Revenue risk |
| Retention Rate | 1 minus churn rate | Loyalty |
| Average Membership Duration | Mean months as a member | Customer lifetime |
| Total Revenue | Sum of membership fees | Financial performance |
| Average Revenue per Member | Revenue divided by members | Pricing effectiveness |
| Average Visits per Member | Visits divided by members | Engagement |

---

## Data Preparation

| Step | Tool | Description |
|---|---|---|
| Import | Power Query | Load raw data files |
| Clean | Power Query | Remove duplicates, fix data types, handle nulls and inconsistent text |
| Transform | Power Query | Create derived columns (age groups, tenure, join month and year) |
| Date table | DAX | Build a dedicated calendar table for time intelligence |
| Validate | Power BI | Check totals and counts against the source data |

---

## Data Model

| Table | Type | Purpose |
|---|---|---|
| `Members` (or equivalent) | Fact | Member records with plan, status, and fees |
| `Calendar` | Dimension | Date attributes for time-based analysis |
| `[Plans / Branches]` | Dimension | Descriptive attributes for slicing |

> Add your model view screenshot: `![Data Model](images/data_model.png)`
> Describe the relationships (for example, one-to-many from Calendar to Members on join date).

---

## DAX Measures

Examples of the measure types used. Replace with your actual measures.

```dax
Total Members = DISTINCTCOUNT ( Members[MemberID] )

Churn Rate =
DIVIDE (
    CALCULATE ( [Total Members], Members[Status] = "Cancelled" ),
    [Total Members]
)

Retention Rate = 1 - [Churn Rate]

Revenue MoM Change % =
VAR CurrentMonth = [Total Revenue]
VAR PreviousMonth =
    CALCULATE ( [Total Revenue], DATEADD ( 'Calendar'[Date], -1, MONTH ) )
RETURN
    DIVIDE ( CurrentMonth - PreviousMonth, PreviousMonth )
```

| Technique | Where Used |
|---|---|
| `CALCULATE` and filter context | Churn and segment-specific KPIs |
| `DIVIDE` | Safe ratio calculations |
| Time intelligence (`DATEADD`, `SAMEPERIODLASTYEAR`) | Month-over-month and year-over-year trends |
| Variables (`VAR`) | Readable, efficient measures |

---

## Design Decisions

| Decision | Reasoning |
|---|---|
| KPIs at the top of each page | Executives see the answer first, detail second |
| Consistent color palette and layout | Easier to read and more professional |
| Slicers for plan, branch, and time | Lets users explore without needing new reports |
| Drill-through to detail | Moves from "what happened" to "why" in one click |
| Dedicated date table | Enables reliable time intelligence |

---

## Skills Demonstrated

| Category | Specifics |
|---|---|
| **Power BI** | Report design, interactive visuals, slicers, drill-through, bookmarks |
| **DAX** | Measures, time intelligence, calculated columns, variables |
| **Power Query** | Data cleaning, transformation, type handling |
| **Data Modeling** | Fact and dimension tables, relationships, date table |
| **Analytics** | KPI design, retention and churn analysis, segmentation |
| **Communication** | Insight-led storytelling and actionable recommendations |

---

## Repository Structure

```
gym-membership-performance-dashboard-powerbi/
├── data/          # Dataset files
├── images/        # Dashboard and data model screenshots
├── dashboard/     # Power BI file (.pbix)
└── README.md
```

> Update the folder names to match your repository.

---



## Future Improvements

| Enhancement | Value |
|---|---|
| Connect to a live database | Automatic refresh instead of static files |
| Add member lifetime value analysis | Prioritize high-value segments |
| Predictive churn indicators | Identify at-risk members early |
| Publish to Power BI Service | Shareable link for stakeholders |

---

## About the Author

**Yasir Sheikh** is a B.Tech Computer Science and Engineering student (2023 to 2027) at G H Raisoni University, Amravati, seeking entry-level **Data Analyst / BI Analyst** roles.

| | |
|---|---|
| GitHub | [mohdyasir5155](https://github.com/mohdyasir5155) |
| LinkedIn | [add your link] |
| Email | [add your email] |
