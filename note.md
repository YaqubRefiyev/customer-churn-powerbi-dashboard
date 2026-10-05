# Customer Churn Dashboard — Project Notes

## 1. Project Overview

This project analyzes customer churn for a telecom company using Power BI.

The dataset contains 7,043 customers and 21 columns.

**Tool used:** Power BI Desktop on Windows

**Dataset:** Telco Customer Churn dataset from Kaggle.

---

## 2. Power Query Decisions

All data cleaning and transformation were performed in Power Query. No preprocessing was done in Python or Excel.

### TotalCharges

`TotalCharges` was initially imported as a text column.

There were 11 customers with `tenure = 0` and blank `TotalCharges` values. These blanks were replaced with `0`, because these customers had no recorded tenure and therefore no accumulated total charges.

The column was then converted to a numeric/decimal data type.

### Data Types

Explicit data types were assigned to the dataset columns according to their meaning, including:

* Text columns → Text
* Customer tenure → Whole Number
* MonthlyCharges → Decimal Number
* TotalCharges → Decimal Number
* ChurnFlag → Whole Number

### TenureBand

A calculated column was created to group customers by tenure:

* 0-12 months
* 13-24 months
* 25-48 months
* 49+ months

### ChargeBand

A calculated column was created by grouping `MonthlyCharges` into quartile-based bands.

### ChurnFlag

A numeric churn indicator was created:

* Yes → 1
* No → 0

The Applied Steps in Power Query were kept in a logical order and named clearly.

---

## 3. DAX Measures

The dashboard uses explicit DAX measures rather than implicit visual aggregations.

### Total Customers

```DAX
Total Customers =
COUNTROWS('WA_Fn-UseC_-Telco-Customer-Churn')
```

### Churned Customers

```DAX
Churned Customers =
CALCULATE(
    [Total Customers],
    'WA_Fn-UseC_-Telco-Customer-Churn'[Churn] = "Yes"
)
```

### Churn Rate %

```DAX
Churn Rate % =
DIVIDE(
    [Churned Customers],
    [Total Customers]
)
```

`DIVIDE` is used instead of the `/` operator so that a zero denominator returns a blank rather than producing a division-by-zero error.

### Average Monthly Charges

```DAX
Avg Monthly Charges =
AVERAGE(
    'WA_Fn-UseC_-Telco-Customer-Churn'[MonthlyCharges]
)
```

### Monthly Revenue at Risk

```DAX
Monthly Revenue at Risk =
CALCULATE(
    SUM(
        'WA_Fn-UseC_-Telco-Customer-Churn'[MonthlyCharges]
    ),
    'WA_Fn-UseC_-Telco-Customer-Churn'[Churn] = "Yes"
)
```

---

## 4. Dashboard

The report contains:

* KPI cards for Total Customers, Churn Rate %, Monthly Revenue at Risk, and Average Monthly Charges
* Churn Rate % by Contract
* Churn Rate % by InternetService
* Churn Rate % by TenureBand
* Churn Rate % by PaymentMethod
* Contract slicer
* InternetService slicer
* TenureBand slicer

The slicers and visual interactions allow the dashboard to be filtered dynamically.

---

## 5. Key Findings

The overall customer churn rate is approximately **26.5%**.

The highest-risk patterns include:

* Month-to-month contracts: approximately **42.7% churn**
* Fiber optic customers: approximately **41.9% churn**
* Electronic check payment method: approximately **45.3% churn**
* Customers with 0-12 months of tenure: approximately **47.7% churn**

Monthly revenue at risk is approximately **$139K**.

The combination of **month-to-month contracts, fiber optic internet, and electronic check payment** represents a particularly high-risk customer profile.

When identifying priority segments, both churn rate and customer volume should be considered. A very high churn rate in a segment with only a few customers is less actionable than a high churn rate affecting a substantial customer population.

---

## 6. Retention Recommendations

### 1. Target month-to-month customers

Prioritize month-to-month customers with targeted incentives to move to one-year or two-year contracts, particularly where churn risk is high.

### 2. Investigate fiber optic churn

Analyze service quality, onboarding, pricing, and support issues among fiber optic customers and introduce targeted retention interventions.

### 3. Focus on early-tenure customers

Strengthen onboarding and early-life customer engagement during the first 12 months, when churn is particularly high.

---

## 7. Deliverables

The repository contains:

* `churn_dashboard.pbix` — Power BI report
* `dashboard.png` — main dashboard screenshot
* `dashboard_month_to_month.png` — dashboard with a slicer applied