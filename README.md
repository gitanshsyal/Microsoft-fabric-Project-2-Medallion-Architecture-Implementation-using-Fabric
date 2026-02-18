# Microsoft-fabric-Project-2-Medallion-Architecture-Implementation-using-Fabric
The objective of this project was to design and implement a Medallion Architecture (Bronze → Silver → Gold) to ingest, clean, standardize, and transform raw data into business-ready analytical insights.

# Tech Stack
Data Source: Azure Data Lake Gen2
Ingestion: Fabric Pipeline (Copy Activity)
Processing: Spark Notebooks
Storage: Lakehouse
Platform: Microsoft Fabric

# Architecture Overview
 1.Bronze Layer
Built a pipeline to ingest raw files from ADLS Gen2 into the Lakehouse
Data stored in raw format without transformations
-----------------------------------------------------------------------------------------------------------
2.Silver Layer (Data Cleaning & Standardization)
 Orders Table
 ---------------------------------------------------------------------------------------------------

Handled first row & corrected column names

Converted quantity → integer

Standardized date formats

Cleaned order_amount (removed ₹, $, USD)

Normalized payment_mode (lowercase, standardized values)

Validated email format

Cleaned shipping address (removed special characters)

Converted feedback score to double and handled null/NaN

Filled nulls:

quantity → 0

order_amount → 0.0

delivery_status → unknown

payment_mode → unknown

Removed duplicate order_id

# Inventory Table
--------------------------------------------------------------------------------------------------------------------------------

Renamed columns (product_name, cost_price, last_stocked)

Converted stock to integer

Standardized date format

Cleaned cost price (removed currency symbols)

Cleaned warehouse name & capitalized

Converted availability flag (Y/N) to Boolean

Dropped records with null customer_id and product_name

# Returns Table
------------------------------------------------------------------------------------------------------------------------
Renamed columns for consistency

Standardized return date

Cleaned return status (lowercase, removed special characters)

Cleaned return amount and converted to double

Cleaned pickup address and product name

Converted customer_id to uppercase

-------------------------------------------------------------------------------------------------------------

# Gold Layer (Business Metrics)

Joined Orders, Inventory, and Returns tables to generate analytics-ready metrics:

Total number of orders

Total number of customers

Total number of returns

Return rate

Total revenue

Average order value

Total stock available

Average cost price

Net Profit

Net Profit = Total Order Amount − (Avg Cost Price × Total Stock)
