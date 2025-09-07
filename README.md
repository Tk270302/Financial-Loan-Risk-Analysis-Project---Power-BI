# Financial Risk & Loan Analytics (Power BI)

An end-to-end **loan risk** analytics project built in **Power BI** using the **Home Credit Default Risk** dataset (Kaggle).  
The report replicates real analyst tasks: data cleaning, feature engineering, risk KPIs, segmentation, drillthrough exploration, and presentation-ready visuals.

**Live Report:** [Power BI (https://app.powerbi.com/links/HB3JwzkUl-?ctid=34c6a16f-5c98-4f1c-9e10-5b1d293bf1d4&pbi_source=linkShare)](#)  
**LinkedIn Post:** [https://www.linkedin.com/posts/talishkhan_new-power-bi-project-financial-risk-activity-7370357429106057216-qNyH?utm_source=share&utm_medium=member_desktop&rcm=ACoAAEC7ouYB3m_UDCnc_fFOISkbK99LF40bYPA](#)

---

## 🎯 Objectives
Measure portfolio risk by calculating key indicators such as Default Rate, Total Loans, and Total Exposure.

Profile borrowers across demographics and financial attributes (Age, Gender, Income Type, Education, Occupation, Credit Size, DTI).

Identify high-risk segments where default rates are significantly above average.

Enable drillthrough analysis so stakeholders can deep-dive into occupations, organizations, and credit distributions for any segment.

Support decision-making in credit risk management, customer targeting, and lending policy design through clear and interactive visuals.

Demonstrate end-to-end analyst workflow: from raw data cleaning in Power Query → calculated columns/measures in DAX → storytelling in Power BI dashboards.

---

## 🧰 Tools & Skills
- **Power BI Desktop & Service**
- **Power Query** (type fixes, anomaly cleanup, custom columns)
- **DAX** (measures, bands, sort-by columns)
- **Design** (cards, slicers, column/bar charts, scatter, drillthrough)
- **Storytelling** (KPI strip, segment breakdowns, distribution view)

---

## 📂 Dataset
- **Source:** Home Credit Default Risk (Kaggle)  
- **File used primarily:** `application_train.csv`  
- **Key fields:** `TARGET (1=default)`, `AMT_CREDIT`, `AMT_ANNUITY`, `AMT_INCOME_TOTAL`, `CODE_GENDER`,  
  `NAME_INCOME_TYPE`, `NAME_EDUCATION_TYPE`, `OCCUPATION_TYPE`, `ORGANIZATION_TYPE`, `DAYS_BIRTH`, `DAYS_EMPLOYED`.

> Kaggle: https://www.kaggle.com/competitions/home-credit-default-risk/data

---

## 🧼 Data Prep (Power Query)
- Set data types (numeric/text) and replace `DAYS_EMPLOYED=365243` with null.
- Added columns:
  - `AgeYears = floor(abs(DAYS_BIRTH)/365)`
  - `EmpYears = floor(abs(DAYS_EMPLOYED)/365, 1)`
  - `CreditTermMonths ≈ AMT_CREDIT / AMT_ANNUITY`
  - `CTI = AMT_CREDIT / AMT_INCOME_TOTAL`
  - `DTI = (AMT_ANNUITY * 12) / AMT_INCOME_TOTAL`
- Cleaned codes (e.g., `CODE_GENDER='XNA'` → `Unknown`).

---

## 🧮 DAX (selected)
- **Bands (calculated columns):** `Age Band`, `Credit Band`, `DTI Band` (+ sort-by columns).  
- **Measures:**
  ```DAX
  Total Loans = COUNTROWS(Loans)
  Defaults = CALCULATE(COUNTROWS(Loans), Loans[TARGET] = 1)
  Default Rate = DIVIDE([Defaults], [Total Loans])
  Total Exposure = SUM(Loans[AMT_CREDIT])
  Avg Loan Amount = AVERAGE(Loans[AMT_CREDIT])
  Avg Income = AVERAGE(Loans[AMT_INCOME_TOTAL])
  Avg DTI = AVERAGE(Loans[DTI])

---

## Dashboard
<img width="1282" height="721" alt="image" src="https://github.com/user-attachments/assets/0534f77d-320f-4995-8765-725b59c5e2e9" />
<img width="1281" height="717" alt="image" src="https://github.com/user-attachments/assets/59352f6a-360b-4a39-be64-5401300d4a4d" />

---

## 📊 Report Pages
1) Risk Overview

KPI cards: Default Rate, Total Loans, Total Exposure, Avg Loan Amount

Slicers: Contract Type, Income Type, Education Type, Gender, Age Band, Credit Band, DTI Band

Charts:

Default Rate by Credit Band

Default Rate by Income Type

Default Rate by Education

Default Rate by Age Band

Scatter: Credit vs Income (TARGET color)

2) Segment Drillthrough

Drillthrough filters: Income Type, Education Type, Age Band, Credit Band, DTI Band (+ Gender/Contract Type optional)

Top section: KPI cards (Default Rate, Total Loans, Total Exposure, Avg Income, Avg DTI)

Left: Top 10 Occupations by Default Rate

Right: Organization Type table (Loans, Default Rate, Avg Loan)

Bottom: Credit Amount Distribution (binned)

