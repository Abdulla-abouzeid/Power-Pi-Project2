# Sales & Profit Analytics Dashboard

An interactive, multi-page Power BI report analyzing sales, profit and orders for **Wide World Importers**, built on a star-schema data model.

## Overview

| Metric | Value |
|---|---|
| Transactions | 26,397 |
| Orders (invoices) | 8,188 |
| Total Sales (incl. tax) | $22.9M |
| Total Profit | $9.9M |
| Profit Margin | 43.4% |

Top states by sales: **California** ($10.2M), **Washington** ($4.9M), **Alaska** ($3.5M).

## Report Pages

| Page | Content |
|---|---|
| **KPI** | Total sales, profit, orders, quantity, customers, products |
| **Charts** | Monthly sales trend, top stock items by sales and profit, top salespeople |
| **Dashboard** | Main dashboard with slicers (year, month, state, city) and bookmark navigation |
| **Analysis Dashboard** | Profit margin, average order value, tax, profit per item, sales and profit by state and city |
| **Charts2** | Sales map by state, profit by state and city, monthly orders |
| **KPI2** | Average order value, profit margin, total tax, average quantity per order, profit per item |

## Data Model

Star schema with one fact table and five dimensions:

- **Fact:** `Sales_Table`
- **Dimensions:** `City_Table`, `Customer_Table`, `Stock_Item_Table`, `Employee_Table`, `Date_Table`

Relationships (many-to-one, single direction):
`Sales_Table` → City (City Key), Customer (Customer Key), Stock Item (Stock Item Key), Employee (Salesperson Key), Date (Invoice Date Key)

## DAX Measures

```DAX
Total Sales = SUM(Sales_Table[Total Including Tax])
Total Profit = SUM(Sales_Table[Profit])
Total Quantity = SUM(Sales_Table[Quantity])
Total Orders = DISTINCTCOUNT(Sales_Table[WWI Invoice ID])
Total Customers = DISTINCTCOUNT(Customer_Table[Customer Key])
Total Products = DISTINCTCOUNT(Stock_Item_Table[Stock Item Key])
Total Tax = SUM(Sales_Table[Tax Amount])
Profit Margin = Sales_Table[Total Profit] / Sales_Table[Total Sales]
Average Order Value = DIVIDE(SUM(Sales_Table[Total Including Tax]), [Total Orders])
Average Quantity per Order = DIVIDE(SUM(Sales_Table[Quantity]), [Total Orders])
Profit per Item = DIVIDE(SUM(Sales_Table[Profit]), SUM(Sales_Table[Quantity]))
```

## Features

- Drill-down analysis by year, month, state and city using slicers
- Geographic analysis with a map visual
- Bookmarks and navigation buttons between pages
- Custom calculated columns: Profit Category and Tax Status

## Tools

Power BI Desktop, DAX, Power Query, Star Schema Modeling

## Screenshots

![Dashboard](screenshots/dashboard.png)
![Analysis Dashboard](screenshots/analysis-dashboard.png)

## Files

- `Midterm_Data.pbix`: the Power BI report (open with Power BI Desktop)

## Data Source

Wide World Importers sample dataset (Microsoft), cleaned and loaded from CSV files.
