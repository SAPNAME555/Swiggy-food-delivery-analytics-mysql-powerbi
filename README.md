Swiggy Food Delivery Analytics | Data Warehouse & Business Intelligence

📊 Project Overview

This project analyzes Swiggy food delivery data (165K+ records) by building a Data Warehouse using MySQL and creating interactive business dashboards in Power BI.

The objective was to simulate a real-world data engineering + analytics workflow including:

Data ingestion

Data cleaning

Data modeling (Star Schema)

KPI generation

Business analysis

Data visualization

The project demonstrates end-to-end data analytics skills used in industry.

🚀 Business Problem

Food delivery platforms like Swiggy generate large volumes of data.
Companies need analytics to answer questions such as:

Which cities generate the most orders?

Which restaurants and dishes are most popular?

What price ranges customers prefer

Monthly order trends

Revenue contribution by state

This project builds a data warehouse and analytics pipeline to answer these questions.

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
🗂 Dataset

Source: Food delivery dataset (Swiggy)

Records: 165,000+

Fields: 10

Key columns:

State

City

Order Date

Restaurant Name

Location

Category

Dish Name

Price

Rating

Rating Count

🛠 Tech Stack
Tool	Purpose
MySQL 8.0	Data cleaning & warehouse creation
SQL	Data transformation & KPI queries
Star Schema	Data warehouse design
Power BI	Interactive dashboard
GitHub	Project portfolio
🏗 Data Warehouse Design

A Star Schema was created to optimize analytical queries.

Dimension Tables

dim_date

dim_location

dim_restaurant

dim_category

dim_dish

Fact Table

fact_swiggy_orders

Contains:

Order metrics

Price

Rating

Foreign keys to dimensions

This structure improves query performance and scalability.

📂 SQL Implementation

The complete SQL implementation is available here:

📄 SQL Script:


swiggy_data_pro1.mysql

The script includes:

Database creation

Data import

Data cleaning

Duplicate removal

Index optimization

Star schema creation

KPI queries

📈 Key Business KPIs
Total Orders
SELECT COUNT(*) FROM fact_swiggy_orders;
Total Revenue
SELECT SUM(price_inr) FROM fact_swiggy_orders;
Average Dish Price
SELECT AVG(price_inr) FROM fact_swiggy_orders;
Average Rating
SELECT AVG(rating) FROM fact_swiggy_orders;
🔍 Business Analysis Performed
📅 Time Analysis

Monthly order trends

Quarterly growth

Yearly performance

Orders by day of week

📍 Location Insights

Top cities by order volume

Top cities by revenue

Revenue contribution by state

🍽 Food Performance

Top restaurants by orders

Most popular dishes

Category performance

💰 Customer Spending Behavior

Orders analyzed across price ranges:

Under ₹100

₹100 – ₹199

₹200 – ₹299

₹300 – ₹499

₹500+

⭐ Rating Insights

Distribution of dish ratings

Category level average rating

📊 Power BI Dashboard

The Power BI dashboard includes:

✔ KPI overview
✔ City level analysis
✔ Order trend visualization
✔ Category performance
✔ Restaurant performance

Dashboard file:

dashboard/swiggy_powerbi_dashboard.pbix
📌 Key Insights

Some interesting findings from the analysis:

A small number of cities generate majority of orders

Certain categories dominate order volume

Most orders fall in the ₹200-₹299 price range

Highly rated dishes correlate with higher order counts

📷 Dashboard Preview

(Add screenshots here)

Example:

images/dashboard_overview.png
images/city_analysis.png
▶️ How To Run This Project
Step 1

Clone repository

git clone https://github.com/yourusername/swiggy-food-delivery-analytics.git
Step 2

Import dataset into MySQL.

Step 3

Run SQL script

swiggy_data_warehouse.sql
Step 4

Open Power BI dashboard

swiggy_powerbi_dashboard.pbix
🎯 Skills Demonstrated

SQL Data Cleaning

Data Warehouse Design

Star Schema Modeling

Index Optimization

Analytical SQL

Business KPI Analysis

Power BI Dashboarding

Data Storytelling

👤 Author

Sapna

Aspiring Data Analyst / Data Engineer

Skills:

SQL

Power BI

Data Warehousing

Business Analytics

⭐ If you like this project

Give it a star ⭐ on GitHub!
