# 🚲 Bike Sales Analysis — Tableau Dashboard Project

> **End-to-End Data Analytics Project** | Excel · MySQL Workbench · Tableau Desktop  
> Prepared by **Rahul** | MS Information Systems | Texas Tech University, Rawls College of Business | 2026

---

## 📌 Overview

This project delivers a complete, interactive **Bike Sales Analysis Dashboard** built in **Tableau Desktop** using a real-world bike sales dataset. The pipeline covers every stage of a data analytics workflow — from raw data inspection and SQL-based normalization, through to a polished, multi-visual, parameter-driven Tableau dashboard.

The dashboard answers key business questions:
- Which products sell the most? Which are most profitable?
- Which age groups and genders drive the most revenue?
- Which countries generate the highest profit?
- How has profit changed year over year?

---

## 📂 Dataset

| Property | Detail |
|---|---|
| **File** | `Bike_sales.twbx` (Tableau Packaged Workbook — data embedded) |
| **Source** | Bike Sales transactional dataset (Kaggle) |
| **Records** | ~100,000+ sales transactions |
| **Date Range** | 2011 – 2016 |
| **Total Fields** | 15 columns |

### Fields

| Field | Type | Description |
|---|---|---|
| `Date` | Date | Transaction date |
| `Country` | Dimension | Country of sale (US, UK, Canada, Australia, France, Germany) |
| `State` | Dimension | State / region |
| `Customer Age` | Measure | Customer age in years |
| `Age Group` | Dimension | Youth · Young Adults · Adults · Seniors |
| `Customer Gender` | Dimension | Male / Female |
| `Product Category` | Dimension | Accessories · Bikes · Clothing |
| `Sub Category` | Dimension | Road Bikes, Helmets, Jerseys, etc. |
| `Product` | Dimension | Individual product name |
| `Order Quantity` | Measure | Units sold per transaction |
| `Unit Cost` | Measure | Cost per unit |
| `Unit Price` | Measure | Selling price per unit |
| `Cost` | Measure | Total cost (Unit Cost × Quantity) |
| `Revenue` | Measure | Total revenue (Unit Price × Quantity) |
| `Profit` | Measure | Net profit (Revenue − Cost) |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Raw data inspection, Text-to-Columns split, TRIM/clean, separate worksheets |
| **MySQL Workbench** | Schema creation, Table Data Import Wizard, SQL UNION normalization queries |
| **Tableau Desktop** | Data connection, worksheet design, dashboard assembly |
| **Tableau (.twbx)** | Packaged workbook — bundles workbook + embedded .hyper data extract |

---

## 🔄 Steps / Workflow

### Step 1 — Data Acquisition
- Downloaded the Bike Sales dataset (CSV format)
- Opened in Excel to inspect all 15 columns and identify data quality issues
- Identified multi-value columns requiring normalization

### Step 2 — Excel Data Preparation
- Used **Text to Columns** (Data → Delimited → Comma) to split multi-value fields
- Applied **TRIM()** to remove leading/trailing whitespace
- Used **Find & Replace** to fill blank cells with `Null`
- Organized each split table into its own worksheet tab

### Step 3 — MySQL Data Import
- Created schema: `bike_sales` in MySQL Workbench
- Imported cleaned CSVs using **Table Data Import Wizard**
- Set `Date` and key fields with correct data types
- Verified row counts post-import

### Step 4 — Relational Table Design (SQL)
- Created normalized dimension tables using `CREATE TABLE … AS SELECT … UNION` queries
- Filtered out NULL rows using `WHERE column IS NOT NULL`

### Step 5 — Tableau Data Connection
- Connected Tableau Desktop → **MySQL Database** → `bike_sales` schema
- Loaded all tables in a single import operation
- Verified field types and row counts in Tableau Data Source tab

### Step 6 — Calculated Fields & Parameter
- **Year Parameter** — Date parameter (2011–2016) shown as radio buttons on dashboard
- **Year Filter** — `DATE(DATETRUNC('year', [Date])) = [Parameter 1]`
- **Chosen Year Profit** — `IF [Date - Year] = [Parameter 1] THEN [Profit] END`
- **Last Year Profit** — `IF [Date - Year] = DATEADD('year', -1, [Parameter 1]) THEN [Profit] END`
- **YoY % Change** — `(SUM([Chosen Year Profit]) - SUM([Last Year Profit])) / SUM([Last Year Profit])`

### Step 7 — Worksheet Design (9 Sheets)

| # | Sheet Name | Visual Type | Key Fields |
|---|---|---|---|
| 1 | Top 10 Products | Horizontal Bar Chart | Product, Order Quantity (TopN filter) |
| 2 | Sub Category Bar Chart | Stacked Bar Chart | Sub Category, Profit, Gender |
| 3 | Age Group Bubble Chart | Packed Bubble Chart | Age Group, Revenue (size + color) |
| 4 | Map | Geographic Bubble Map | Country, Profit |
| 5 | Profit Card | KPI Text Card | Chosen Year Profit |
| 6 | YoY % Change | KPI Text Card | YoY % Change calculated field |
| 7 | Revenue Card | KPI Text Card | SUM(Revenue) |
| 8 | Revenue Line Chart | Line Chart | Date (Month), Revenue |
| 9 | Cost Card | Text Table | Product Category, SUM(Cost) |

### Step 8 — Dashboard Assembly
- Created **Sales Dashboard** canvas in Tableau Desktop
- Used **Horizontal & Vertical Layout Containers** for structured zone placement
- Applied **Year Parameter** as a global control (radio button)
- Added **Country** as a multi-select checkbox filter (applied to all sheets)
- Set all filters to **Apply to All Worksheets Using This Data Source**
- Applied consistent **orange-and-dark colour theme** throughout

---

## 📊 Dashboard

**Dashboard Name:** `Bike Sales Analysis`  
**File:** `Bike_sales.twbx`

### Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  🚲  Bike Sales Analysis                                            │
├──────────┬──────────────────────────┬──────────────────┬───────────┤
│ Profit   │ Top 10 Products          │ Product Category │ Year      │
│ $7,035K  │ (Horizontal Bar)         │ Sales by Gender  │ Param..   │
│ YoY -6.5%│                          │ (Stacked Bar)    │ ○ 2011    │
├──────────┤                          │                  │ ○ 2012    │
│ Revenue  │──────────────────────────│──────────────────│ ○ 2013    │
│ $17.7M   │ Sales by Age Group       │ Sales by Country │ ● 2016    │
├──────────┤ (Bubble Chart)           │ (World Map)      ├───────────┤
│ Access.  │                          │                  │ Country   │
│ Bikes    │                          │                  │ ☑ (All)   │
│ Clothing │                          │                  │ ☑ Aust.   │
└──────────┴──────────────────────────┴──────────────────┴───────────┘
```

### Key Metrics (2016 Sample)

| Metric | Value |
|---|---|
| Total Profit | $7,035,948 |
| Year-on-Year Change | −6.5% |
| Total Revenue | $17,713,385 |
| Accessories Cost | $1,720,138 |
| Bikes Cost | $7,507,005 |
| Clothing Cost | $1,450,294 |

---

## 📈 Key Results & Insights

### 🏆 Product Performance
- **Water Bottle (30 oz)** is the #1 product by volume at **47K units**
- **Accessories dominate quantity** — top 10 products are all accessories (low unit cost, high repeat rate)
- **Bikes drive revenue** despite much lower unit volume — highest-margin category

### 👥 Customer Demographics
- **Adults** are the largest revenue-generating age group (biggest bubbles in bubble chart)
- **Male customers** generate significantly higher profit in Road Bikes and Touring Bikes
- **Seniors** represent a notable secondary segment worth targeted marketing

### 🌍 Geographic Distribution
- **United States** is the dominant market by a significant margin
- **Australia** punches above its weight relative to population size
- European markets (UK, Canada, France, Germany) contribute but are not dominant

### 📉 Financial Trends
- YoY profit declined **−6.5%** in the selected year — warrants investigation into pricing or volume
- **Bikes = 70% of total cost** ($7.5M of $10.7M) — margin management is critical
- Revenue Line Chart shows clear **seasonality peaks** in spring/summer months

---

## 📁 Project File Structure

```
bike-sales-tableau/
│
├── Bike_sales.twbx              # Tableau Packaged Workbook (data + viz)
├── README.md                    # This file
│
├── data/
│   ├── bike_sales_raw.csv       # Original dataset
│   ├── Cast.csv                 # Normalized cast/member table (if applicable)
│   ├── Countries.csv            # Normalized countries table
│   └── Description.csv         # Product descriptions
│
├── sql/
│   ├── create_schema.sql        # MySQL schema setup
│   ├── import_tables.sql        # Table creation scripts
│   └── union_normalize.sql      # UNION normalization queries
│
└── report/
    └── Bike_Sales_Tableau_Report.docx   # Full project report (Word)
```

---

## ▶️ How to Run

### Prerequisites
- [Tableau Desktop](https://www.tableau.com/products/desktop) (any recent version)
- OR [Tableau Public](https://public.tableau.com/) (free) to view .twbx files
- MySQL Workbench (optional — only needed to rebuild from raw data)

### Option A — Open the Packaged Workbook (Easiest)
```bash
# Simply double-click the .twbx file, or:
# File → Open → Select Bike_sales.twbx in Tableau Desktop
```
The `.twbx` file contains both the workbook and embedded data — no database connection required.

### Option B — Rebuild from Raw Data
```sql
-- 1. Create schema in MySQL Workbench
CREATE DATABASE bike_sales;
USE bike_sales;

-- 2. Import bike_sales_raw.csv using Table Data Import Wizard

-- 3. Run normalization queries
-- (see /sql/union_normalize.sql)
```

```
-- 4. Connect Tableau Desktop:
--    Connect → MySQL → localhost → bike_sales
--    Load all tables → build worksheets → assemble dashboard
```

### Option C — Use Tableau Public (No Installation)
1. Go to [public.tableau.com](https://public.tableau.com)
2. Sign in → My Profile → Create a Viz
3. Upload `Bike_sales.twbx`
4. Explore the interactive dashboard online

---

## 🧠 Skills Demonstrated

| Category | Skills |
|---|---|
| **Data Preparation** | Excel Text-to-Columns, TRIM, Find & Replace, multi-sheet organization |
| **SQL / Database** | MySQL schema design, Table Import Wizard, CREATE TABLE AS SELECT, UNION queries, NULL filtering |
| **Tableau** | Data connection, calculated fields, parameters, TopN filters, mark types (Bar, Circle, Pie, Map) |
| **Dashboard Design** | Layout containers, global filters, parameter controls, colour theming |
| **Business Analytics** | KPI cards, YoY comparison, demographic analysis, geographic profitability |

---

## 👤 Author

**Rahul**  
MS Information Systems | Texas Tech University, Rawls College of Business  
📧 Available on LinkedIn  
📅 2026

---

## 📄 License

This project was created for educational purposes as part of the Udemy course  
*"Data Analysis | SQL, Tableau, Power BI & Excel | Real Projects"*

Dataset sourced from Kaggle — used for learning and portfolio demonstration only.

---

*⭐ If you found this project useful, consider giving it a star on GitHub!*
