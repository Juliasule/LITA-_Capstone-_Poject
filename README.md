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
```Excel				
					
	AVERAGE SALES PER PRODUCT:					
			GLOVES	200.0673854		=AVERAGEIF(Table2[Product],M3,Table2[Total Sales])
			HAT	158.8121547		=AVERAGEIF(Table2[Product],M4,Table2[Total Sales])
			JACKET	139.9395161		=AVERAGEIF(Table2[Product],M5,Table2[Total Sales])
			SHIRT	326.5635508		=AVERAGEIF(Table2[Product],M6,Table2[Total Sales])
			SHOES	308.6965274		=AVERAGEIF(Table2[Product],M7,Table2[Total Sales])
			SOCKS	121.8227763		=AVERAGEIF(Table2[Product],M8,Table2[Total Sales])
				1255.901911		=SUM(N3+N4+N5+N6+N7+N8)
						
						
	TOTAL REVENUE BY REGION					
			EAST	 485,925 		=SUMIFS(H2:H50001,D2:D50001,"East")
			NORTH	 386,900 		=SUMIFS(H3:H50002,D3:D50002,"North")
			SOUTH	 927,320 		=SUMIFS(H4:H50003,D4:D50003,"South")
			WEST	 300,345 		=SUMIFS(H5:H50004,D5:D50004,"West")
						

```


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

```
### Insights
The analysis reveals:
- The Total Sales by all Regions in 2023 and 2024 is **2,101,090**
- The Region with the **highest Total sales is the South with 927,820**
  
- Seasonal Trends: Higher sales are noticed in **February** in both 2023 and 2024 with Total Sales of **247,500 and **298,800** respectively which might be due to Valentine's celebrations, as people are buying gifts for their loved ones.
- Best-Selling Products: The Product with the highest transaction volume is **Hats**, with a Total volume of **15,929**. However, regarding Total sales, the product with the highest Total Sales is **Shoes**, with a **total sales of 613,380** against **Hats's 316,195**. Although the product **Hats** sold more, it ranked third in Total Sales contributed.
  
- Customer Insights: Customer segmentation based on purchase frequency and value is noticed throughout the Regions. The **Westerners** are buying more Hats with Total sales of **174300** probably due to their weather. Peak period in the months of **April and August** both in 2023 and 2024 is noticed in this region. however the **Southerners** are buying more of **Shoes** with Total sales of **546,300**. While the **Northerners** who are buying more shirts seem not to be seasonal shoppers with only high sales seen in the month of **January with Total Sales of 198,400**. The **Easterners** who favor **Shirts** with Total sales of **237,600** seem not to have a season of shopping as fluctuations can be seen throughout the year.


## Data Visualization

### Excel Dashboard


![DashBoard SD](https://github.com/user-attachments/assets/a3f0a5bb-d045-41d9-aab7-3a40a3da4cd6)



### Power BI Dashboard

![POWER BI DASHBOARD](https://github.com/user-attachments/assets/79468aa5-fa61-489c-92f3-70b9821df754)


![POWER BI DASHBOARD 2](https://github.com/user-attachments/assets/f0a3014e-2102-458f-995a-fc85dd343478)


## project 2: Customer Segmentation for a Subscription Service

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
# Project 2: Customer Segmentation for a Subscription Service

## Project Overview
This project involves analyzing customer data for a subscription service to identify segments, track subscription types, and detect trends in cancellations and renewals. By understanding customer behavior, we can provide actionable insights to improve retention, manage churn, and target customers more effectively.

## Features

The dataset used in this analysis includes:
- **Customer ID**: Unique identifier for each Customer.
- **Subscription Type**: Category of each Subscription.
- **Subscription Start**: start date for subscription.
- **Subscription End**: Expiration date or end date of subscription.
- **Subscription Duration**: Revenue made by each Subscription Type.
- **Canceled**: Subscription Status.
- **Customer Name**: Names of customer.
- **Region**: Geographical area where the shop is located.
- **Revenue**: Revenue made by each Subscription Type.
  

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
- **The most popular subscription Type**: Subscription Type that generates the highest sales and profit.
- **Customer subscription Partten**: Average spend per customer and subscription frequency.
- **Average Subscription Duration**:  Average Duration of Subscription.
- **Total Revenue by Region**: Revenue contributed by each Region
- **Total revenue by subscription type**: Total Revenue generated by subscription type.
- **Top 3 regions by subscription cancellations**:Regions with the highest numbers of subscription cancellations
- **Number of customers by Region**: Percentage of the total sales contributed by each Region.
   

## Exploratory Data Analysis
The data set for the key metrics was analyzed using a pivot table and some Excel formulas. The cleaned data set was then imported to SQL for further analysis using  SQL query, and later, the Result was imported to Power BI for visualization.

## Data Analysis and Insights
```SQL
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
### Pivot Tables




![CD PIVOT](https://github.com/user-attachments/assets/08e307f2-7c59-42d0-ba0c-23e0a2b39fb1)


![CD PIVOT 2](https://github.com/user-attachments/assets/538248b4-a2f5-45f0-bf67-9eaa7130ebf7)

### Insights
The analysis reveals: Insights on customer behavior, segment profiles, and suggestions for improving retention and reducing churn.
Some notable ones are:
- **Customer segmentation**: This is done based on Regionusing RFM ( Recency, Frequency, and Monetary). The number of customers per Region is **East (8488)**, **South (8446)**, **North (8446)**, and **West (8420)** from the highest to the lowest.
- The Top 3 regions by subscription Cancellation are **North (5067) Inactive and (3366) Active** subscriptions, **South (5064) Inactive and (3382) Active** subscriptions, and **West (5044) Inactive and (3376) Active** subscriptions, while **East with (8488) Active** subscriptions had no cancellations.
- All Regions contributed  equally, with a Total Revenue of **17M** each.
- The most popular **subscription Type** is **Basic** with Total Revenue of **34M** followed by **Premium and Standard with a Total Revenue of **16.9M** each.
- **Subscription Pattern and Trend**: The **Average subscription Duration by customer is **365 days** which is equivalent to 1 year.
- Total number of **Active and Inactive subscriptions is **18612 and 15175** respectively.
- **20** Customers had their subscription exceeding 1 year'
- **3385** customers canceled in 6 months of subscription, this might be due to poor service delivery or after-sales customer service.

## Data visualization
### Power BI Dashboard

![CD DASHBOARD](https://github.com/user-attachments/assets/536de783-aabd-4954-9c77-0a7d48caa463)
![CD DASHBOARD 2](https://github.com/user-attachments/assets/90f4f621-784d-41f1-b0f6-69ae30b39320)

## Highlights of some class Projects
### Map Data
Map of Nigeria showing the Population of Nigeria in 2019 which is **196M**


![MAP SNIP](https://github.com/user-attachments/assets/c3787dcf-f126-4ff6-b921-14681025ea42)

###HR DATA

![HR DATA DASHBOARD](https://github.com/user-attachments/assets/df2b8c03-0b3d-4072-b949-b1588d18e0f7)
![HR DATA DASHBOARD  1png](https://github.com/user-attachments/assets/a5d45e0c-82e5-44d4-be2e-94f65a2bf942)
