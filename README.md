# Global Electronics Retail Analysis | Power BI Dashboard

## Problem Statement

A global electronics retailer wants to understand why its overall revenue growth is slowing down. This project analyzes sales data across countries and product categories to find out where the slowdown is happening, whether it's because fewer orders are coming in or because each order is worth less, and whether the drop is a business issue or possibly related to outside factors like the pandemic. The goal is to help the company know where to focus and what needs to be improved.

## Dataset

- **Source:** Maven Analytics — Global Electronics Retailer
- **Scale:** 62,884 records, 37 fields, across 5 related source tables
- **Tables:** Sales, Products, Customers, Stores, Exchange Rates
- **Coverage:** 9 countries/channels, 2016–2021
- **Note:** 2021 was excluded from the main trend analysis because it was an incomplete year with only 51 days of records.

## Data Preparation (Power Query)

- Imported and cleaned all 5 source tables
- Fixed an Order Date locale/format error using **Change Type with Locale** (English UK), reducing errors from 61% to 0%
- Investigated missing Delivery Date values (79% blank) and kept them as blanks rather than removing or estimating them
- Created a composite key using **Currency Code + Order Date** in Sales and the corresponding currency + date fields in Exchange Rates
- Merged Sales with Exchange Rates using the composite key
- Expanded the merged column to bring the Exchange value into the Sales table as **ExchangeRate**
- Verified data types across the tables

## Data Modeling

- Built a star-schema structure with **Sales** as the main fact table
- Connected Sales with **Customers, Products, Stores, and Calendar**
- Created a separate **Calendar** table for time-based analysis
- Marked Calendar as the date table
- Created a separate **_measures** table to organize DAX measures
- Created and verified the required relationships between the tables

## Key DAX Measures

| Measure | Purpose |
|---|---|
| `Total Revenue` | Calculates total revenue using `SUMX` and `RELATED` |
| `Total Orders` | Counts unique orders using `DISTINCTCOUNT` |
| `Average Order Value` | Calculates revenue per order using `DIVIDE` |
| `Revenue LY` | Gets previous-year revenue using `SAMEPERIODLASTYEAR` |
| `Revenue YoY %` | Calculates year-over-year revenue growth |
| `Revenue YoY 2020` | Calculates 2020 revenue change compared with the previous year |
| `Country Rank` | Ranks countries by revenue using `RANKX` |

## Data Investigation Process

Before building the final dashboard, I investigated the data:

1. **Checked revenue by year** → found growth of 72% in 2018 and 43% in 2019
2. **Checked total orders by year** → investigated whether changes in order volume explained the revenue trend
3. **Checked country performance for 2019** → found significant differences between markets
4. **Checked category performance for 2019** → found significant differences between categories
5. **Investigated 2020 month by month** → found a sharp decline starting around March 2020, which coincided with the COVID period
6. **Checked 2021 data** → found it was only a partial year, so it was excluded from the main year comparison

## Dashboard Pages

### 1. Overview
Shows overall revenue, revenue trends, country performance, and category performance.

### 2. Country Performance
Shows revenue and YoY performance by country, along with order volume, average order value, and country ranking.

### 3. Category Performance
Shows category revenue growth, category performance, and top products by revenue.

### 4. 2020 Impact
Shows country and category performance during 2020 and helps analyze the large revenue decline separately.

All pages include Year and Country slicers for interactive filtering.

## Key Findings

- Overall revenue growth slowed from **72% in 2018 to 43% in 2019**
- **Italy** recorded the lowest 2019 revenue growth among the markets at **9.36%**
- **Home Appliances** was the only category to decline in 2019 at **-4.73%**
- **Games and Toys** had the strongest category growth at **105.69%**
- Revenue fell by approximately **49% in 2020**
- The 2020 decline was analyzed separately because the sharp decline around March coincided with the COVID period

## Tools Used

- Power BI
- Power Query
- DAX
- Data Modeling
- Star Schema

## What This Project Demonstrates

- Data cleaning and validation
- Data investigation before dashboard creation
- Multi-year and multi-country analysis
- Time-based DAX calculations
- Power Query data merging using a composite key
- Star-schema data modeling
- Building an interactive business dashboard
