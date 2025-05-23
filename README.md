# Plant Company Gross Profit Performance Dashboard
# Overview

This project analyzes the financial performance of the Plant Company, focusing on gross profit metrics derived from the Plant_DTS.xls dataset. As a data analyst, I cleaned and transformed the dataset, created custom DAX measures in Power BI, and developed an interactive dashboard to visualize year-to-date (YTD) and prior year-to-date (PYTD) performance across sales, quantity, and gross profit. The dashboard highlights trends by country, product type, and month, showcasing my expertise in data manipulation, measure development, and data visualization.

# Dataset

The original dataset, Plant_DTS.xls, contains sales transactions with fields such as Product_id, Sales_USD, Quantity, Price_USD, COGS_USD, Date_Time, and Account_id. Additionally, a related product dimension includes botanical details like Family, Common_Name, Scientific_Name, Product_id, Size, and Product_Type. The dataset spans transactions from 2022 to 2024, providing a foundation for temporal and categorical analysis.

# Data Cleaning and Preparation

I performed a thorough cleaning process Power Query to ensure data quality:


Handling Missing Values: Identified and replaced missing or invalid Date_Time entries with the median date and filled null COGS_USD values with calculated costs based on Price_USD and Quantity.

Type Conversion: Converted Sales_USD, COGS_USD, and Price_USD to numeric formats, resolving inconsistencies (e.g., text artifacts in currency fields). Ensured Quantity was an integer.

Date Standardization: Parsed Date_Time into a consistent YYYY-MM-DD format and created a Dim_Date table with Year, Month, and InPast flags for temporal analysis.

Duplicate Removal: Removed duplicate entries based on Product_id and Date_Time to prevent inflated metrics.

Outlier Detection: Filtered out transactions with negative Sales_USD or COGS_USD values, ensuring data integrity.

Exporting Cleaned Data: Saved the cleaned dataset as plant_cleaned.csv for Power BI import.

This process resulted in a refined dataset of approximately 1000 records, ready for advanced analysis.

# Measure Creation in Power BI

I developed custom DAX measures to enable dynamic performance tracking:

Gross Profit: Gross Profit = SUM('Plant_FACT'[Sales_USD]) - SUM('Plant_FACT'[COGS_USD]) - Calculated total gross profit (e.g., 6.89M YTD).

GP%: GP% = DIVIDE([Gross Profit], [Sales]) - Derived gross profit margin (e.g., 39.77% YTD).

PYTD Gross Profit: PYTD_GrossProfit = CALCULATE([Gross Profit], SAMEPERIODLASTYEAR(Dim_Date[Date]), Dim_Date[InPast] = TRUE) - Compared YTD with PYTD (e.g., -5.49M variance).

PYTD Quantity: PYTD_Qauntity = CALCULATE([Qauntity], SAMEPERIODLASTYEAR(Dim_Date[Date]), Dim_Date[InPast] = TRUE) - Tracked prior year quantity.

PYTD Sales: PYTD_Sales = CALCULATE([Sales], SAMEPERIODLASTYEAR(Dim_Date[Date]), Dim_Date[InPast] = TRUE) - Compared prior year sales.

Dim_Date Table: Dim_Date = CALENDAR(DATE(2022, 1, 1), DATE(2024, 12, 31)) - Created a calendar table for time intelligence, with relationships to Date_Time.

Dynamic Titles:

_Report title = "Plant Company " & SELECTEDVALUE(Slc_Values[Values]) & " Performance " & SELECTEDVALUE(Dim_Date[Date].[Year])

_column char title = SELECTEDVALUE(Slc_Values[Values]) & "YTD vd PYTD | Month"

_Waterfall title = SELECTEDVALUE(Slc_Values[Values]) & "YTD vs PYTD | Month - Country - Product"

_scatter title = "Account Profitability segmentation | GP% and " & SELECTEDVALUE(Slc_Values[Values])

These measures facilitated interactive analysis of YTD vs. PYTD performance and profitability segmentation.

# Dashboard Creation in Power BI

I designed an interactive Power BI dashboard to visualize the cleaned data and measures:

Summary Metrics: Displayed YTD Gross Profit (6.89M), YTD vs. PYTD variance (-5.49M), YTD Quantity (1.40M), and GP% (39.77%) with color-coded indicators.

Gross Profit YTD vs. PYTD by Month: A column chart showing monthly gross profit trends, with Indoor (blue), Landscape (cyan), and Outdoor (red) product types, highlighting a peak in Qtr 2 (0.92M YTD vs. 0.76M PYTD).

Top 10 YTD vs. PYTD by Country: A waterfall chart illustrating country-level performance (e.g., Hungary -0.48M, Switzerland -0.31M), with total variance of -1.5M.

Account Profitability Segmentation: A scatter plot mapping GP% vs. Gross Profit, with accounts clustered around 40–80% GP%, indicating profitability distribution.

Slicers: Added filters for Values (Gross Profit, Quantity, Sales), YTD, and Product_Type to enable user interaction.

Design: Used a modern theme with clear labels, tooltips, and a background image for visual appeal.

The dashboard provides a comprehensive view of financial performance and trends.

# Key Insights

Performance Decline: YTD Gross Profit (6.89M) is down 5.49M from PYTD (6.89M vs. 12.38M), indicating a significant drop in profitability.

Monthly Trends: Qtr 2 shows the highest YTD Gross Profit (0.92M), suggesting seasonal strength, while Qtr 3 dips to 0.46M.

Country Impact: Hungary and Switzerland contribute the largest negative variances (-0.48M and -0.31M), warranting further investigation.

Product Type Performance: Indoor products lead YTD Gross Profit (e.g., 0.88M), while Outdoor types show growth potential (e.g., 0.50M).

Profitability Segmentation: Most accounts maintain GP% above 40%, with top performers exceeding 60%, highlighting a robust profit margin structure.

Interesting Fact: Despite a 5.49M decline, GP% remains stable at 39.77%, suggesting cost control amidst revenue challenges.

These insights demonstrate my ability to derive actionable trends from financial data.
