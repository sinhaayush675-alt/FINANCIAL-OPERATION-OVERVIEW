

┌──────────────────┐      ┌─────────────────┐      ┌──────────────────┐
│  Generative AI   │ ───► │ Microsoft Excel │ ───► │     Power BI     │
│ (Raw Messy Data) │      │(Data Preprocess)│      │ (Data Viz & DAX) │
└──────────────────┘      └─────────────────┘      └──────────────────┘ 


## 🛠️ Project Overview

This project demonstrates a real-world enterprise data reporting workflow:
1. **Generating** complex, raw, and uncleaned transactional financial data using Generative AI.
2. **Cleaning & Structuring** messy fields, dates, missing entries, and monetary formats using Microsoft Excel.
3. **Building** an interactive Power BI dashboard complete with dynamic time-intelligence DAX functions, custom star-schema date tables, and KPI scorecards.


# 📊 End-to-End Financial & Operations Analytics Dashboard

---

## 🧰 Tech Stack

* **Data Generation:** Generative AI (Synthetic Data Engine)
* **Data Preprocessing:** Microsoft Excel (Power Query, Text Functions, Formatting)
* **Data Visualization:** Microsoft Power BI Desktop
* **Analytics Engine:** DAX (Data Analysis Expressions)

---

## 🧬 Data Pipeline

### 1. Data Generation (GenAI)
* Synthetic sales and operational data generated via Generative AI to simulate messy real-world business records.
* **Fields Included:** `Date`, `Transaction_ID`, `Customer_ID`, `Customer_Segment`, `Region`, `Product_Category`, `Sales_Manager`, `Order_Quantity`, `Unit_Cost`, `Unit_Price`, `Gross_Sales`, `Discount_Amount`, `Net_Sales`, `Cost_of_Goods_Sold`.

### 2. Data Cleaning & Preparation (Excel)
Before importing into Power BI, raw data was audited and standardized in **Excel**:
* **Date Standardization:** Standardized mixed date strings into clean `YYYY-MM-DD` ISO formats.
* **Numeric Integrity:** Cleaned string currency symbols (e.g., `$`) and enforced proper decimal structures for financial math.
* **Calculated Validation:** Cross-checked conditional column logic:
  - Net Sales = Gross Sales - Discount Amount
  - COGS = Order Quantity * Unit Cost

### 3. Visualization & DAX Modeling (Power BI)
* Created a continuous, dedicated **Date Dimension Table (`Calendar`)** marked as a Date Table to prevent time-intelligence calculation errors.
* Designed a relational model connecting `'Calendar'[Date]` to `'Sales_Data'[Date]`.

---

## 🧮 Key Business Metrics (DAX)

The dashboard is powered by custom DAX measures created within a dedicated `_Measures` table:

// Core Revenue & Margin Measures
Total Net Sales = SUM('Sales_Data'[Net_Sales])
Total COGS = SUM('Sales_Data'[Cost_of_Goods_Sold])
Gross Profit = [Total Net Sales] - [Total COGS]
Gross Profit Margin % = DIVIDE([Gross Profit], [Total Net Sales], 0)
Discount Rate % = DIVIDE(SUM('Sales_Data'[Discount_Amount]), SUM('Sales_Data'[Gross_Sales]), 0)

// Time Intelligence Measures
PY Net Sales = CALCULATE([Total Net Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))
YoY Sales Growth % = DIVIDE([Total Net Sales] - [PY Net Sales], [PY Net Sales], 0)

---

## 🖥️ Dashboard Visuals & Layout

* **Top Banner (KPI Cards):** High-level Scorecards displaying **Total Net Sales**, **Gross Profit Margin %**, **Total COGS**, and **Discount Rate %**.
* **Middle Left (Area Chart):** Monthly Net Sales Revenue Trend line with shaded opacity overlay.
* **Middle Right (Clustered Bar Chart):** Product Category breakdown sorted by revenue.
* **Bottom Matrix Visual:** Sales Manager & Regional Breakdown featuring integrated conditional **Data Bars** and **Profit Target Indicators**.


  
