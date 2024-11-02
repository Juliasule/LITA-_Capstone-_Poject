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
Analysis for the Key  Metrics was performed on the Data Set using the Pivot Table; and some Excel Formula. The data set was imported to SQL for further analysis using SQL query and later the Result was imported to Power BI for visualization.

## Data Analysis and Insights
The Excel formula used to calculate the Average sales per product and Total Revenue by Region:
...Excel				
AVERAGE SALES PER PRODUCT:					
		GLOVES	200.0673854		=AVERAGEIF(Table2[Product],M3,Table2[Total Sales])
		HAT	158.8121547		=AVERAGEIF(Table2[Product],M4,Table2[Total Sales])
		JACKET	139.9395161		=AVERAGEIF(Table2[Product],M5,Table2[Total Sales])
		SHIRT	326.5635508		=AVERAGEIF(Table2[Product],M6,Table2[Total Sales])
		SHOES	308.6965274		=AVERAGEIF(Table2[Product],M7,Table2[Total Sales])
		SOCKS	121.8227763		=AVERAGEIF(Table2[Product],M8,Table2[Total Sales])
					
![image](https://github.com/user-attachments/assets/f872fc8f-e981-4cf4-a3d2-633522c97eea)

TOTAL REVENUE BY REGION					
		EAST	 485,925 		=SUMIFS(H2:H50001,D2:D50001,"East")
		NORTH	 386,900 		=SUMIFS(H3:H50002,D3:D50002,"North")
		SOUTH	 927,320 		=SUMIFS(H4:H50003,D4:D50003,"South")
		WEST	 300,345 		=SUMIFS(H5:H50004,D5:D50004,"West")
![image](https://github.com/user-attachments/assets/ab87fbbb-5618-474a-9311-9ef479683881)
...Excel

![Picot Tables SD](https://github.com/user-attachments/assets/74faba8b-93ba-4697-a612-de156480469d)


##Insights
The analysis reveals:

Seasonal Trends: Higher sales during Valentine season.
Best-Selling Products: Products with the highest transaction volume.
Customer Insights: Customer segmentation based on purchase frequency and value.

