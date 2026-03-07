🍔Swiggy Food Delivery Analytics
Data Warehouse | SQL Analytics | Business Intelligence

📌 Project Overview

This project builds a scalable analytics solution for food delivery data, transforming raw operational records into a structured data warehouse optimized for business intelligence and decision-making.
Using 195K+ order records, the project demonstrates how real-world transactional data can be transformed into actionable insights for business strategy.

The pipeline includes:

-Data ingestion

-Data cleaning & validation

-Dimensional modeling


-Data warehouse design

-KPI generation

-Business intelligence reporting

The final system enables deep insights into revenue trends, customer behavior, restaurant performance, and geographic demand patterns.


🧠 Business Problem

Food delivery platforms like Swiggy generate large volumes of data.To scale efficiently, the business must answer critical questions:

📌Which cities generate the most revenue?

📌What food categories drive the highest demand?

📌Which restaurants perform best?

📌How do customer spending patterns vary?

📌Are there seasonal or time-based ordering trends?

However, raw transactional data is not optimized for analytics.

-Without proper data modeling:

-Queries become slow

-Business metrics are inconsistent

-Insights are difficult to extract

This project solves the problem by building a data warehouse architecture and generating business KPIs through analytical SQL queries.


🎯 Project Objectives

-Build a star schema data warehouse to support efficient analytics on food delivery data.

-Clean and transform raw transactional data into structured fact and dimension tables.

-Generate key business KPIs using optimized SQL queries.

-Analyze trends across time, location, restaurants, and cuisine categories.

-Develop a Power BI dashboard to visualize insights and support data-driven decisions.


🗂 Dataset

-Source: Food delivery dataset (Swiggy)

-Records: 197,000+

-Structured Data: 1,65,000+

-Fields: 10

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


🧠 Project Architecture

Data Source (CSV Dataset)
        ↓
Database & Data Warehouse (MySQL)
        ↓
Star Schema (Fact & Dimension Tables)
        ↓
Analytics & KPIs (SQL Queries)
        ↓
Visualization Dashboard (Power BI)


⚙️ Data Pipeline

CSV Dataset
   ↓
Data Import into MySQL
   ↓
Data Cleaning (Null checks, duplicates removal)
   ↓
Data Transformation (Date conversion, indexing)
   ↓
Data Warehouse Loading (Fact & Dimension tables)
   ↓
KPI Queries & Analysis
   ↓
Power BI Dashboard


🛠 Tech Stack

Tech Stack
||Tools	||Techniques / Usage
||MySQL 8.0||Database creation, data cleaning, SQL querying, indexing, and data warehouse implementation
||SQL	||Joins, aggregations, KPI queries, duplicate detection, and analytical business queries
||Star Schema Modeling	||Fact and dimension table design for analytical data warehouse
||Microsoft Power BI	||Power BI data modeling, DAX calculations, KPI development, interactive dashboard analytics
||github   ||Repository hosting and project documentation


🏗 Data Warehouse Design

A Star Schema was created to optimize analytical queries.

1.Dimension Tables

1.dim_date

2.dim_location

3.dim_restaurant

4.dim_category

5.dim_dish


2.Fact Table

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

📊Total Orders

SELECT COUNT(*) AS total_orders

FROM fact_swiggy_orders;

📊Total Revenue

SELECT ROUND(SUM(price_inr)/1000000,2)

AS total_revenue_inr_million

FROM fact_swiggy_orders;

📊Average Dish Price

SELECT ROUND(AVG(price_inr),2)

FROM fact_swiggy_orders;

📊Average Rating

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

✔Built an interactive dashboard in Microsoft Power BI for order and revenue analysis.

✔Implemented data modeling using relationships between fact and dimension tables.

✔Developed DAX measures for KPIs such as Total Orders, Revenue, Average Price, and Ratings.

✔Enabled interactive filtering using slicers and visuals.


📌 Key Insights

✔Analysis of 165K+ food delivery transactions enabled evaluation of customer ordering behavior, restaurant performance, and pricing patterns across multiple cities.

✔Mid-range priced meals (₹100–₹299) generate the highest order volume, indicating that affordability plays a major role in customer 
purchasing decisions.

✔Food delivery demand is highly concentrated in major urban cities, which contribute the largest share of both orders and revenue.

✔A small group of top-performing restaurants captures a significant portion of total orders, highlighting strong competition and the importance of ratings and pricing strategies.

✔Certain cuisine categories consistently attract higher order volumes and maintain strong customer ratings, indicating clear consumer preferences.

✔Dish-level analysis shows that a limited number of popular dishes drive repeat customer orders, suggesting the importance of optimized menu offerings.

✔Customer ratings are predominantly above 4 stars, indicating generally high service quality across restaurants on the platform.


🎯 Skills Demonstrated

-SQL Data Cleaning

-Data Warehouse Design

-Star Schema Modeling

-Index Optimization

-Analytical SQL

-Business KPI Analysis

-Data modeling and DAX calculations

-Power BI Dashboarding

-Data Storytelling


👤 Author

 Sapna Mehra

Aspiring Data Analyst / Data Engineer

Skills:

-SQL

-Power BI

-Data Warehousing

-Business Analytics

⭐ If you like this project


Give it a star ⭐ on GitHub!
