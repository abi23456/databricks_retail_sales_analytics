# Gold Layer: Curated KPI Metrics

## Overview

This notebook creates and analyzes the **curated_kpi_metrics** table in the gold layer, providing business-ready KPIs and metrics for retail sales analytics. The table consolidates data from sales, returns, and inventory fact tables to enable comprehensive performance analysis.

**Notebook**: `03_gold_curated_kpi`  
**Target Table**: `03_gold_catalog.gold_schema.curated_kpi_metrics`  
**Layer**: Gold (Curated/Business Layer)

---

## Data Sources

The curated KPI metrics table integrates data from multiple gold layer fact and dimension tables:

### Fact Tables
- **fact_sales**: Transaction-level sales data with product, customer, and store information
- **fact_returns**: Product return transactions and amounts
- **fact_inventory**: Current and historical inventory snapshots

### Dimension Tables
- **dim_store**: Store attributes including name and region

---

## Table Schema

The `curated_kpi_metrics` table includes:

### Identifiers
- `transaction_key`: Unique transaction identifier
- `customer_key`: Customer identifier
- `product_key`: Product identifier
- `store_key`: Store identifier

### Time Dimensions
- `transaction_date`: Full transaction timestamp
- `transaction_year`, `transaction_month`, `transaction_day`: Date components
- `transaction_date_only`: Date truncated to day level

### Product Attributes
- `product_name`: Name of the product
- `product_category`: Product category

### Sales Metrics
- `quantity_sold`: Units sold in transaction
- `unit_price`: Price per unit
- `total_sales_amount`: Total sales revenue
- `discount_amount`: Discount applied
- `profit_amount`: Profit generated

### Return Metrics
- `return_count`: Number of returns for the transaction
- `returned_amount`: Total amount returned
- `is_returned`: Flag indicating if transaction was returned (1/0)

### Inventory Metrics
- `current_stock_quantity`: Current stock level
- `is_out_of_stock`: Flag for out-of-stock status (1/0)
- `inventory_value_cost`: Inventory value at cost
- `inventory_value_retail`: Inventory value at retail price

### Helper Metrics
- `transaction_count`: Counter for transaction aggregations (always 1)

---

## Key Performance Indicators (KPIs)

The notebook calculates and displays the following KPIs:

### 1. Overall Business Performance
- Total Sales Revenue
- Total Transactions
- Unique Customers

### 2. Product Performance
- Top 10 Products by Profit
- Units Sold per Product
- Average Profit per Unit

### 3. Category Analysis
- Revenue by Category
- Category Revenue Share
- Units Sold and Transactions by Category
- Total Profit by Category

### 4. Customer Behavior
- Average Basket Size
- Min/Max Basket Size
- Repeat Customer Rate
- Customer Segmentation (One-time, Regular, Loyal, VIP)
- Average Purchases per Repeat Customer

### 5. Returns Analysis
- Return Rate (by transactions and amount)
- Total Returned Amount
- Returned Transactions Count

### 6. Inventory Health
- Out-of-Stock Rate
- Out-of-Stock Products List
- Slow-Moving Products (no sales in 30 days)
- Slow-Moving Rate

### 7. Store Performance
- Top 5 Stores by Average Daily Sales
- Total Sales per Store
- Days Active per Store
- Performance Ranking

### 8. Discount Impact
- Total Discount Given
- Discount Rate
- Potential Revenue without Discounts
- Discount Impact by Category

---

## Analyses Included

The notebook provides ready-to-use analyses:

1. **Executive Summary** - High-level business metrics
2. **Product Performance** - Best-selling and most profitable products
3. **Category Performance** - Revenue distribution across categories
4. **Basket Analysis** - Customer purchasing patterns
5. **Returns Analysis** - Return rates and impact
6. **Inventory Status** - Stock health and out-of-stock alerts
7. **Store Performance** - Location-based performance ranking
8. **Discount Analysis** - Promotion effectiveness
9. **Customer Loyalty** - Repeat purchase behavior and segmentation
10. **Slow-Moving Inventory** - Products requiring attention

---

## Usage Instructions

### Prerequisites
- Ensure gold layer fact tables exist:
  - `03_gold_catalog.gold_schema.fact_sales`
  - `03_gold_catalog.gold_schema.fact_returns`
  - `03_gold_catalog.gold_schema.fact_inventory`
  - `03_gold_catalog.gold_schema.dim_store`

### Running the Notebook

1. **Execute Cell 1** to create/refresh the `curated_kpi_metrics` table
2. **Execute Cells 2-11** to view individual KPI analyses
3. **Execute Cell 12** to view the complete metrics table

### Refresh Schedule
- Run this notebook after the gold layer fact tables are updated
- Recommended: Daily refresh for current inventory and sales metrics

---

## Key Insights

This curated KPI table enables:

✅ **Real-time Business Monitoring** - Track sales, inventory, and customer metrics  
✅ **Product Strategy** - Identify bestsellers and slow-moving inventory  
✅ **Customer Insights** - Understand purchasing patterns and loyalty  
✅ **Store Performance** - Compare locations and optimize operations  
✅ **Inventory Optimization** - Reduce out-of-stock and overstock situations  
✅ **Discount Effectiveness** - Measure promotion ROI  
✅ **Return Management** - Monitor and reduce return rates

---

## Technical Notes

- **Table Type**: Delta Lake (supports ACID transactions and time travel)
- **Partition Strategy**: None (suitable for reporting/analytics workload)
- **Update Pattern**: Full refresh (CREATE OR REPLACE)
- **Join Strategy**: LEFT JOIN to preserve all sales transactions
- **Inventory Snapshot**: Uses most recent inventory snapshot per product/store

---

