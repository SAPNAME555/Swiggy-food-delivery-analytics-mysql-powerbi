### ABOUT PROJECT
#PROJECT  : SWIGGY FOOD DELIVERY ANALYTICS
#OBJECTIVE : BUILD DATA WAREHOUSE AND GENERATE BUSINESS KPIs  
#DATASET SIZE : 165K+ RECORDS
#TOOLS: MYSQL80


###1. DATABASE CREATION AND USAGE

use swiggy_database5;

###2.CREATING TABLE SWIGGY_DATA1

CREATE TABLE swiggy_data1 (
    state VARCHAR(250),
    city VARCHAR(250),
    order_date text,
    restaurant_name VARCHAR(250),
    location VARCHAR(250),
    category VARCHAR(200),
    dish_name VARCHAR(250),
    price_inr DECIMAL(8,2),
    rating DECIMAL(2,1),
    rating_count INT);
  
  
###3.LOADING/IMPROTING HUGE DATA INTO TABLE
  
SHOW VARIABLES LIKE 'secure_file_priv';

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/Swiggy_Data.csv'
INTO TABLE swiggy_data1
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

###4.  MODIFYING COLUMN NAME AND DATA TYPE

ALTER TABLE swiggy_data1
ADD COLUMN order_date_new DATE;

SET SQL_SAFE_UPDATES = 0;

UPDATE swiggy_data1
SET order_date_new = STR_TO_DATE(order_date, '%d-%m-%Y');

SET SQL_SAFE_UPDATES = 1;

SELECT order_date, order_date_new
FROM swiggy_data1
LIMIT 10;

ALTER TABLE swiggy_data1
DROP COLUMN order_date;

alter table swiggy_data1
change order_date_new order_date date;

ALTER TABLE swiggy_data1
MODIFY order_date DATE
AFTER city;
select count(*) from swiggy_data1;


###5.DATA CLEANING AND VALIDATION


# 1.NULL CHECK

 SELECT
    SUM(state IS NULL) AS state_nulls,
    SUM(city IS NULL) AS city_nulls,
    SUM(order_date IS NULL) AS order_date_nulls,
    SUM(restaurant_name IS NULL) AS restaurant_name_nulls,
    SUM(location IS NULL) AS location_nulls,
    SUM(category IS NULL) AS category_nulls,
    SUM(dish_name IS NULL) AS dish_name_nulls,
    SUM(price_inr IS NULL) AS price_nulls,
    SUM(rating IS NULL) AS rating_nulls,
    SUM(rating_count IS NULL) AS rating_count_nulls
FROM swiggy_data1;


#2. BLANK OR EMPTY STRINGS

SELECT
    SUM(TRIM(state) = '') AS state_blanks,
    SUM(TRIM(city) = '') AS city_blanks,
    SUM(TRIM(restaurant_name) = '') AS restaurant_name_blanks,
    SUM(TRIM(location) = '') AS location_blanks,
    SUM(TRIM(category) = '') AS category_blanks,
    SUM(TRIM(dish_name) = '') AS dish_name_blanks
FROM swiggy_data1;

#3.DUPLICATE DETECTION

SELECT COUNT(*) AS dup_rows
FROM swiggy_data1 t1
WHERE EXISTS (
    SELECT 1
    FROM swiggy_data1 t2
    WHERE
        t1.state = t2.state
        AND t1.city = t2.city
        AND t1.restaurant_name = t2.restaurant_name
        AND t1.dish_name = t2.dish_name
        AND t1.price_inr = t2.price_inr
        AND t1.rating = t2.rating
        AND t1.rating_count = t2.rating_count
        AND t1.order_date > t2.order_date
);

#4.DELETE DUPLICATION AND CREATING INDEX FOR OPTIMAL PERFORMNACE WITHOUT ERROR

CREATE INDEX idx_dup
ON swiggy_data1 (
    state(20),
    city(30),
    restaurant_name(50),
    dish_name(50),
    price_inr,
     rating,
    rating_count,
    order_date
);

set sql_safe_updates=0;

DELETE t1
FROM swiggy_data1 t1
JOIN swiggy_data1 t2
  ON t1.state = t2.state
 AND t1.city = t2.city
 AND t1.restaurant_name = t2.restaurant_name
 AND t1.dish_name = t2.dish_name
 AND t1.price_inr = t2.price_inr
 AND t1.rating = t2.rating
 AND t1.rating_count = t2.rating_count
 AND t1.order_date > t2.order_date;
 
 SET sql_safe_updates = 1;
 
 select count(*) from swiggy_data1;
 
 ###6. CREATING STAR SCHEMA FOR FAST AND IMPROVED QUERY PERFORMANCE

#1.CREATING DIMENSION TABLE

#1.DATE TABLE

create table dim_date
(date_id int auto_increment primary key,
full_date date,
year int,
month int,
month_name varchar(20),
quarter int,
day int,
week int);

#2.DIM_LOCATION
create table dim_location (
location_id int auto_increment primary key,
state varchar(100),
city varchar(100),
location varchar(200));

#3.DIM_RESTAURANT
create table dim_restaurant(
restaurant_id int auto_increment primary key,
restaurant_name varchar(200));

#4.DIM_CATEGORY
create table dim_category(
category_id int auto_increment primary key,
category varchar(200));

#5.DIM_DISH
create table dim_dish(
dish_id int auto_increment primary key,
dish_name varchar(200));

#2.FACT TABLE

CREATE TABLE fact_swiggy_orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,

    date_id INT,
    price_inr DECIMAL(10,2),
    rating DECIMAL(4,2),
    rating_count INT,

    location_id INT,
    restaurant_id INT,
    category_id INT,
    dish_id INT,

    CONSTRAINT fk_date
        FOREIGN KEY (date_id)
        REFERENCES dim_date(date_id),

    CONSTRAINT fk_location
        FOREIGN KEY (location_id)
        REFERENCES dim_location(location_id),

    CONSTRAINT fk_restaurant
        FOREIGN KEY (restaurant_id)
        REFERENCES dim_restaurant(restaurant_id),

    CONSTRAINT fk_category
        FOREIGN KEY (category_id)
        REFERENCES dim_category(category_id),

    CONSTRAINT fk_dish
        FOREIGN KEY (dish_id)
        REFERENCES dim_dish(dish_id)
) ENGINE=InnoDB;

#3.INSERT DATA INTO DIMENSION TABLE

#1.DIM_DATE
INSERT INTO dim_date
(
    full_date,
    year,
    month,
    month_name,
    quarter,
    day,
    week
)
SELECT DISTINCT
    order_date AS full_date,
    YEAR(order_date) AS year,
    MONTH(order_date) AS month,
    MONTHNAME(order_date) AS month_name,
    QUARTER(order_date) AS quarter,
    DAY(order_date) AS day,
    WEEK(order_date, 1) AS week
FROM swiggy_data1
WHERE order_date IS NOT NULL;
select * from dim_date;

#2.DIM_LOCATION
 insert into  dim_category(category)
 select distinct 
 category from swiggy_data1;
 
 #3.DIM_DISH
 insert into dim_dish(dish_name)
 select distinct dish_name from swiggy_data1;
 
 #4.DIM_LOCATION
 insert into dim_location(state,city,location)
 select distinct 
 state,city,location
 from swiggy_data1;
 
 #5.DIM_RESTAURANT
 insert into dim_restaurant(restaurant_name)
 select distinct restaurant_name 
 from swiggy_data1;
 
 #4.INSERT DATA INTO FACT TABLE
 
 #1.CREATE INDEXS FOR SWIGGY_DATA1- FAST PERFORMANCE/HANDLING HUGE DATA
 
CREATE INDEX idx_swiggy_date ON swiggy_data1(order_date);
CREATE INDEX idx_swiggy_location ON swiggy_data1(state, city, location);
CREATE INDEX idx_swiggy_restaurant ON swiggy_data1(restaurant_name);
CREATE INDEX idx_swiggy_category ON swiggy_data1(category);
CREATE INDEX idx_swiggy_dish ON swiggy_data1(dish_name);

#2.CREATE INDEXES FOR DIMENSION TABLES- FAST PERFORMANCES WITH JOINS

CREATE UNIQUE INDEX idx_dim_date_full_date ON dim_date(full_date);
CREATE UNIQUE INDEX idx_dim_location ON dim_location(state, city, location);
CREATE UNIQUE INDEX idx_dim_restaurant ON dim_restaurant(restaurant_name);
CREATE UNIQUE INDEX idx_dim_category ON dim_category(category);
CREATE UNIQUE INDEX idx_dim_dish ON dim_dish(dish_name);



#3.INSERT DATA INTO fact_ swiggy_orders

 INSERT INTO fact_swiggy_orders
(date_id,
    price_inr,
    rating,
    rating_count,
    location_id,
    restaurant_id,
    category_id,
    dish_id
)
SELECT
    dd.date_id,
    s.price_inr,
    s.rating,
    s.rating_count,
    dl.location_id,
    dr.restaurant_id,
    dc.category_id,
    dsh.dish_id
FROM swiggy_data1 s
JOIN dim_date dd
    ON dd.full_date = s.order_date
JOIN dim_location dl
    ON dl.state = s.state
   AND dl.city = s.city
   AND dl.location = s.location
JOIN dim_restaurant dr
    ON dr.restaurant_name = s.restaurant_name
JOIN dim_category dc
    ON dc.category = s.category
JOIN dim_dish dsh
    ON dsh.dish_name = s.dish_name;
    
    
select count(*) from swiggy_data1;
select  * from fact_swiggy_orders;
 
 
 select * from fact_swiggy_orders f
 join dim_category dc on f.category_id=dc.category_id
 join dim_date d on f.date_id=d.date_id 
 join dim_dish di on f.dish_id=di.dish_id
 join dim_location l on f.location_id=l.location_id
 join dim_restaurant r on f.restaurant_id=r.restaurant_id;
 
 select * from fact_swiggy_orders;
 select * from swiggy_data1;
 
 ####7.KPIs
 
 
 #1. TOTAL ORDERS
 Select count(*) as total_orders from fact_swiggy_orders;
 
 #2.TOTAL REVENUE(INR MILLION)
 select round(sum(price_inr)/1000000,2) as total_revenue_inr_million
 from fact_swiggy_orders;
 
 #3.AVERAGE DISH PRICE
 select round(avg(price_inr),2) avg_dish_price
 from fact_swiggy_orders;
 
 #4.AVERAGE RATING
 select round(avg(rating),2) avg_rating
 from fact_swiggy_orders;
 
###DEEP DIVE BUSINESS ANALYSIS

#5.DATE BASED ANALYSIS
 

#1.MONTHLY ORDER TRENDS
 SELECT
    dd.year,
    dd.month,
    dd.month_name,
    COUNT(f.order_id) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date dd
    ON f.date_id = dd.date_id
GROUP BY
    dd.year,
    dd.month,
    dd.month_name
ORDER BY
    dd.year,
    dd.month;

#2.QUARTERLY ORDER TRENDS
SELECT
    dd.year,
    dd.quarter,
    COUNT(f.order_id) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date dd
    ON f.date_id = dd.date_id
GROUP BY
    dd.year,
    dd.quarter
    order by 
    dd.quarter;
    
#3.YEARLY TRENDS
SELECT
    dd.year,
    COUNT(f.order_id) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date dd
    ON f.date_id = dd.date_id
GROUP BY
    dd.year;
    
#4.ORDERS BY DAY OF WEEK(MON-SUN)
 
SELECT
    DAYNAME(dd.full_date) AS day_of_week,
    COUNT(f.order_id) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date dd
    ON f.date_id = dd.date_id
GROUP BY
    DAYNAME(dd.full_date)
ORDER BY
    total_orders DESC;
    
###6.LOCATION BASED ANALYSIS

#1.TOP 10 CITIES BY ORDER VOLUME

select l.city,
 l.state,count(f.order_id) total_orders
 from fact_swiggy_orders f 
 join dim_location l
 on l.location_id = f.location_id
group by l.state,l.city 
order by total_orders desc
limit 10;

#2.TOP 10 CITIES BY REVENUE
 select l.city,
 l.state, round(sum(f.price_inr),0) total_revenue
 from fact_swiggy_orders f 
 join dim_location l
 on l.location_id = f.location_id
group by l.state,l.city 
order by total_revenue desc
limit 10;

#3.REVENUE CONTRIBUTION BY STATES
select 
 l.state, round(sum(f.price_inr),0) total_revenue
 from fact_swiggy_orders f 
 join dim_location l
 on l.location_id = f.location_id
group by l.state
order by total_revenue desc;


###7.FOOD PERFORMANCE


#1.TOP 10 RESTAURANTS BY ORDER
select r.restaurant_name, count(* ) total_order from
fact_swiggy_orders f join dim_restaurant r on
f.restaurant_id=r.restaurant_id 
group by restaurant_name 
order by total_order desc
limit 10;

#2.TOP CATEGORIES BY ORDER VOLUME
select c.category, count(* ) total_order from
fact_swiggy_orders f join dim_category c on
f.category_id=c.category_id
group by category
order by total_order desc
limit 10;

#3.MOST ORDERED DISHES
select d.dish_name, count(* ) total_order from
fact_swiggy_orders f join dim_dish d on
f.dish_id=d.dish_id
group by dish_name
order by total_order desc;

###8.CUISINE/CATEGORY PERFORMANCE

#1.TOP CATEGORY BY RATING

SELECT
    dc.category AS cuisine,
    COUNT(f.order_id) AS total_orders,
    ROUND(AVG(f.rating), 2) AS avg_rating
FROM fact_swiggy_orders f
JOIN dim_category dc
    ON f.category_id = dc.category_id
GROUP BY
    dc.category
ORDER BY
    total_orders DESC;
    
###9.CUSTOMER SPENDING INSIGHTS
   
#1.TOTAL ORDERS BY PRICE RANGE

    SELECT
    CASE
        WHEN price_inr < 100 THEN 'Under 100'
        WHEN price_inr BETWEEN 100 AND 199 THEN '100 - 199'
        WHEN price_inr BETWEEN 200 AND 299 THEN '200 - 299'
        WHEN price_inr BETWEEN 300 AND 499 THEN '300 - 499'
        ELSE '500+'
    END AS price_range,
    COUNT(order_id) AS total_orders
FROM fact_swiggy_orders
GROUP BY
    CASE
        WHEN price_inr < 100 THEN 'Under 100'
        WHEN price_inr BETWEEN 100 AND 199 THEN '100 - 199'
        WHEN price_inr BETWEEN 200 AND 299 THEN '200 - 299'
        WHEN price_inr BETWEEN 300 AND 499 THEN '300 - 499'
        ELSE '500+'
    END
ORDER BY
    total_orders DESC;
   
###10.RATING ANALYSIS
    
#1.RATING COUNT DISTRIBUTION
select rating,
count(*) rating_count from fact_swiggy_orders
group by rating
order by  rating_count desc;


