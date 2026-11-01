# E-Commerce Customer Churn Analysis (MySQL)

A MySQL project that cleans, transforms and analyses an e-commerce customer dataset to understand **why customers churn** and which groups are most at risk. The goal is to give the business insights it can use for targeted retention strategies.

## Dataset
- **File:** `E-Commerce_Customer_churn_db.sql` (creates the `ecomm` database and the `customer_churn` table)
- **Size:** 5,630 customer records (5,628 after cleaning)
- **Key columns:** Tenure, PreferredLoginDevice, CityTier, WarehouseToHome, PreferredPaymentMode, Gender, HourSpendOnApp, NumberOfDeviceRegistered, PreferedOrderCat, SatisfactionScore, MaritalStatus, NumberOfAddress, Complain, OrderAmountHikeFromlastYear, CouponUsed, OrderCount, DaySinceLastOrder, CashbackAmount, Churn

## Project Structure
```
.
├── E-Commerce_Customer_churn_db.sql   # Dataset (creates database and table)
├── Churn_Analysis_Solution.sql        # Cleaning, transformation and analysis queries
└── README.md
```

## How to Run
1. Open MySQL Workbench (or any MySQL client).
2. Run `E-Commerce_Customer_churn_db.sql` to create and load the `ecomm` database.
3. Run `Churn_Analysis_Solution.sql` from top to bottom in one go (**Ctrl+A**, then **Ctrl+Shift+Enter** in Workbench).
4. To start over, re-run step 2 first. The cleaning steps change the table and are not meant to be run twice.

## What the Project Covers

### 1. Data Cleaning
- Filled missing values with the **mean** (rounded) for WarehouseToHome, HourSpendOnApp, OrderAmountHikeFromlastYear and DaySinceLastOrder.
- Filled missing values with the **mode** for Tenure, CouponUsed and OrderCount.
- Removed outliers: deleted rows where WarehouseToHome > 100 (2 rows).
- Standardised text values: `Phone` and `Mobile` to `Mobile Phone`, `COD` to `Cash on Delivery`, `CC` to `Credit Card`.

### 2. Data Transformation
- Renamed `PreferedOrderCat` to `PreferredOrderCat` and `HourSpendOnApp` to `HoursSpentOnApp`.
- Created `ComplaintReceived` (Yes/No) from `Complain` and `ChurnStatus` (Churned/Active) from `Churn`.
- Dropped the original `Churn` and `Complain` columns.

### 3. Data Exploration and Analysis
17 business questions answered with SQL, using `GROUP BY`, aggregate functions, `HAVING`, subqueries, `CASE WHEN` and `JOIN`. A new `customer_returns` table is created and joined with the customer data.

## Key Findings

| Question | Result |
|---|---|
| Churned vs active customers | 948 churned, 4,680 active |
| Average tenure of churned customers | 3.18 months |
| Total cashback of churned customers | 152,030 |
| Churned customers who complained | 53.59% |
| City tier with most churned Laptop & Accessory customers | Tier 3 (150) |
| Most preferred payment mode (active customers) | Debit Card |
| City tier with the most customers | Tier 1 (3,666) |
| Gender using the most coupons | Male |
| Average satisfaction score of complainers | 3.00 |
| Top 3 categories by average cashback | Others, Grocery, Fashion |
| Payment modes with average tenure of about 10 months and 500+ orders | Credit Card, Debit Card, E wallet |

**Insights**
- Churned customers have a very short average tenure (about 3 months), so the early months are the most important time to retain customers.
- More than half of churned customers had complained, so complaint handling is closely linked to churn.
- Customers living far from the warehouse (more than 15 km) make up the largest share of churned customers.

## Notes
- For question 15, averages are decimals (for example 9.95), so `ROUND(AVG(Tenure)) = 10` is used instead of an exact match.
- Total orders per payment mode (`SUM(OrderCount) > 500`) is used for "placed more than 500 orders".

## Tools
- MySQL 8.x / MySQL Workbench

## Author
Add your name and links here.
