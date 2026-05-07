CA1_MB25L33-36_IDDS
Sales & Logistics BI Dashboard — Interactive Dashboards and Data Storytelling (IDDS)
Course: Interactive Dashboards and Data Storytelling (IDDS)  
Assessment: CA 1 — Data Visualization Dashboard  
Institution: Dnyaan Prasad Global University — School of Management & Research  
Faculty: Prof. Sunita Bangal  
Group No.: 9  
Submission Date: 7th April 2026
---
👥 Group Members
Roll No.	Name
MB25L33	Sanyogita Indrajeetsing Rajput
MB25L34	Saptarishi Sanjay Garje
MB25L35	Sejal Parashar
MB25L36	Shiv Nandan Yadav
---
📌 Business Problem Statement
The organization operates across 4 regions (North, South, East, West) and 3 sales channels (Online, Store, Marketplace) selling across product categories including Electronics, Fashion, Grocery, and Home & Kitchen.
Analysis of FY 2022–2023 data reveals key operational challenges:
West region contributes ~40% of total revenue (₹15.3L) yet has the longest average delivery time (4–5 days), creating a latent churn risk
A return rate of 0.52 and seasonal revenue volatility (low: ₹95K, peak: ₹160K) indicate structural risks in demand and fulfillment management
Unstructured discounting (avg 10.45%) across regions is eroding net profitability without proportional revenue gains
Target Stakeholders: Sales Head & Operations Manager  
Goal: Enable data-driven decisions on regional strategy, channel investment, discount optimization, and logistics improvement.
---
📁 Repository Structure
```
CA1_MB25L33-36_IDDS/
│
├── README.md                              ← This file
├── CA1_MB25L33-36_Sales_Logistics.xlsx   ← Cleaned dataset (Advanced Excel dashboard)
├── CA1_MB25L33-36_Sales_Logistics.pbix   ← Power BI report file (4 pages)
├── CA1_MB25L33-36_Presentation.pdf       ← 3–5 min presentation export
└── screenshots/
    ├── dashboard_page2.png                ← Main dashboard screenshot
    ├── insights_page3.png                 ← Insights & recommendations page
    ├── home_page1.png                     ← Navigation/home page
    └── data_model.png                     ← Power BI data model view
```
---
📊 Dataset Description
Source: Provided by faculty — Sales & Logistics academic dataset  
Period: January 2022 – December 2023  
Format: Microsoft Excel (.xlsx) — 4 sheets
Sheet	Rows	Key Columns
Sales_Data	360	Order_ID, Date, Region, Channel, Product_Category, Revenue, Unit_Price, Quantity, Discount_%, Delivery_Days, Returned
Customer_Master	100	Customer_ID, City, Age, Gender, Income_Level, Segment
Product_Master	50	Product_ID, Product_Category, Cost_Price, Supplier, Lead_Time_Days
Logistics_Data	48	Region, Date, Total_Shipments, OnTime_%, Avg_Delay_Hours, Transport_Cost
---
🧹 Data Cleaning Log
All cleaning was performed in Power Query Editor (Power BI) and Excel.
#	Issue Found	Column(s) Affected	Action Taken
1	Inconsistent region casing: `'west '`, `'West'`, `'EAST'`	Region	Standardized to: North, South, East, West using `Text.Proper()` + `Text.Trim()` in Power Query
2	Inconsistent channel casing: `'online'`, `'Online'`	Channel	Standardized to: Online, Store, Marketplace
3	Inconsistent category casing: `'electronics'`, `'Electronics'`	Product_Category	Standardized to: Electronics, Fashion, Grocery, Home & Kitchen
4	Inconsistent returned values: `'yes'`, `'Yes'`, `'NO'`, `'No'`, null	Returned	Standardized to Yes/No. Nulls (72 rows) treated as "No" — assumption: no return recorded = no return made
5	Revenue stored as text with commas: `'5,293'`	Revenue	Converted to numeric using `Number.FromText(Text.Remove(..., {","}))`
6	Missing Discount_% values	Discount_% (64 nulls)	Replaced with 0 — assumption: no discount applied if not recorded
7	Mixed date formats: `'01/01/2022'` and `'Sep-2023'`	Date	Standardized to DD/MM/YYYY format using Power Query date parsing
8	Blank/unnamed extra column	Column 13 (Unnamed)	Deleted — 359 of 360 rows were empty
9	Missing Age and Income values	Customer_Master (57 & 52 nulls)	Retained as-is; excluded from age/income-specific visuals
10	Missing OnTime_% values	Logistics_Data (31 nulls)	Replaced with column average — noted as limitation
Assumption disclosure: All assumptions above are documented as limitations on the Insights page of the Power BI report.
---
🔗 Data Model / Relationships
Relationships established in Power BI Model View:
```
Sales_Data[Customer_ID]      →  Customer_Master[Customer_ID]    (Many-to-One)
Sales_Data[Product_Category] →  Product_Master[Product_Category] (Many-to-One)
Sales_Data[Region]           →  Logistics_Data[Region]           (Many-to-One)
```
> Screenshot of the data model is available in `/screenshots/data_model.png`
---
📐 DAX Measures Used
```dax
Total Revenue = SUM(Sales_Data[Revenue])

Avg Discount % = AVERAGE(Sales_Data[Discount_%])

Return Rate = 
DIVIDE(
    COUNTROWS(FILTER(Sales_Data, Sales_Data[Returned] = "Yes")),
    COUNTROWS(Sales_Data)
)

Avg Delivery Days = AVERAGE(Sales_Data[Delivery_Days])

OnTime Delivery % = AVERAGE(Logistics_Data[OnTime_%])

Total Quantity Sold = SUM(Sales_Data[Quantity])

Average Order Value = DIVIDE([Total Revenue], COUNTROWS(Sales_Data))

Revenue Growth % = 
DIVIDE(
    [Total Revenue] - CALCULATE([Total Revenue], PREVIOUSYEAR('Sales_Data'[Date])),
    CALCULATE([Total Revenue], PREVIOUSYEAR('Sales_Data'[Date]))
) * 100
```
---
📈 Dashboard Pages Overview
Page 1 — Home / Navigation
Report title and group details
3 navigation buttons (Page Navigation action) linking to Dashboard, Insights, and Problem Statement pages
3 synced slicers: Region, Channel, Date Range
Page 2 — Main Dashboard
5 KPI Cards: Total Revenue (₹4M), Avg Discount % (10.45), Return Rate (0.52), Total Quantity Sold (2K), Average Order Value (₹13.96K)
Visual 1: Total Revenue by Region — Horizontal Bar Chart
Visual 2: Monthly Revenue Trend 2022–23 — Line Chart
Visual 3: Total Orders by Product Category — Bar Chart
Visual 4: Total Revenue by Channel — Donut Chart
Visual 5: Avg Delivery Time, Revenue & Quantity by Region — Scatter Plot
All visuals respond to Page 1 slicers
Page 3 — Insights & Recommendations
3 key insights with supporting mini-charts as visual evidence
2 actionable recommendations for stakeholders
1 limitation/assumption note
Ethical disclosure statement
Page 4 — Problem Statement & Data Context
Full business problem statement
Stakeholder identification
Dataset summary
Data cleaning log table
Data model screenshot
---
💡 Key Insights
Insight 1 — West Region Revenue Dominance with Delivery Risk
West region contributes ₹15,31,893 (~40% of total revenue), significantly ahead of North (₹9,36,069), East (₹7,86,250), and South (₹6,96,301). However, the scatter plot reveals West also has the highest average delivery time (4–5 days) and highest revenue — meaning customers are tolerating delays today, but this is a latent churn risk if not addressed.
Insight 2 — Seasonal Revenue Volatility
Revenue peaked at ₹160K in Aug–Nov 2023 but dropped sharply to ₹121K in December 2023 — a ~24% quarter-end decline. A similar trough occurred in mid-2022 (₹95K). This pattern indicates demand seasonality requiring proactive inventory and staffing planning before peak periods.
Insight 3 — Electronics Drives Volume, Not Necessarily Value
Electronics has the highest order count (104 orders) across all product categories, yet Fashion (72 orders) and Home & Kitchen (59 orders) likely yield higher revenue-per-order. This volume-vs-value disconnect requires a category-wise profitability review to identify where margin is actually being made.
---
✅ Recommendations
Recommendation 1 — Targeted Discounting Strategy  
Replace blanket discounting (avg 10.45%) with segment-based pricing. Premium customer segments should receive loyalty benefits instead of blanket discounts. Reducing average discount by just 2–3% across 360 orders can significantly improve net margin.
Recommendation 2 — Logistics Optimization in West Region  
Despite generating the highest revenue, West has the longest delivery time. Auditing the logistics partner in West and setting SLA targets (on-time delivery > 85%) will protect customer retention in the most valuable region.
---
⚠️ Limitations & Ethical Disclosure
72 missing "Returned" values were treated as "No" — this may underestimate the true return rate
31 missing OnTime_% values in Logistics_Data were imputed with column average — logistics performance metrics may not be fully representative
64 missing Discount_% values were replaced with 0 — actual discount figures may be higher
Revenue column had mixed formatting (text vs numeric) — corrected during ETL but source data quality should be improved
All axes in visuals start at zero to avoid misleading comparisons
Data source is an academic dataset provided by faculty — findings should not be used for real business decisions without validation on live data
Dataset covers only FY 2022–2023 — trends may not reflect current market conditions
---
🛠️ Tools Used
Tool	Purpose
Microsoft Excel (Advanced)	Data cleaning, pivot tables, Excel dashboard visuals
Power BI Desktop	ETL via Power Query, DAX measures, 4-page interactive report
GitHub	Version control and artifact submission
PowerPoint / PDF	Presentation export
---
📎 How to Open the Files
Excel file: Open with Microsoft Excel 2016 or later
PBIX file: Open with Power BI Desktop (free download)
Go to File → Open → select `CA1_MB25L33-36_Sales_Logistics.pbix`
All 4 pages and slicers will be available
PDF presentation: Open with any PDF viewer
---
📬 Submission
Submitted via: https://forms.gle/6vjbrCv52PHzuEZ69  
GitHub Repository: (paste your repo link here after creating)
---
This repository is created for academic purposes as part of IDDS CA1 assessment at DPGU School of Management & Research.
