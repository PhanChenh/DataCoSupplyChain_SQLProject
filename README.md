# Project Title: Supply Chain Optimization – Tackling Delivery Delays and Profitability Challenges (2015-2017) 

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Objective](#objective)
- [Analysis Approach](#analysis-approach)
- [Key Findings](#key-findings)
- [How to Use](#how-to-use)
- [Technologies Used](#technologies-used)
- [Results & Visualizations](#results--visualizations)
- [Contributing](#contributing)
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

## How to use
1. Using SQL Server Management Studio (SSMS) or another SQL Client to execute SQL queries
2. Run the analysis notebooks in Jupyter.

## Technologies Used
- SQL code: SQL queries were executed to extract insights from the dataset, focusing on sales, profits, orders, shipping delays, and customer behavior. Queries specifically targeted late deliveries, order values, regional performance, and product profitability.
- Python code: Extracted SQL data was saved as CSV and analyzed using Jupyter Notebook with Python. Key libraries used include Pandas for data manipulation, Seaborn and Matplotlib for data visualization and generating charts to

## Results & Visualizations

![Screenshot 2025-02-17 144025](https://github.com/user-attachments/assets/b7646344-bbf4-4e83-a152-6aa4ea15f20d)

Figure 1: Delivery status vs. total orders and percentage result 

- Total late delivery orders: 97,782 
- Advanced shipping: 41,124 
- Shipping on time: 31,822 
- Shipping cancelled:7,668  

=> Delivery Delays: There is a significant issue with on-time deliveries, with a 40.9% on-time delivery rate, 54.8% late deliveries, and 4.3% order cancelled. Late deliveries contribute to customer dissatisfaction and potential revenue loss. 

![Screenshot 2025-02-17 144011](https://github.com/user-attachments/assets/ffacb64e-3658-456c-b7e0-a72189c6bb41)

Figure 2: Shipping mode vs. total orders, and late delivery percentage 

- Same day: 45.8% 
- First class: 95.3% 
- Second class: 76.6% 
- Standard class: 38.1%

=> A major bottleneck is the high percentage of late deliveries, first Class, which has a high rate of late deliveries, should be re-examined for process inefficiencies. 

![Screenshot 2025-02-17 144825](https://github.com/user-attachments/assets/74be5e82-1faa-4c2f-9a1c-ffb40d2961bd)

Figure 3: Customer vs. total sales

Customer segment vs. total sales: 
- Consumer: $18,932,959 
- Corporate: $11,063,676 
- Home office: $6,456,448

=> Consumer customers contribute the most in sales, followed by corporate and home office 
segments. There is room for targeting and optimizing the experience for each customer type to boost sales further. 

![Screenshot 2025-02-17 145639](https://github.com/user-attachments/assets/01045d39-5faf-4f4d-8a8f-1d6d1c011f1e)

Figure 4: Top 10 category vs. late delivery 

![Screenshot 2025-02-17 145652](https://github.com/user-attachments/assets/49bf066c-865e-486d-89d4-629d9860ff04)

Figure 5: Top 10 product vs. late delivery 

## Contact

📧 Email: pearriperri@gmail.com

🔗 [LinkedIn](https://www.linkedin.com/in/phan-chenh-6a7ba127a/) | Portfolio
  
