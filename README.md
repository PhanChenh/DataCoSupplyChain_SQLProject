# Project Title: Supply Chain Optimization: From Data to Decisions

## 📌 Project Overview:

Dataset: DataCoSupplyChainDataset from Kaggle (https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis/code)

**Noted:** Create a temporary table and filter out 2018, ensuring temporal consistency in insights and avoiding bias from incomplete data.

Efficient supply chain management is critical for business success, ensuring that products are delivered on time while optimizing costs and customer satisfaction.

## 📌 Objectives:

The objective of this project is to analyze and optimize supply chain performance by identifying key inefficiencies in order fulfillment, shipping delays, and regional sales distribution. Through data-driven insights, the project aims to improve delivery reliability, enhance customer satisfaction, and maximize profitability by addressing logistical bottlenecks, refining shipping strategies, and aligning inventory management with demand patterns.

## 🔧 Tech Stack:
- Programming: Python (Pandas, Matplotlib, Seaborn) (for visualization)
- Data Analysis: SQL (for querying)
- Tools: Jupyter Notebook

## 🛠 Project Structure:
1. Order-Related Descriptive
2.  Shipping & Delivery Performance
3.  Customer Behavior & Segmentation
4.  Product & Category Insights
5.  Inventory & Supply Chain Efficiency
6.  Key Findings & Business Recommendations

## 📌 Key Insights: 
- Order Performance: High sales, but mixed order values suggest both high- and low-ticket items. Top regions drive most revenue, while underperforming regions need attention.
- Shipping Delays: 54.81% of orders are late. First-class shipping has the most delays; standard-class is the most reliable.
- Customer Segments: Consumers drive the most revenue. Opportunities to increase retention and explore B2B or international expansion.
- Product Insights: Top products are profitable, but some items (like Sole E35) are loss-making and should be discontinued or repriced.
- Inventory & Supply Chain: High-demand products also experience frequent delays. Improve inventory management and analyze supplier lead times.
- Regional Performance: No regional delivery trends; focus on improving warehouse efficiency over regional logistics.

## 🚀 How to Run the Project
1. Clone the repository: https://github.com/PhanChenh/DataCoSupplyChain_SQLProject.git
2. Run the analysis notebooks in Jupyter or execute SQL queries.
----

## 📊 Outcome:

```sql
select * from DataCoSupplyChainDataset;
-- Verify the Column Names
SELECT COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'DataCoSupplyChainDataset';

-- Create a temporary table and filter out 2018, ensuring temporal consistency in insights and avoiding bias from incomplete data.
SELECT * 
INTO #DataCoSupplyChain
FROM DataCoSupplyChainDataset
WHERE YEAR(order_date_DateOrders) <> 2018;

SELECT COUNT(Order_Id) AS Total_Orders,
       SUM(Sales) AS Total_Sales,
       AVG(Sales) AS Avg_Order_Value,
       COUNT(DISTINCT Customer_Id) AS Unique_Customers,
       SUM(Order_Profit_Per_Order) AS Total_Profit
FROM #DataCoSupplyChain;

-- Average Shipping Delay (Actual vs. Scheduled) and On-Time Delivery Rate
SELECT 
    AVG(CAST(Days_for_shipping_real AS FLOAT)) AS Avg_Actual_Shipping_Days,
    AVG(CAST(Days_for_shipment_scheduled AS FLOAT)) AS Avg_Scheduled_Shipping_Days,
    AVG(CAST(Days_for_shipping_real AS FLOAT)) - AVG(CAST(Days_for_shipment_scheduled AS FLOAT)) AS Avg_Delay,
	COUNT(CASE WHEN Late_delivery_risk = 0 THEN 1 END) AS On_Time_Deliveries,
    (COUNT(CASE WHEN Late_delivery_risk = 0 THEN 1 END) * 100.0 / COUNT(*)) AS On_Time_Delivery_Percentage
FROM #DataCoSupplyChain;

-- Late Delivery Count
SELECT COUNT(Order_Id) AS Late_Delivery_Orders
FROM #DataCoSupplyChain
WHERE Late_delivery_risk = 1;

-- Orders by Region
SELECT Order_Region, COUNT(Order_Id) AS Total_Orders 
FROM #DataCoSupplyChain
GROUP BY Order_Region
ORDER BY Total_Orders DESC;

-- Region by Sales
SELECT Order_Region, SUM(Sales) AS Total_Sales 
FROM #DataCoSupplyChain
GROUP BY Order_Region
ORDER BY Total_Sales DESC;

-- Region by Profits
SELECT Order_Region, SUM(Order_Profit_Per_Order) AS Total_Profit 
FROM #DataCoSupplyChain
GROUP BY Order_Region
ORDER BY Total_Profit DESC;

----------
-- 2. Shipping & Delivery Performance
-- Orders by Delivery_Status with Percentage of Each Status
WITH TotalOrders AS (
    SELECT COUNT(Order_Id) AS Total_Orders
    FROM #DataCoSupplyChain
)
SELECT 
    Delivery_Status, 
    COUNT(Order_Id) AS Total_Orders,
    (COUNT(Order_Id) * 100.0 / (SELECT Total_Orders FROM TotalOrders)) AS Percentage
FROM #DataCoSupplyChain
GROUP BY Delivery_Status
ORDER BY Total_Orders DESC;

-- Late Deliveries by Region
SELECT 
    Order_Region, 
    COUNT(CASE WHEN Late_delivery_risk = 1 THEN 1 END) AS Late_Deliveries
FROM #DataCoSupplyChain
GROUP BY Order_Region
ORDER BY Late_Deliveries DESC;

-- Check Average Scheduled Shipping Days for Each Shipping Mode
SELECT 
    Shipping_Mode, 
    AVG(CAST(Days_for_shipment_scheduled AS FLOAT)) AS Avg_Scheduled_Shipping_Days
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode
ORDER BY Avg_Scheduled_Shipping_Days;
--=> as I 've checked, the shipping schedual is the same for all region, state

-- Average Shipping Time by Shipping Mode with Late Deliveries and Total Orders
SELECT 
    Shipping_Mode, 
    COUNT(*) AS Total_Orders,
    AVG(CAST(Days_for_shipping_real AS FLOAT)) AS Avg_Shipping_Days,
    COUNT(CASE WHEN Late_delivery_risk = 1 THEN 1 END) AS Late_Deliveries,
    (COUNT(CASE WHEN Late_delivery_risk = 1 THEN 1 END) * 100.0 / COUNT(*)) AS Late_Delivery_Percentage
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode
ORDER BY Avg_Shipping_Days;

-- Check how Late Delivery for shipping mode 
SELECT 
    Shipping_Mode,
    CAST(Days_for_shipping_real AS INT) AS Days_for_shipping_real,
    CAST(Days_for_shipment_scheduled AS INT) AS Days_for_shipment_scheduled,
    CAST(Days_for_shipping_real AS INT) - CAST(Days_for_shipment_scheduled AS INT) AS Shipping_Delay,
    COUNT(*) AS Total_Orders
FROM #DataCoSupplyChain
GROUP BY 
    Shipping_Mode, 
    CAST(Days_for_shipping_real AS INT), 
    CAST(Days_for_shipment_scheduled AS INT)
ORDER BY Shipping_Mode, Shipping_Delay DESC;

-- Late deliver rate by order region
SELECT 
    Shipping_Mode,
    Order_Region,
    COUNT(*) AS Total_Orders,
    COUNT(CASE WHEN Days_for_shipping_real > Days_for_shipment_scheduled THEN 1 END) AS Late_Orders,
    (COUNT(CASE WHEN Days_for_shipping_real > Days_for_shipment_scheduled THEN 1 END) * 100.0 / COUNT(*)) AS Late_Percentage
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode, Order_Region--, Customer_State
ORDER BY Shipping_Mode, Order_Region;

-- How long does order delay by each order region and customer state
SELECT 
    Shipping_Mode, 
    Order_Region, 
    Customer_State,
    AVG(CAST(Days_for_shipment_scheduled AS FLOAT)) AS Avg_Scheduled_Shipping_Days,
    AVG(CAST(Days_for_shipping_real AS FLOAT)) AS Avg_Actual_Shipping_Days,
    AVG(CAST(Days_for_shipping_real AS FLOAT)) - AVG(CAST(Days_for_shipment_scheduled AS FLOAT)) AS Avg_Delay,
    COUNT(*) AS Total_Orders
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode, Order_Region, Customer_State
ORDER BY Shipping_Mode, Order_Region, Avg_Delay DESC;

-- shipping mode by Sales
SELECT Shipping_Mode, SUM(Sales) AS Total_Sales 
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode
ORDER BY Total_Sales DESC;

-- Analyze Order Quantity vs. Delay
SELECT 
    Shipping_Mode,
    AVG(Order_Item_Quantity) AS Avg_Order_Quantity,
    SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) AS Late_Orders,
    COUNT(*) AS Total_Orders,
    (SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) * 100.0) / COUNT(*) AS Late_Delivery_Percentage
FROM #DataCoSupplyChain
WHERE Shipping_Mode IN ('Second Class', 'Same Day', 'First Class', 'Standard Class')
GROUP BY Shipping_Mode
ORDER BY Late_Delivery_Percentage DESC;

-- late rate by order month and shipping mode - Check Delays by Warehouse Load
SELECT 
    Shipping_Mode, 
    COUNT(*) AS Total_Orders, 
    SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) AS Late_Orders,
    (SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) * 100.0) / COUNT(*) AS Late_Percentage,
    FORMAT(order_date_DateOrders, 'yyyy-MM') AS Order_Month
FROM #DataCoSupplyChain
GROUP BY Shipping_Mode, FORMAT(order_date_DateOrders, 'yyyy-MM')
ORDER BY Order_Month DESC, Late_Percentage DESC;

-- late percentage of specific product
SELECT 
    Product_Name,
    COUNT(*) AS Total_Orders,
    SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) AS Late_Orders,
    AVG(Order_Item_Quantity) AS Avg_Quantity_Ordered,
    SUM(Sales) AS Total_Sales,
    (SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) * 100.0) / COUNT(*) AS Late_Percentage
FROM #DataCoSupplyChain
WHERE Shipping_Mode IN ('Second Class', 'Same Day', 'Same Day', 'First Class')
GROUP BY Product_Name
ORDER BY Late_Percentage DESC;

-- late percentage of specific category
SELECT 
    Category_Name,
    COUNT(*) AS Total_Orders,
    SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) AS Late_Orders,
    AVG(Order_Item_Quantity) AS Avg_Quantity_Ordered,
    SUM(Sales) AS Total_Sales,
    (SUM(CASE WHEN Late_delivery_risk = 1 THEN 1 ELSE 0 END) * 100.0) / COUNT(*) AS Late_Percentage
FROM #DataCoSupplyChain
WHERE Shipping_Mode IN ('Second Class', 'Same Day', 'Same Day', 'First Class')
GROUP BY Category_Name
ORDER BY Total_Orders DESC;

-----------
-- 3. Customer Behavior & Segmentation

-- Sales by Customer Segment
SELECT Customer_Segment, SUM(Sales) AS Total_Sales 
FROM #DataCoSupplyChain
GROUP BY Customer_Segment
ORDER BY Total_Sales DESC;

-- Customer Distribution by Country
SELECT Customer_Country, COUNT(DISTINCT Customer_Id) AS Total_Customers 
FROM #DataCoSupplyChain
GROUP BY Customer_Country
ORDER BY Total_Customers DESC;


---------------
-- 4. Product & Category Insights
-- Top 10 Best-Selling Product Categories by Sales
-- Top 10 Categories by Sales per Region
WITH CategoryRanking AS (
    SELECT 
        Order_Region,
        Category_Name, 
        SUM(Sales) AS Total_Sales,
        RANK() OVER (PARTITION BY Order_Region ORDER BY SUM(Sales) DESC) AS Rank
    FROM #DataCoSupplyChain
    GROUP BY Order_Region, Category_Name
)
SELECT Order_Region, Category_Name, Total_Sales
FROM CategoryRanking
WHERE Rank <= 10
ORDER BY Order_Region, Rank;

-- Top 10 Most Ordered Products by Order Region
WITH ProductRanking AS (
    SELECT 
        Order_Region,
        Product_Name, 
        SUM(Sales) AS Total_Revenue,
        RANK() OVER (PARTITION BY Order_Region ORDER BY COUNT(Order_Item_Id) DESC) AS Rank
    FROM #DataCoSupplyChain
    GROUP BY Order_Region, Product_Name
)
SELECT Order_Region, Product_Name, Total_Revenue
FROM ProductRanking
WHERE Rank <= 10
ORDER BY Order_Region, Rank;

-- Highest Profit Margin products
SELECT Product_Name, SUM (Order_Profit_Per_Order) AS Total_Profit 
FROM #DataCoSupplyChain
GROUP BY Product_Name
ORDER BY Total_Profit DESC;

--------------
-- 5. Inventory & Supply Chain Efficiency
--category
-- Inventory Turnover Rate (Sales-to-Stock Ratio)
SELECT Category_Name, COUNT(Order_Id) AS Total_Order 
FROM #DataCoSupplyChain
GROUP BY Category_Name
ORDER BY Total_Order DESC;
--=> need to arrange inventory

-- Most Frequently Late category
SELECT TOP 10 Category_Name, COUNT(Order_Id) AS Late_Deliveries 
FROM #DataCoSupplyChain
WHERE Late_delivery_risk = 1
GROUP BY Category_Name
ORDER BY Late_Deliveries DESC;

--product name
-- Inventory Turnover Rate (Sales-to-Stock Ratio)
SELECT Product_Name, COUNT(Order_Id) AS Total_Order 
FROM #DataCoSupplyChain
GROUP BY Product_Name
ORDER BY Total_Order DESC;
--=> need to arrange inventory

-- Most Frequently Late Products
SELECT TOP 10 Product_Name, COUNT(Order_Id) AS Late_Deliveries 
FROM #DataCoSupplyChain
WHERE Late_delivery_risk = 1
GROUP BY Product_Name
ORDER BY Late_Deliveries DESC;


-----------------
-- 6. Investigating why certain regions underperform.

SELECT 
    Order_Region,
    AVG(CAST(Days_for_shipping_real AS INT)) AS Avg_Actual_Shipping_Time,
    AVG(CAST(Days_for_shipment_scheduled AS INT)) AS Avg_Scheduled_Shipping_Time
FROM #DataCoSupplyChain
--WHERE Order_Region IN ('Central Asia', 'Canada', 'Southern Africa', 'Central Africa', 'East Africa')
GROUP BY Order_Region
ORDER BY Avg_Actual_Shipping_Time DESC;


-------------------------
-- filter column for power BI project
SELECT 
		Days_for_shipping_real,
		Days_for_shipment_scheduled,
		Delivery_Status,
		Late_delivery_risk,
		Shipping_Mode,
		Customer_Fname,
		Customer_Id,
		Customer_Lname,
		Customer_Segment,
		Customer_State,
		FORMAT(order_date_DateOrders, 'M/d/yyyy h:mm:ss tt') AS DateOrders,
		Order_Id,
		Order_Item_Discount_Rate,
		Order_Item_Quantity,
		Sales,
		Order_Item_Total,
		Order_Profit_Per_Order,
		Order_Item_Discount,
		Order_Region,
		Category_Name,
		Product_Name,
		Product_Price
FROM #DataCoSupplyChain;


-- cleanup
DROP TABLE #DataCoSupplyChain;
```

1. Order-Related Insights
- Total sales: 36.45M
- Total profit: 3.93M
- High total sales and profit, but an average order value of $204.3 suggests a mix of high- and low-ticket items.
- Top-performing regions (Central America, Western Europe, etc.) drive most orders and profits, while underperforming regions (Central Asia, Canada, Southern Africa, etc.) lag behind.

Recommendations:
- Expand operations in high-performing regions with targeted marketing.
- Investigate barriers in underperforming regions (logistics, demand, pricing issues).
- Customer acquisition strategy: With 18,529 unique customers, assess ways to improve retention and upselling.

2. Shipping & Delivery Performance
- On-time delivery rate is only 40.88%, 4.31% canceled, and 54.81% of orders are late.
- First-class shipping has the highest delay (95.3%), followed by second-class (76.6%). Standard-class performs best.
- Late deliveries happen across all regions, suggesting internal logistics or warehouse issues rather than regional performance issues.

Recommendations:
- Revise delivery scheduling algorithms: Adjust estimated delivery times to be more realistic.
- Improve warehouse efficiency: Since delays aren’t regional, warehouse bottlenecks may be an issue. Look at order processing times.
- Optimize shipping mode selection: Since standard-class is most reliable, encourage its use for non-urgent shipments.
- Investigate supplier delays: If certain products/categories are consistently late, supply chain issues could be the root cause.

3. Customer Behavior & Segmentation
- Consumer segment is the biggest revenue driver ($18.93M), followed by Corporate ($11.06M) and Home Office ($6.45M).
- Customers are only from the U.S. and Puerto Rico.

Recommendations:
- Segmented marketing campaigns: Since consumers drive the most sales, run loyalty programs or personalized promotions for them.
- Expand internationally: If logistics allow, expanding to neighboring countries could unlock new revenue.
- B2B sales opportunities: Corporate customers generate high revenue; create bulk-purchase incentives.

4. Product & Category Insights
- Top 5 products by profit include fitness and sports gear, while the bottom 3 are loss-making (Sole E35, Bushnell Pro X7, Sole E25).
- All regions have the same top products & categories.

Recommendations:
- Discontinue or reprice loss-making products (or negotiate better supplier pricing).
- Boost top-performing products with promotions & bundling.
- Diversify the product mix if regional demand is identical, as it may indicate lack of localized strategy.

5. Inventory & Supply Chain Efficiency
- Most-ordered products & categories are also the most frequently delayed.
- Golf Bags & Carts, Basketball, Fitness Accessories have highest late delivery rates.

Recommendations:
- Increase inventory buffer for high-demand, frequently late items.
- Analyze supplier lead times for late products—are suppliers the issue?
- Warehouse processing improvements to meet demand more efficiently.

6. Regional Performance & Warehouse Bottlenecks
- No regional trend in delivery delays.
- Shipping mode affects lateness more than location.

Recommendations:
- Improve warehouse processing speeds instead of focusing on regional logistics.
- Analyze seasonal order surges and adjust staffing/resources accordingly.

## 📬 Contact & Contributions

Feel free to fork, open issues, or suggest improvements!

📧 Email: pearriperri@gmail.com

🔗 [LinkedIn](https://www.linkedin.com/in/phan-chenh-6a7ba127a/) | Portfolio
  
