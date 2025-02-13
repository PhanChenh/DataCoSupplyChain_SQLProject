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
  
