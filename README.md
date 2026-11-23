# Transactional Sales Data Cleaning & Transformation Project


📖 Table of Contents
- [About This Project](#-about-this-project)
- [Business Problem](#-business-problem)
- [Tools & Technologies](#-tools--technologies)
- [Dataset](#-dataset)
- [Folder Structure](#-folder-structure)
- [Problems Found in Raw Data](#-problems-found-in-raw-data)
- [Data Cleaning Process](#-data-cleaning-process)
- [Data Transformation](#-data-transformation)
- [Data Model](#-data-model)
- [Challenges & Solutions](#-challenges--solutions)
- [Skills Demonstrated](#-skills-demonstrated)
- [Future Improvements](#-future-improvements)


---

📌 About This Project
This project focuses on cleaning and transforming messy transactional sales data from **2016 to 2019** using **Power BI**.

The raw data came in 4 separate yearly files (`sales 2016.csv` to `sales 2019.csv`) with inconsistent formatting, mixed data, wrong capitalization, wrong data types, duplicates, and missing values.

I used **Power Query Editor** to clean, reshape, and combine the data into one clean model, then used **DAX** to create new tables, new columns, and key measures for analysis.

The final output is a clean, analysis-ready dataset fit for dashboards, reporting, and business decision-making.

---

🎯 Business Problem
A business had 4 years of sales data but could not trust it for reporting because:

- Sales figures did not match across years
- Product and customer names were written in different ways
- Dates and amounts were stored as text
- Mixed data in single columns made filtering impossible

**Goal:** Clean all 4 years, combine them into one trusted dataset, and build measures that answer: *How much did we sell? What sold best? Where did we sell most? How are we growing?*

---

🛠️ Tools & Technologies
| Tool | Used For |
| --- | --- |
| **Power BI Desktop** | Data loading, modelling, dashboard |
| **Power Query Editor (M)** | Cleaning, splitting, transforming |
| **DAX** | Measures, calculated columns, new tables |
| **Excel / CSV** | Raw data source |

---

📂 Dataset
**Source:** Transactional sales system exports

| File | Period |
| --- | --- |
| sales 2016.csv | Jan - Dec 2016 |
| sales 2017.csv | Jan - Dec 2017 |
| sales 2018.csv | Jan - Dec 2018 |
| sales 2019.csv | Jan - Dec 2019 |
| **Total Combined** | **2016 - 2019** |

**Main Columns in Raw Data:**
`Order ID`, `Order Date`, `Customer Name`, `City`, `Region`, `Product`, `Category`, `Quantity`, `Unit Price`, `Amount`, `Payment Method`

---

📁 Folder Structure
Transactional-Sales-Cleaning/
├── http://README.md
├── data/
│   ├── raw/
│   │   ├── sales 2016.csv
│   │   ├── sales 2017.csv
│   │   ├── sales 2018.csv
│   │   └── sales 2019.csv
│   └── clean/
│       └── clean_sales_2016-2019.csv
├── powerbi/
│   └── Sales_Cleaning_2016-2019.pbix
└── docs/
    └── screenshots/
        ├── http://power-query-steps.png
        ├── http://data-model.png
        

---

❌ Problems Found in Raw Data
- Mixed data in one column (e.g. Product + Category together, City / Region together)
- Inconsistent capitalization: `lagos`, `LAGOS`, `Lagos`
- Extra spaces and inconsistent spelling: `  Lagos `, `Abuja  `
- Dates stored as text in different formats
- Amounts / prices stored as text with commas and currency symbols: `₦1,500`, `1,500`
- Duplicates and blank rows
- Wrong data types (numbers as text, dates as text)
- Missing values: `unknown`, `N/A`, blank, `NULL`

---

🧹 Data Cleaning Process
All cleaning was done in **Power Query Editor** so every step is repeatable and auditable.

1. Loading & Combining Data
- Loaded all 4 CSV files into Power BI
- Used **Append Queries** to combine 2016-2019 into one fact table `Sales`
- Checked row counts before and after append to ensure no data loss

2. Removing Duplicates & Errors
- Removed duplicate rows based on `Order ID`
- Removed blank rows and error rows
- Removed empty columns created by export

3. Fixing Capitalization & Text
- Applied **Trim** to remove leading/trailing spaces: `Text.Trim()`
- Applied **Clean** to remove non-printable characters: `Text.Clean()`
- Fixed inconsistent capitalization using **Format > Capitalize Each Word** / `Text.Proper()`:
    - Product names standardized

4. Separating Mixed Data
- Some columns contained mixed data e.g. `Product - Category` or `City / Region`
- Used **Split Column > By Delimiter** (`-`, `/`, `,`) to separate into clean columns
- Renamed new columns: `Product`, `Category`, `City`, `Region`
- Removed the original mixed column after split

5. Fixing Data Types
| Column | Before | After |
| --- | --- | --- |
| Order Date | Text | Date |
| Quantity | Text | Whole Number |
| Unit Price | Text with commas / ₦ | Decimal Number |
| Amount | Text with commas | Decimal Number |
| Customer Name | Mixed case | Proper Case |

- Used **Change Type** and **Replace Values** to remove `₦`, `,`, and spaces before converting Amount to number
- Used **Date.From()** to convert mixed date formats to one standard `dd/mm/yyyy`

6. Handling Missing & Inappropriate Values
- Replaced `unknown`, `N/A`, `NULL`, `no-email`, blank → `null` or `Not Specified`
- Replaced negative / zero amounts where they were data entry errors
- Filled down missing Region based on City where possible

7. Renaming & Reordering
- Renamed all columns to clean, consistent names: `OrderID`, `OrderDate`, `CustomerName`, `ProductName`
- Reordered columns logically: Date → Customer → Product → Sales

8. Final Validation
- Checked for remaining duplicates: `0`
- Checked for nulls in key columns: `0`
- Checked Total Sales after cleaning matches source total (excluding errors)

---

🔄 Data Transformation

New Columns Created in Power Query / DAX
- `Year` = `YEAR([OrderDate])`
- `Month` = `FORMAT([OrderDate], "MMMM")`
- `Month Number` = `MONTH([OrderDate])`
- `Quarter` = `"Q" & FORMAT([OrderDate], "Q")`
- `Day of Week` = `FORMAT([OrderDate], "dddd")`

New Tables Created
1. **Date Table** - For time intelligence
2. **Products Table** - Distinct products for filtering
3. **Customers Table** - Distinct customers for analysis

--

---

💡 Skills Demonstrated
- Data Cleaning & Transformation
- Power Query (M Language) - Append, Split, Trim, Replace, Change Type
- DAX - SUM, CALCULATE, DIVIDE, DATEADD, DISTINCTCOUNT, TOPN
- Data Modelling - Fact vs Dimension, Star Schema
- Data Validation & Quality Checks

---

🚀 Future Improvements
- Connect to live SQL database instead of CSVs for automatic refresh
- Add customer segmentation (RFM Analysis) using DAX
- Add profit margin analysis if cost data is available
- Build a Power BI Service dashboard with scheduled refresh
- Add forecasting for 2020 sales using Power BI Forecast

---

👩‍💻 Author
[Solomon Joel]
Aspiring Data Analyst | Power BI | SQL | Excel | Power Query | DAX



---
_This project was built to demonstrate end-to-end data cleaning and transformation in Power BI — 
