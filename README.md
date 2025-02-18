# Project_Online_Sales
## Project Overview
#### **Project's Titles** : `Online Sales Project`
#### **Database** : `online_sales_project`
#### **Tables** : `online_sales`
This project aims to demonstrate SQL skills and techniques in data analysis specifically to explore, clean, and analyze online sales data. The project consisted of setting up a online sales database, performing exploratory data analysis (EDA), and answering business questions through specific SQL queries.

## Project Objectives
#### 1) Set Up the Database :
Prepare a database for this project from previously available data
#### 2) Data Cleaning 
identify and delete null,missing values or duplicate data from database
#### 3) Exploratory Data Analysis (EDA) 
carry out data exploration to better understand the dataset
#### 4) Business Question Analysis
Using SQL queries to answer several business questions related to this retail sales project

## STRUCTURE 
### 1) DATABASE and TABLE SET UP
+ **Database Creation** : The first step to start this project is create the database entitled **`online_sales_project3`**
+ **Tables Creation** : The table used in this project is entitled **`onlibe_sales`** which consists of several columns, such as transactions_id, transaction_date,product_category,product_name,unit_sold,Unit_price,Total_revenue,region,payment_method
```sql
create Database online_sales_project3;
create table online_sales 
(transaction_id int,
transaction_date datetime not null,
Product_category varchar(1000),
Product_name varchar(5000),
unit_sold int,
Unit_price int,
Total_revenue int,
region varchar(1000),
payment_method varchar (100));
```

### 2) Check Is There Null Values 
**Cleaning Data** : Find the null values from dataset and remove them.
```sql
select * from online_sales;
select count(*) from online_sales;
-- Check is there null value in the dataset
select count(*) is null from online_sales;
```

## 3) EDA and Project's Insight
This process is carried out by answering several questions related to the dataset with the aim of deepening understanding regarding the dataset
#### **Project Insight**
+ Explore the popularity of different product categories accross regions
+ Investigate the impact of payment methods on sales volume or revenue
+ Identify top- selling products with each category to optimize inventor and marketing strategies
+ Evaluate the performance of specific product or categories in different region to tailer marketing campaigns accoringly
#### Exploration Data Analysis(EDA)
This procces aims to get more understanding about the dataset using SQL Query
### Task1. analyze sales trend over time to identify seasonal patterns or growth oppurtunities. 
```SQL
select month(transaction_date) as month_transaction,sum(Total_revenue) as total_revenue
from online_sales
group by month_transaction
order by total_revenue desc;
```
### Task2. Explore the popularity of different product categories accross regions
```sql
select Product_category, 
region,
sum(unit_sold) as total_unit,
sum(Total_revenue) as total_revenue
from online_sales
group by Product_category, region
order by total_revenue desc;
```
### Task3. Identify top- selling products with each category to optimize inventor and marketing strategies
```sql
With Rankedproducts as (
select 
product_name,product_category,
sum(Total_revenue) as total_revenue,
RANK() over (Partition by product_category order by sum(total_revenue) desc) as Rangked
from online_sales
group by 1,2
) 
Select 
product_category, product_name, Total_revenue
from 
Rankedproducts
where Rangked = 1;
```

### Task4. Evaluate the performance of specific product or categories in different region to tailer marketing campaigns accoringly
```SQL
with SpecificProductCategory AS (
Select 
Product_name,
Product_category,
region,
sum(unit_sold) as TOTAL_UNIT,
sum(Total_revenue) as total_revenue,
Rank () OVER (PARTITION BY region order by sum(total_revenue) desc) as ranked
from online_sales
group by 1,2,3)

Select 
Product_name, 
Product_category, 
region,TOTAL_UNIT,
total_revenue
from SpecificProductCategory

where ranked = 1;
```
### Task 5. Find the product category has the highest total revenue
```sql
select Product_category
, sum(Total_revenue) as total_revenue
from online_sales 
group by 1
order by total_revenue desc
limit 1;
```
### Task 6.find the product has the highest unit sold. 
```sql
select Product_name, Product_category,
sum(unit_sold) as Total_Unit_Sold
from online_sales
group by 1,2
order by Total_Unit_Sold desc
Limit 1;
```
### Find What's product has highest sold in each category 
```sql
With ProductSold AS (
Select Product_name,
Product_category, 
sum(unit_sold) as Total_Unit_Sold, 
RANK() OVER (PARTITION BY Product_category ORDER BY sum(unit_sold) desc) as ranked
FROM online_sales
Group by 1,2
) 
Select 
Product_name,
Product_category, 
Total_Unit_Sold
from ProductSold

where ranked = 1;
```
### Task 8. Find the region that has the highest revenue for Electronic Category
```sql
select region,
Product_category, 
sum(Total_revenue) as total_revenue
from online_sales
where Product_category ='Electronics'
group by 1
order by total_revenue desc
limit 1;
```
### Task. 9 What is the favorite payment method in each region
```sql
select payment_method, 
region, 
count(transaction_id) as total_transaction 
from online_sales
group by payment_method,region
order by payment_method desc;
```

### Task 10.What the month earn the highest revenue in general
```sql
select 
MONTH(transaction_date) as month,
sum(Total_revenue) as total_revenue
from online_sales
group by MONTH(transaction_date)
Order by total_revenue desc;
```
### Task 11. Find the each product category contribution to total revenue
```sql
select Product_category, 
sum(Total_revenue) as category_revenue,
sum(Total_revenue)/sum(sum(Total_revenue)) over()*100 as category_contribution
from online_sales
group by 1
order by category_revenue desc;
```

### Task 12.What's the product that has the highest average unit price
```sql
select Product_category,Product_name,avg(Unit_price)
from online_sales
group by 1,2
order by 1,3 desc
Limit 1;
```
### Task 13. Investigate the impact of payment methods on sales volume or revenue
```sql
select
payment_method,sum(transaction_id) as sales_volume, sum(Total_revenue) as total_revenue
from online_sales
group by payment_method
order by total_revenue desc;
```

## CONCLUSION
This project is a form of direct application of the use of SQL for data analysis which consists of creating databases and tables, cleaning data, exploring and analyzing data, and answering several business questions using SQL queries. Through this project, it is hoped that we can improve our ability to process data using SQL and can help businesses make better decisions.

## AUTHOR - PUTU ARISMADI
This project is one of the projects I worked on to enhance my data analysis and processing skills using SQL.
For more information about me or if you're interested in connecting, feel free to reach out to me via:
+ LinkedIn: [Connect me in Linkedin](https://www.linkedin.com/in/putu-arismadi-103223223/)
+ Instagram: [Follow me in Instagram](https://www.instagram.com/arismadi._?igsh=MTVzdDFsZzQyaHpwbQ==)










