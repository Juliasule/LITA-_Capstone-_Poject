# LITA-_Capstone-_Poject
This Capstone contains two projects namely: 
- Project 1:Retail Store Sales Performance Analysis
- Project 2: Customer Segmentation for a Subscription Service
We will analyze these two projects in detail and highlight some projects performed as part of my Learning experience with INCUBATOR HUB.

## Table of Contents

[Project Overview](#project-overview)

[Features](#features)

[Data Source](#data-source)

[Tools Used](#tools-used)

[Data Cleansing and Preparation](#data-cleaning-and-preparation)

[Key Metrics](key-metrics)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

...
# Project 1: Retail Store Sales Performance Analysis
This project analyzes sales data from a retail store to uncover trends, measure key performance indicators (KPIs), and provide insights to improve sales and profitability. The analysis includes detailed reports on product performance, seasonal trends, and customer behavior.

## Project Overview

Retail businesses rely on data-driven decisions to stay competitive. This project provides an in-depth sales performance analysis, focusing on metrics such as monthly revenue trends, product category performance, and customer purchasing behavior. Insights gained here can help optimize marketing strategies, improve inventory management, and enhance overall customer satisfaction.

## Features

The dataset used in this analysis includes:
- **Order Date**: Date of each sale
- **Order ID**: Unique identifier for each order
- **Product**: Category of each product sold
- **Quantity Sold**: Number of units sold per transaction
- **Unit Price**: Price per unit of the product
- **Customer ID**: Unique identifier for each customer
- **Region**: Geographical area where the shop is located
- **Sales**: sale made by each product

## Data Source
The dataset was obtained from (theincubatorhub.org] LITA Bootcamp


## Tools Used [Download Here](https://www.microsoft.com)
- Microsoft Excel for:
  1. Data cleaning
  2. Data Analysis
  3. Data Visualization
- SQL for Data query
- Power BI: for visualization
- GitHub for portfolio building.

 ## Data Cleansing and Preparation
In the initial phase of data cleaning and preparations, we perform the following actions:
- Data loading and inspection.
- Handling missing variables.
- Removal of Duplicates.
- Data cleaning and formatting.
The cleaned Data set was saved as SALESDATA.csv

## Key Metrics

The analysis focuses on several KPIs critical for understanding retail sales performance:

- **Monthly Sales Trend**: Monthly revenue and growth rate.
- **Top Performing Products**: Products that generate the highest sales and profit.
- **Customer Purchase Behavior**: Average spend per customer and purchase frequency.
- **Sales by Product Category**: Distribution of sales across different product categories.
- **Average Sales per product**: sales contributed averagely per product.
- **Total Revenue by Region**: Revenue contributed by each Region
- **Percentage of Total sales by Region**: Percentage of the total sales contributed by each Region.
- **Top 5 Customers**: Top 5 Customers by their purchasing power. 

## Exploratory Data Analysis
The data set for the key metrics was analyzed using a pivot table and some Excel formulas. The data set was then imported to SQL for further analysis using an SQL query, and later, the Result was imported to Power BI for visualization.

## Data Analysis and Insights
The Excel formula used to calculate the Average sales per product and Total Revenue by Region:
...Excel				
					
![image](https://github.com/user-attachments/assets/f872fc8f-e981-4cf4-a3d2-633522c97eea)



![image](https://github.com/user-attachments/assets/ab87fbbb-5618-474a-9311-9ef479683881)

...Excel


### Pivot Tables
![Picot Tables SD](https://github.com/user-attachments/assets/74faba8b-93ba-4697-a612-de156480469d)

### SQL Queries

```SQL

SELECT * FROM SALESDATA
-----TOTAL SALES FOR EACH PRODUCT CATEGORY
SELECT Product, SUM(Sales) AS Total_Sales
FROM SALESDATA
GROUP BY Product
ORDER BY Total_Sales DESC

-------NUMBER OF SALES TRANSACTION BY REGION----
SELECT Region, COUNT(OrderID) AS transaction_count
FROM SALESDATA
GROUP BY Region
ORDER BY transaction_count DESC;

-------HIGHEST SELLING PRODUCT BY TOTAL SALES VALUE----
SELECT product, Total_sales
FROM (
    SELECT product, SUM(Sales) AS Total_sales
    FROM SALESDATA
    GROUP BY product
) AS product_sales
WHERE Total_sales = (SELECT MAX(total_sales) FROM (
    SELECT SUM(saleS) AS total_sales
    FROM SALESDATA
    GROUP BY product
) AS Highest_selling_product);

------MONTHLY SALES TOTAL FOR YEAR 2024----
SELECT MONTH(OrderDate) AS month, SUM(sales) AS total_sales
FROM SALESDATA
WHERE YEAR(OrderDate) = 2024
GROUP BY MONTH(OrderDate)
ORDER BY month;
----MONTHLY SALES FOR CURRENT YEAR OPTION B----
SELECT Month(OrderDate) AS month, SUM(Sales) AS Monthly_Sales
FROM SALESDATA
WHERE Year(OrderDate) = Year(GETDATE())
GROUP BY Month(OrderDate)
ORDER BY Month(OrderDate)

-----TOP 5 CUSTOMERS BY TOTAL PURCHASE AMOUNT-------
SELECT TOP 5 Customer_Id, Sum(Sales) AS Total_Purchase_Amount
FROM SALESDATA
GROUP BY Customer_Id
ORDER BY Total_Purchase_Amount DESC 

------PERCENTAGE CONTRIBUTED BY EACH REGION-------
SELECT 
    region,
    SUM(sales) AS total_sales,
    (SUM(sales) * 100.0 / (SELECT SUM(sales) FROM SALESDATA)) AS sales_percentage
FROM 
    SALESDATA
GROUP BY 
    region;


-----OPTION 2----
SELECT 
    region,
    SUM(Sales) AS total_sales,
    (SUM(Sales) * 100.0 / SUM(SUM(Sales)) OVER ()) AS sales_percentage
FROM 
    SALESDATA
GROUP BY 
    region;

----PRODUCTS WITH NO SALES IN THE LAST QUATER---

SELECT DISTINCT product
FROM SALESDATA
WHERE product not in (
SELECT Product FROM SALESDATA
WHERE OrderDate >= DATEADD(quarter, -1, GETDATE())
and OrderDate< GETDATE())


--------------------------------------------
-------CUSTOMER DATA ANALYSIS----------
---------------------------------------------------
SELECT* FROM Customerdata;

------TOTAL NUMBER OF CUSTOMER BY REGION-----
SELECT Region, COUNT(customerID) AS total_customers
FROM Customerdata
GROUP BY Region;

-----MOST POPULAR SUBSCRIPTION TYPE---
SELECT TOP 1  subscriptiontype, COUNT(customerID) AS customer_count
FROM Customerdata
GROUP BY subscriptiontype
ORDER BY customer_count DESC;

------CUSTOMERS WHO CANCELED BY 6 MONTHS-----
SELECT customerID
FROM Customerdata
WHERE Canceled = 'TRUE'
AND SubscriptionEnd >= DATEADD(MONTH, -6, GETDATE());

------OPTION B-----
SELECT customerID
FROM Customerdata
WHERE Canceled = 'TRUE'
AND SubscriptionEnd >= DATEADD(MONTH, -6, GETDATE());


-----------AVERAGE SUBSCRIPTION DURATION-------

SELECT AVG(DATEDIFF(DAY, subscriptionstart, subscriptionend)) AS average_duration
FROM Customerdata
WHERE subscriptionend IS NOT NULL;

-------SUBSCRIPTION EXCEEDING 1 YEAR-----
SELECT Count(customerID)
FROM CUSTOMERDATA
WHERE DATEDIFF(DAY, subscriptionstart, subscriptionend) > 365
AND SUBSCRIPTIONEND IS NOT NULL

-----option b----
SELECT CustomerID
FROM CustomerData
WHERE Subcription_Duration > 12;


-------TOTAL REVENUE BY SUBSCRIPTION TYPE-----
SELECT SubscriptionType, sum(Revenue) AS Total_Revenue
From Customerdata
GROUP BY SubscriptionType;

------TOP 3 REGION BY SUBSCRIPTION CANCELED------

SELECT TOP 3 Region
FROM Customerdata
WHERE (Canceled = 'TRUE') 
GROUP BY Region;


-------TOP 3 REGION WITH CANCELLATION-----
SELECT  TOP 3 Region, COUNT(*) AS cancellation_count
FROM CustomerData
WHERE Canceled = 'TRUE'
GROUP BY region
ORDER BY cancellation_count DESC;

-------NUMBERS OF ACTIVE AND CANCELED SUBSCRIPTION-----
SELECT 
    SUM(CASE WHEN Canceled = 'FALSE' THEN 1 ELSE 0 END) AS active_count,
    SUM(CASE WHEN Canceled = 'TRUE' THEN 1 ELSE 0 END) AS canceled_count
FROM 
    CustomerData;
```
### Insights
The analysis reveals:
- The Region with the **highest Total sales is the South with 927,820**
- Seasonal Trends: Higher sales are noticed in February which might be due to the Valentine's celebrations, as people are buying gifts for their loved ones
- Best-Selling Products:  The Product with the highest transaction volume is **Hats** with a Total volume of **15,929** interestingly when it comes to Total sales the product with the highest Total is **Shoes** with a **total sales of 3,087,500** against **Hat is 316,195**. That is although the product **Hats** sold more quantity it ranked third in Total Sales contributed.
- Customer Insights: Customer segmentation based on purchase frequency and value is noticed throughout the Regions. The **Westerners** are buying more Hats with Total sales of **174300** probably due to their weather.
and peak period in the months of **April and August** both in 2023 and 2024. however the **Southerners** are buying more of **Shoes** with Total sales of **546,300**
















The analysis reveals:

Seasonal Trends: Higher sales during Valentine's season.
Best-Selling Products: Products with the highest transaction volume.
Customer Insights: Customer segmentation based on purchase frequency and value.

