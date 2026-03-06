🍽️ Swiggy Food Delivery Analytics
Data Warehouse | SQL Analytics | Business Intelligence
📌 Project Overview

This project builds a scalable analytics solution for food delivery data, transforming raw operational records into a structured data warehouse optimized for business intelligence and decision-making.

Using 165K+ order records, the project demonstrates how real-world transactional data can be transformed into actionable insights for business strategy.

The pipeline includes:

Data ingestion

Data cleaning & validation

Dimensional modeling

Data warehouse design

KPI generation

Business intelligence reporting

The final system enables deep insights into revenue trends, customer behavior, restaurant performance, and geographic demand patterns.

🧠 Business Problem
-Food delivery platforms like Swiggy generate large volumes of data.To scale efficiently, the business must answer critical questions:

Which cities generate the most revenue?

What food categories drive the highest demand?

Which restaurants perform best?

How do customer spending patterns vary?

Are there seasonal or time-based ordering trends?

However, raw transactional data is not optimized for analytics.

Without proper data modeling:

Queries become slow

Business metrics are inconsistent

Insights are difficult to extract

This project solves the problem by building a data warehouse architecture and generating business KPIs through analytical SQL queries.

🎯 Project Objectives

The key objectives of this project were:

1️⃣ Transform raw order data into a clean, structured dataset
2️⃣ Design a Star Schema Data Warehouse for fast analytical queries
3️⃣ Build SQL queries to generate business KPIs and insights
4️⃣ Enable interactive dashboard reporting using Power BI


🧠 Project Architecture
Raw Data (CSV)
        │
        ▼
MySQL Data Cleaning
        │
        ▼
Star Schema Data Warehouse
        │
        ▼
Fact + Dimension Tables
        │
        ▼
Business KPI Queries
        │
        ▼
Power BI Dashboard 

⚙️ Data Pipeline
1️⃣ Data Ingestion

Raw CSV data was imported into MySQL.

Example:

LOAD DATA INFILE 'Swiggy_Data.csv'
INTO TABLE swiggy_data1
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
2️⃣ Data Cleaning & Validation

Multiple checks were performed to ensure data quality.

Data Quality Checks

NULL value detection

Blank string validation

Duplicate detection

Data type corrections

Example:

SELECT
SUM(state IS NULL) AS state_nulls,
SUM(city IS NULL) AS city_nulls
FROM swiggy_data1;
3️⃣ Data Transformation

Raw transactional data was transformed into dimensional tables.

Date Dimension Example
INSERT INTO dim_date
SELECT DISTINCT
order_date,
YEAR(order_date),
MONTH(order_date),
MONTHNAME(order_date),
QUARTER(order_date),
DAY(order_date),
WEEK(order_date,1)
FROM swiggy_data1;
4️⃣ Performance Optimization

Indexes were created to improve query performance.

Example:

CREATE INDEX idx_swiggy_date
ON swiggy_data1(order_date);

This significantly improves join performance and aggregation speed.

🗂 Dataset
Source: Food delivery dataset (Swiggy)
Records: 197,000+
Fields: 10
Key columns:
-State
-City
-Order Date
-Restaurant Name
-Location
-Category
-Dish Name
-Price
-Rating
-Rating Count

🛠 Tech Stack
Tool	Purpose
MySQL 8.0	Data cleaning & warehouse creation
SQL	Data transformation & KPI queries
Star Schema	Data warehouse design
Power BI	Interactive dashboard
GitHub	Project portfolio

🏗 Data Warehouse Design
A Star Schema was created to optimize analytical queries.
1.Dimension Tables
1.dim_date
2.dim_location
3.dim_restaurant
4.dim_category
5.dim_dish
Fact Table

2.fact_swiggy_orders
Contains:
-Order metrics
-Price
-Rating
-Foreign keys to dimensions
This structure improves query performance and scalability.

📂 SQL Implementation
The complete SQL implementation is available here:
📄 SQL Script: swiggy_data_pro1.mysql
The script includes:
-Database creation
-Data import
-Data cleaning
-Duplicate removal
-Index optimization
-Star schema creation

📈 Key Business KPIs

The data warehouse enables fast calculation of critical metrics.

Total Orders
SELECT COUNT(*) AS total_orders
FROM fact_swiggy_orders;
Total Revenue
SELECT ROUND(SUM(price_inr)/1000000,2)
AS total_revenue_inr_million
FROM fact_swiggy_orders;
Average Dish Price
SELECT ROUND(AVG(price_inr),2)
FROM fact_swiggy_orders;
Average Rating
SELECT ROUND(AVG(rating),2)
FROM fact_swiggy_orders;

🔍 Business Analysis Performed
📅 Time Analysis
-Monthly order trends
-Quarterly growth
-Yearly performance
-Orders by day of week

📍 Location Insights
-Top cities by order volume
-Top cities by revenue
-Revenue contribution by state

🍽 Food Performance
-Top restaurants by orders
-Most popular dishes
-Category performance

💰 Customer Spending Behavior
Orders analyzed across price ranges:
-Under ₹100
-₹100 – ₹199
-₹200 – ₹299
-₹300 – ₹499
-₹500+

⭐ Rating Insights
-Distribution of dish ratings
-Category level average rating

📊 Power BI Dashboard
The Power BI dashboard includes:
✔ KPI overview
✔ City level analysis
✔ Order trend visualization
✔ Category performance
✔ Restaurant performance

Dashboard file:dashboard/swiggy_powerbi_dashboard.pbix

📌 Key Insights
Some interesting findings from the analysis:
-A small number of cities generate majority of orders
-Certain categories dominate order volume
-Most orders fall in the ₹200-₹299 price range
-Highly rated dishes correlate with higher order counts

📷 Dashboard Preview

(Add screenshots here)

Example:

images/dashboard_overview.png
images/city_analysis.png


🎯 Skills Demonstrated
-SQL Data Cleaning
-Data Warehouse Design
-Star Schema Modeling
-Index Optimization
-Analytical SQL
-Business KPI Analysis
-Power BI Dashboarding
-Data Storytelling

👤 Author

Sapna

Aspiring Data Analyst / Data Engineer

Skills:
-SQL
-Power BI
-Data Warehousing
-Business Analytics

⭐ If you like this project

Give it a star ⭐ on GitHub!
