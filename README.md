# 🚀 Sales Performance Dashboard

**A professional Power BI project** that analyzes sales, customer experience, and operational performance for a simulated **Food Delivery** dataset.

This repository contains:
- 📌 `Food_Delivery_Dashboard.pbix` — Main Power BI report
- 🗂️ Star schema data model
- 🧮 Key DAX measures for business KPIs
- 🗺️ Optional custom GeoJSON for India state analysis
- 🎨 (Coming soon) Dark Neon Power BI theme file

---

## 🎯 Project Goals

| Objective | Description |
|-----------|-------------|
| 💰 **Revenue Tracking** | Track sales volume, revenue trends and growth % |
| 🧠 **Operational Insights** | Identify best & worst performing restaurants & dishes |
| ⭐ **Customer Experience** | Monitor ratings and detect quality issues |
| 🗺️ **Geographic Analysis** | Identify key high-revenue cities/states |

---

## 🛠️ Data & Setup

### 1️⃣ SQL Server Data Source

| Component | Setting (example) |
|-----------|-------------------|
| Server Name | `(DESKTOP-ABHIJIT\SQLEXPRESS`) |
| Database | `SwiggyDB` |


🔗 **How to connect in Power BI:**
> `Home` → `Get Data` → `SQL Server` → enter server & database → choose tables.

---

### 2️⃣ Star Schema Data Model (Power BI)

| Table Type | Table Name | Description |
|------------|------------|-------------|
| 📌 **Fact** | `fact_swiggy_orders` | Transactions + Ratings + Prices |
| 🕓 **Dim Date** | `dim_date` | Date hierarchy for DAX |
| 🏙️ **Dim Location** | `dim_location` | State → City mapping |
| 🍽️ **Dim Restaurant** | `dim_restaurant` | Restaurant attributes |
| 🍴 **Dim Dish** | `dim_dish_name`, `dim_category` | Dish & category definitions |

> ⚠️ Mark `dim_date` as **Date Table** for Time Intelligence measures.

---

## 🧹 Data Preparation (Power Query)

Common transformations performed:
- 🔤 Trim & standardize case for cities, restaurants
- 💰 Set correct numeric types (currency, decimals)
- ⭐ Remove/ignore zero or null ratings for accuracy
- 🌍 Standardize state names for mapping accuracy

📌 **Example: Trim + Proper Case for City**
```m
= Table.TransformColumns(Source, {{"City", each Text.Proper(Text.Trim(_)), type text}})


-- Total Revenue
[Total Revenue] =
SUM('fact_swiggy_orders'[Price_INR])

-- Total Orders
[Total Orders] =
COUNTROWS('fact_swiggy_orders')

-- Average Order Value (AOV)
[AOV] =
DIVIDE([Total Revenue], [Total Orders])

-- Previous Month Revenue
[PM Revenue] =
CALCULATE([Total Revenue], DATEADD('dim_date'[Full_date], -1, MONTH))

-- Month-over-Month Growth %
[MoM Revenue %] =
DIVIDE([Total Revenue] - [PM Revenue], [PM Revenue])

-- Average Rating (exclude 0/null)
[Avg Rating] =
CALCULATE(
    AVERAGE('fact_swiggy_orders'[Rating]),
    FILTER('fact_swiggy_orders', 'fact_swiggy_orders'[Rating] > 0)
)


📊 Dashboard Overview
📍 Report 1: Sales Performance Summary

🔹 KPIs (Revenue, Orders, AOV, MoM%)
🔹 Revenue Trend over Time
🔹 Map of Revenue by State/City

⭐ Report 2: Customer Experience & Quality

🔸 Rating Distribution (1–5 Star)
🔸 Restaurant Quality Scorecard
🔸 Avg Rating Trend

## 📊 Dashboard Preview
  <img src="https://github.com/user-attachments/assets/691b0708-8406-4aef-8fe7-8c754128c747" width="850">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/851c82da-14ff-40d3-8f71-54cce9292823" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/63b371d9-af19-46ae-9e00-d77e049ad8a9" />
