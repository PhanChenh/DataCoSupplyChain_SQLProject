# Project Title: Supply Chain Optimization – Tackling Delivery Delays and Profitability Challenges (2015-2017) 

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Objective](#objective)
- [Analysis Approach](#analysis-approach)
- [Key Findings](#key-findings)
- [How to run code](#how-to-run-code)
- [Technologies Used](#technologies-used)
- [Results & Visualizations](#results--visualizations)
- [Recommendation](#Recommendation)
- [Contact](#contact)

## Overview:

This analysis focuses on evaluating the performance of the supply chain over the period of 2015-2017, with the main goal of identifying inefficiencies, delays, and areas for optimization. The study examines key metrics such as order performance, shipping and delivery rates, regional sales and profit, product profitability, and warehouse efficiency.

The importance of this study lies in its potential to provide actionable insights that can significantly enhance supply chain operations. By understanding delivery delays, profitability trends, and regional performance, the company can improve customer satisfaction, reduce costs, and increase profitability. Ultimately, this analysis aims to provide strategic recommendations that will help optimize the supply chain, streamline operations, and support better decision-making.

## Dataset

The analysis is based on the DataCoSupplyChainDataset, obtained from Kaggle:

🔗 DataCo Smart Supply Chain Dataset
- Source: [Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis/code)
- Time Period Covered: 2015–2017 (2018 data excluded for consistency)
- Number of Records: 178396 rows
- Number of Features: 22 
- Key Variables:

  + Sales & Profitability: Sales, Sales_per_customer, Order_Item_Profit_Ratio, Order_Item_Discount, Order_Item_Discount_Rate, Order_Profit_Per_Order
  + Customer Information: Customer_Id, Customer_Segment, Customer_State
  + Order Details: Order_Id, Order Date, Order_Region, Order_Item_Quantity
  + Product Information: Category_Id, ProductN_ame, Product_Price
  + Shipping & Delivery Performance: Days_for_shipping_real, Days_for_shipment_scheduled, Delivery_Status, Late_delivery_risk, Shipping_Mode
 
## Objective

The objective of this analysis is to evaluate the supply chain's performance, identify delivery delays, regional and product profitability trends, and uncover warehouse inefficiencies, with the goal of providing actionable recommendations to optimize operations, improve customer satisfaction, and increase profitability.

## Analysis Approach
1. Data Preparation

The dataset from the DataCoSupplyChainDataset was filtered to exclude data from 2018, as it was found to be inconsistent and would introduce bias into the analysis. This step ensured temporal consistency across the years 2015–2017.

2. Exploratory Data Analysis (EDA)

Key variables like sales, orders, and delivery rates were analyzed to identify patterns, trends, and areas of concern, such as late deliveries and low-profit products.

3. Performance Analysis

KPIs such as on-time delivery rates, shipping days, and profitability were examined across shipping modes, regions, and customer segments to uncover inefficiencies and performance gaps.

4. Root Cause Identification

Analysis was conducted to determine the root causes of delays, negative profits, and regional underperformance, focusing on shipping modes and warehouse inefficiencies.

5. Segmentation and Insights

Customer segments, product categories, and shipping modes were segmented to identify performance trends and areas for improvement.

6. Recommendations

Actionable recommendations were made to optimize shipping schedules, improve warehouse operations, and refine customer strategies to boost profitability and customer satisfaction.

## Key Finding: 
-	Late Deliveries: Around 55% of orders face delivery delays, with First Class shipping particularly impacted (95.3%). Delays are consistent across regions, indicating internal process issues.
-	Profitability: Some products (e.g., Sole E25 Elliptical, Bushnell Pro X7) are unprofitable, suggesting a need for re-evaluating pricing and demand strategies.
-	Regional Insights: High sales and profits are concentrated in regions like Western Europe and Central America, while delays occur universally, indicating systemic inefficiencies.
-	Shipping Mode Issues: Standard Class has the highest sales but still faces delays (38.1%). First and Second Class suffer from severe delays, pointing to inefficiencies in shipping mode management.
-	Warehouse Bottlenecks: The delays across all shipping modes suggest that warehouse processing may be a key bottleneck.

## How to run code
1. Using SQL Server Management Studio (SSMS) to execute SQL queries
2. Run the analysis notebooks in Jupyter.

## Technologies Used
- SQL code: SQL queries were executed to extract insights from the dataset, focusing on sales, profits, orders, shipping delays, and customer behavior. Queries specifically targeted late deliveries, order values, regional performance, and product profitability.
- Python code: Extracted SQL data was saved as CSV and analyzed using Jupyter Notebook with Python. Key libraries used include Pandas for data manipulation, Seaborn and Matplotlib for data visualization.

## Results & Visualizations

![Screenshot 2025-02-17 203508](https://github.com/user-attachments/assets/85219b16-5852-42c9-bea4-e0b481ea21c3)


Figure 1: Delivery status vs. total orders and percentage result 

- Total late delivery orders: 97,782 
- Advanced shipping: 41,124 
- Shipping on time: 31,822 
- Shipping cancelled:7,668  

=> Delivery Delays: There is a significant issue with on-time deliveries, with a 40.9% on-time delivery rate, 54.8% late deliveries, and 4.3% order cancelled. Late deliveries contribute to customer dissatisfaction and potential revenue loss. 

![Screenshot 2025-02-17 203844](https://github.com/user-attachments/assets/94853754-a76c-4c4d-8b18-816fc6c97f60)


Figure 2: Shipping mode vs. total orders, and late delivery percentage 

- Same day: 45.8% 
- First class: 95.3% 
- Second class: 76.6% 
- Standard class: 38.1%

=> A major bottleneck is the high percentage of late deliveries, first Class, which has a high rate of late deliveries, should be re-examined for process inefficiencies. 

![image](https://github.com/user-attachments/assets/831c3bbb-804a-40a5-b9f1-626f88dd9b07)

Figure 3: Late rate per month in 2015

![image](https://github.com/user-attachments/assets/c5e9ab7c-6d0d-4d51-a575-2de00b239362)

Figure 4: Late rate per month in 2016

![image](https://github.com/user-attachments/assets/5caf155d-be57-4270-83bd-0bffb0da854f)

Figure 5: Late rate per month in 2017

=> Late shipment trends vary by shipping mode but show no clear pattern from 2015 to 2017. Standard Class had the lowest late percentage (38%), while First Class was the highest (95%). Second Class averaged 75%, and Same Day fluctuated between 30% and 60%.

![Screenshot 2025-02-17 204157](https://github.com/user-attachments/assets/a565e110-197c-4865-9573-9b14daffac90)

Figure 6: Customer vs. total sales

Customer segment vs. total sales: 
- Consumer: $18,932,959 
- Corporate: $11,063,676 
- Home office: $6,456,448

=> Consumer customers contribute the most in sales, followed by corporate and home office 
segments. There is room for targeting and optimizing the experience for each customer type to boost sales further. 

![Screenshot 2025-02-17 145639](https://github.com/user-attachments/assets/01045d39-5faf-4f4d-8a8f-1d6d1c011f1e)

Figure 7: Top 10 category vs. late delivery  

![Screenshot 2025-02-17 145652](https://github.com/user-attachments/assets/49bf066c-865e-486d-89d4-629d9860ff04)

Figure 8: Top 10 product vs. late delivery 

- Top Categories & Late Deliveries: Categories like Golf Bags & Carts, Basketball, and 
Fitness Accessories have high delivery late rates and also the highest order volumes, 
suggesting issues with inventory management or fulfillment processes in these categories.

- Product Profitability: Some products, like Sole E25 Elliptical and Bushnell Pro X7, have a negative profit, indicating issues either with pricing, demand, or high shipping costs. 
Analysing pricing strategy or discontinuing unprofitable products could improve margins.

- High-Volume Categories: Cleats, Men's Footwear, and Women's Apparel have the highest 
order volumes but are also frequently late. It may indicate inefficiencies in inventory 
management or supply chain processes for these categories
- Low-Volume Products: Products with fewer orders tend to have the highest delivery late 
percentages, possibly due to low inventory or poor demand forecasting. 

![Screenshot 2025-02-17 201320](https://github.com/user-attachments/assets/53961959-68f4-4792-89c5-f94ac98f8347)

Figure 9: Regional vs. late delivery

The data suggests that late deliveries are a consistent problem across all regions, so the issue likely lies in internal processes rather than regional-specific issues. This may indicate a universal need for operational improvements rather than regional adjustments. 

## Recommendation

- Improve Shipping Scheduling: Align shipping policies with realistic delivery expectations and improve the scheduling for First Class and Second Class to reduce delays.
- Optimize Warehouse Operations: Investigate and streamline warehouse workflows to minimize delays and improve inventory management.  
- Enhance Demand Forecasting: Improve forecasting to ensure timely availability of highdemand products, especially in categories like Cleats and Men’s Footwear. 
- Tailor Customer Strategies: Focus on customer segments like consumer, corporate, and home office to increase sales and retention, particularly in U.S. and Puerto Rico.
- 4. Enhance Demand Forecasting

## Contact

📧 Email: phanchenh99@gmail.com

🔗 [LinkedIn](https://www.linkedin.com/in/phan-chenh-6a7ba127a/) | [Portfolio](https://henh-phan-chenh.vercel.app/)
  
