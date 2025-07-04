**Customer & Product Behavior Analysis**

This repository contains a comprehensive analysis of customer and product behavior based on transactional sales data. The primary goal is to derive actionable insights by segmenting customers and evaluating product performance. The analysis is conducted using SQL to process raw sales data and generate summary reports.

**Table of Contents**

- [Project Description]
- [Data Model]
- [Analysis Methodology]
- [Key Report Findings]
  - [Customer Segmentation Report]
  - [Product Performance Report]
- [How to Reproduce the Analysis]
- [Files in this Repository]
  
**Project Description**

The purpose of this project is to understand the purchasing patterns of customers and the sales performance of products. By analyzing metrics such as order frequency, sales value, and customer lifespan, we can identify our most valuable customers and top-performing products. This information is critical for making informed business decisions related to marketing, inventory management, and sales strategy.

**Data Model**

The analysis is based on a simple star schema consisting of one fact table and two dimension tables:

- **gold.fact_sales (Fact Table):** Contains all transactional data.
  - order_number: A unique identifier for each transaction.
  - product_key: Foreign key linking to the dim_products table.
  - customer_key: Foreign key linking to the dim_customers table.
  - order_date, shipping_date, due_date: Dates related to the order lifecycle.
  - sales_amount, quantity, price: Core sales metrics for each transaction.
- **gold.dim_customers (Dimension Table):** Contains descriptive information for each customer.
  - customer_key: The primary key for identifying a unique customer.
  - Includes demographic data such as first_name, last_name, country, marital_status, gender, and birthdate.
- **gold.dim_products (Dimension Table):** Contains descriptive information for each product.
  - product_key: The primary key for identifying a unique product.
  - Includes product details like product_name, category, subcategory, cost, and product_line.

**Analysis Methodology**

The core of the analysis is performed by the Customer_Product_Behaviour_Analysis.sql script. This script executes two main analytical tasks:

1. **Customer Segmentation:** It processes the sales data to aggregate key metrics for each customer. Customers are then segmented based on their overall value and engagement. The primary segments are:
    - **VIP:** High-value customers with a significant number of orders and high total spending.
    - **Regular:** Customers with consistent but moderate purchasing activity.
    - **New:** Customers who have made recent or few purchases.
2. **Product Performance Analysis:** The script also aggregates data at the product level. It calculates total sales, quantities sold, and the number of unique customers for each product. Products are segmented into:
    - **High-Performer:** Products with total sales exceeding $50,000.
    - **Mid-Range:** Products with total sales between $10,000 and $50,000.
    - **Low-Performer:** Products with total sales below $10,000.

The final outputs are two detailed views, gold.report_customers and gold.report_products, which are then exported as CSV files.

**Key Report Findings**

**Customer Segmentation Report**

The gold.report_customers.csv file reveals distinct customer groups with different purchasing behaviors.

- **VIP Customers:** This is a small but highly valuable group.
  - **Example:** Jon Yang (customer_key: 11000) is a top VIP customer, contributing **$8,249 in total sales** across **3 orders**. This indicates a high average order value.
- **Regular Customers:** This group forms the backbone of the customer base with steady purchasing habits.
  - **Example:** Dalton Perez (customer_key: 11028) is a typical regular customer with **28 total orders** and **$1,186 in total sales**, showing high frequency but lower value per order compared to VIPs.
- **New Customers:** This segment represents an opportunity for growth.
  - **Example:** Lauren Walker (customer_key: 11002) is a new customer with **2 orders** totaling **$81 in sales**. Engaging this segment could convert them into regular or VIP customers over time.

**Product Performance Report**

The gold.report_products.csv file highlights which products are driving the most revenue and engagement.

- **High-Performers:** These are the star products of the business.
  - **Example:** The 'Mountain-200 Silver, 46' (product_key: 351) is a high-performing product with **$137,246 in total sales** from **131 orders** across **127 unique customers**. Its popularity is widespread.
- **Mid-Range Products:** These products are consistent contributors to revenue.
  - **Example:** The 'HL Mountain Frame - Black, 44' (product_key: 319) falls into this category with **$45,849 in total sales**.
- **Low-Performers:** These products may be niche or require marketing attention.
  - **Example:** The 'AWC Logo Cap' (product_key: 212) is a low-performer with **$2,143 in total sales**, suggesting it might be an accessory item rather than a primary purchase driver.

**How to Reproduce the Analysis**

1. **Set up a database:** Use a SQL database server (like SQL Server, PostgreSQL, etc.).
2. **Load the data:** Create the dim_customers, dim_products, and fact_sales tables. Populate them using the corresponding .csv files.
3. **Run the SQL script:** Execute the entire Customer_Product_Behaviour_Analysis.sql script. This will create the two report views.
4. **Export the results:** Query the gold.report_customers and gold.report_products views and export the data to CSV to get the final report files.

**Files in this Repository**

- Customer_Product_Behaviour_Analysis.sql: The main SQL script used for the analysis.
- gold.dim_customers.csv: Raw data for the customer dimension.
- gold.dim_products.csv: Raw data for the product dimension.
- gold.fact_sales.csv: Raw transactional sales data.
- gold.report_customers.csv: The final, generated report on customer segmentation.
- gold.report_products.csv: The final, generated report on product performance.






