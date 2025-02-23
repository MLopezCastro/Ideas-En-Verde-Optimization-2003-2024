# Ideas-En-Verde-Optimization-2003-2024
Data analysis and operational sustainability project for Ideas en Verde (2003-2024). This project focuses on optimizing costs and improving efficiency for an indoor gardening business.

# Ideas en Verde Optimization (2003-2024)

This repository contains the data analysis and operational sustainability project for **Ideas en Verde**, a company specializing in indoor gardening for businesses.

## 📊 Objectives
- Analyze historical data (2003-2024) to identify trends and patterns.
- Optimize costs and improve operational efficiency.
- Enhance sustainability through in-house production and plant recovery.

## 🔄 Workflow
1. Consolidate data from multiple Excel files into a SQL Server relational database.
2. Perform exploratory data analysis using Python (pandas, matplotlib).
3. Design interactive dashboards in Power BI to visualize key performance indicators.

## 🛠️ Tools Used
- **Python**: pandas, matplotlib
- **SQL Server**: Database modeling and queries
- **Power BI**: Advanced visualizations and dashboards

## 🌱 Key Metrics
- **REAL/SERV**: Cost of purchased plants to maintain client stocks.
- **VALOR/SERV**: Combined cost of purchased plants and the value of recovered or in-house produced plants.

## 🚀 Results
- Significant reduction in plant replacement rates.
- Identification of new growth opportunities in under-served regions.
- Improved decision-making through dynamic, data-driven dashboards.

-------------------------------------

## README - Data Integration from 2003-2024 and Power BI Analysis

📌 Overview

This document outlines the complete process of integrating and analyzing historical client restocking data from 2003 to 2024. It details the transformation of data from an initial CSV file to its consolidation in SQL Server, its optimization, and integration with Power BI for visual analysis. Challenges encountered and solutions applied are also documented.

# 📂 1. Data Source

The original data came from a CSV file containing records from 2003 to 2023, with columns for each client's cost and service metrics. The file received was:

tabla_larga_corregida_manual_2024.csv (including 2024 data and new clients)

The goal was to integrate this data into SQL Server, transform it into an analysis-friendly format, and visualize it in Power BI.

# 🔄 2. Data Transformation in SQL Server

2.1. Importing the CSV into SQL Server

The file tabla_larga_corregida_manual_2024.csv was imported into SQL Server using SSMS.

The Date column was set to DATETIME, and other columns to FLOAT, ensuring that null values were maintained correctly.

The initial table was created as follows:

![image](https://github.com/user-attachments/assets/eb322a8e-7e83-4137-bb7c-63bd94c7ab22)

2.2. Creating a Backup Copy

Before applying transformations, a backup of the table was created:

![image](https://github.com/user-attachments/assets/8862af3f-fc8d-429f-8ac5-8010272c568d)

2.3. Transforming into a "Long Table" Format

Since the imported table was in a wide format (each client had separate columns), it was transformed into a long format:

![image](https://github.com/user-attachments/assets/9ff7ee5f-12bf-4570-a597-22ed74f291e7)

# ⚙️ 3. Table Adjustments for Power BI

3.1. Removing Unnecessary Columns

Since Project 1 only used REAL_X/SERV_X and VALOR_X/SERV_X, the extra columns were dropped:

![image](https://github.com/user-attachments/assets/29161212-8f44-4070-aa1a-202182c87a78)

3.2. Correcting the Metric Format

Column names were adjusted to match Project 1, replacing _ with /:

![image](https://github.com/user-attachments/assets/c3dcecaf-c3a3-4b7f-a693-021e74722ebd)

3.3. Creating the "NumericPart" Column

A new column was added to extract the numeric client ID:

![image](https://github.com/user-attachments/assets/0cf9385f-8624-4c64-98cd-8ad527ebf111)

# 📊 4. Integration in Power BI

4.1. Connecting Power BI to SQL Server

Power BI was connected to tabla_larga_cliente_2024 through the following steps:

Get Data → SQL Server

Enter server and database details

Select the tabla_larga_cliente_2024 table

Load data into Power Query

4.2. Adjustments in Power Query

Removed "Changed Type" steps to prevent incorrect data conversions.

Applied filters to only select REAL_X/SERV_X and VALOR_X/SERV_X metrics.

Verified the correct representation of null values.

Created relationships with other metric tables.

4.3. Creating the Graph in Power BI

X-Axis: Date

Values: REAL_X/SERV_X and VALOR_X/SERV_X

Legend: Cliente

Ensured data consistency with Project 1.

🛠️ 5. Issues and Solutions

Issue

Solution

Null values were mistakenly removed in SQL

Structure was reviewed, and original null values were preserved

Incorrect metric format (e.g., "REAL_1 SERV_1")

Fixed using UPDATE tabla SET Métrica = REPLACE(Métrica, '_', '/')

Values appeared as zeros in Power BI

Removed "Changed Type" transformation in Power Query

Excessive decimal places in Power BI

Adjusted data type in SQL Server for proper precision

📌 6. Conclusion and Next Steps

This document outlines the entire workflow from integrating new data to visualizing it in Power BI. Errors in metric naming, formatting, and Power Query transformations were resolved, leading to a fully aligned integration with Project 1.

Next Steps:

Optimize Power BI to improve data loading efficiency.

Automate SQL Server updates with a scheduled pipeline.

Explore predictive modeling to anticipate trends in restocking.

📂 References

Database: SQL Server (SSMS)

Visualization: Power BI

Data Source: tabla_larga_corregida_manual_2024.csv

📌 Last updated: 2025-02-23











