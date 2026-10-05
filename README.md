# Customer Churn Dashboard in Power BI

An interactive Power BI dashboard built to analyze customer churn for a telecommunications company.

## Project Overview

This project is an end-to-end customer churn analysis built in Power BI.

The objective is to identify the main drivers of customer churn and present the findings through an interactive dashboard that can be used by a retention manager for decision-making.

The project focuses on:

* Data cleaning and transformation in Power Query
* Data type management
* Customer segmentation
* DAX measures and filter context
* Interactive dashboard design
* Churn analysis and retention recommendations

## Dataset

**Dataset:** Telco Customer Churn

**Source:** Kaggle — Telco Customer Churn dataset

The dataset contains:

* **7,043 customers**
* **21 columns**

The original dataset was imported directly into Power BI. Data cleaning and transformation were performed in Power Query rather than in Python or Excel.

## Tools & Technologies

* Power BI Desktop
* Power Query
* DAX
* GitHub

## Power Query

The following transformations were performed in Power Query:

* Assigned explicit data types to the columns
* Converted `TotalCharges` from text to numeric
* Handled blank `TotalCharges` values for customers with zero tenure
* Created `TenureBand`
* Created `ChargeBand`
* Created numeric `ChurnFlag`
* Kept transformation steps in a logical order

## DAX Measures

The dashboard uses explicit DAX measures for:

* Total Customers
* Churned Customers
* Churn Rate %
* Average Monthly Charges
* Monthly Revenue at Risk

`DIVIDE()` is used for the churn rate calculation to safely handle a zero denominator.

## Dashboard

The dashboard includes:

* Total Customers KPI
* Churn Rate % KPI
* Monthly Revenue at Risk KPI
* Average Monthly Charges KPI
* Churn Rate % by Contract
* Churn Rate % by InternetService
* Churn Rate % by TenureBand
* Churn Rate % by PaymentMethod
* Contract slicer
* InternetService slicer
* TenureBand slicer

The dashboard is interactive, with slicers and visual interactions affecting the report dynamically.

## Key Findings

The overall churn rate is approximately **26.5%**.

Important churn patterns include:

| Segment                 | Churn Rate |
| ----------------------- | ---------: |
| Month-to-month contract |     ~42.7% |
| Fiber optic             |     ~41.9% |
| Electronic check        |     ~45.3% |
| 0-12 months tenure      |     ~47.7% |

Monthly revenue at risk is approximately **$139K**.

The analysis indicates that customers combining **month-to-month contracts, fiber optic internet, and electronic check payment** represent a particularly high-risk profile.

Segment size is considered alongside churn rate when identifying priority segments, since a very high churn rate in a very small customer group may not represent a meaningful business opportunity.

## Retention Recommendations

1. **Target month-to-month customers** with incentives to move to longer-term contracts, especially in high-risk segments.

2. **Investigate fiber optic churn** by reviewing service quality, pricing, onboarding, and customer support issues.

3. **Strengthen early-tenure retention** through improved onboarding and proactive engagement during the first 12 months.

## Bonus Features

The project may also include:

* Tooltip page
* Conditional formatting for high churn rates
* Contract × InternetService churn matrix
* What-if parameter for estimated revenue saved
* Power BI Service publication

## Deliverables

* `churn_dashboard.pbix` — Power BI report
* `dashboard.png` — main dashboard screenshot
* `dashboard_month_to_month.png` — dashboard with a slicer applied
* `note.md` — Power Query decisions, DAX definitions, analysis, and recommendations
