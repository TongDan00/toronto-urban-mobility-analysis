# Toronto Urban Mobility: Big Data ETL & Efficiency Analysis
Author: YuTong Lin
**Interactive Dashboard:** [!(images/toronto_urban_mobility_dashboard.png)](https://public.tableau.com/views/TorontoUrbanMobilityOperationalEfficiencyAnalysis/TorontoUrbanMobilityPost-PandemicEfficiencyRevenueAnalysis?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
*< Click the image above to view the interactive dashboard on Tableau Public >*

## Project Overview
This project is an end-to-end data engineering and business intelligence analysis of Toronto's urban mobility network from 2020 to 2026. The objective was to process a massive, enterprise-scale dataset locally and extract actionable business insights regarding operational efficiency, revenue recovery, and opportunity costs.

**The Challenge:** The raw dataset consisted of 73 individual CSV files totaling over **60+ GB** and **302,715,163 rows** of data. Loading this into memory simultaneously would cause a standard machine to crash.

**The Solution:** I engineered a local ETL (Extract, Transform, Load) pipeline using Python and SQLite. By utilizing iterative batch processing, I successfully loaded and parsed all 300+ million rows on a local machine, aggregated the data using SQL, and exported three lightweight, optimized KPI datasets for visualization in Tableau.

## Tech Stack
- **Data Engineering:** Python (Pandas, Glob), SQLite3
- **Data Analysis:** SQL (Aggregation, Date Parsing, Chunking)
- **Data Visualization:** Tableau Public
- **Version Control:** Git / GitHub

## Key Business Insights
**1. The True Cost of Idle Time (Opportunity Cost)**
While post-pandemic revenue has successfully recovered (hitting ~$160M CAD in early 2026), vehicle idle time has scaled proportionally. By engineering a custom metric based on the Ontario minimum wage ($17.60/hr), I calculated that driver idle time is currently costing the platform an estimated **$35M CAD per month** in lost opportunity. Optimizing route-matching algorithms represents the single largest lever for increasing net profitability.

**2. The "Rush Hour" Cancellation Effect**
Cancellations experience a massive spike at 17:00 (5:00 PM), peaking at **1.51 Million** total historical cancellations. A secondary spike of 1.32M occurs during the 8:00 AM morning commute. *(Note: To calculate the true percentage-based cancellation rate, hourly trip volume data would need to be requested from the data engineering team).*

**3. Pooled Trips and the COVID-19 Margin Impact**
Pooled rides represent the highest-margin product for the platform. Analysis shows pooled efficiency hovering around 7-9% before an immediate drop to **0% in March 2020** due to pandemic social distancing mandates. As of 2026, efficiency has only recovered to roughly 3-4%, highlighting a major marketing opportunity to incentivize shared rides and reclaim profit margins.

## Project Structure

```text
toronto-urban-mobility/
│
├── Dashboards/                         # Local Tableau workbook files
├── images/                             # Dashboard screenshots for documentation
├── sample_data/                        # Lightweight raw CSV subsets for script testing
├── Scripts/                            # Jupyter notebooks for data processing
│   ├── 01_etl_extract_load.ipynb       # Batch loads 73 raw CSV files into SQLite
│   └── 02_kpi_analysis.ipynb           # SQL queries aggregating 302M rows
├── kpi_1_cancellations_by_hour.csv     # Aggregated output (24 rows representing hours 00 to 23)
├── kpi_2_revenue_and_idle.csv          # Aggregated output (daily, Jan 2020–Jan 2026)
├── kpi_3_pooled_efficiency.csv         # Aggregated output (daily, Jan 2020–Jan 2026)
├── .gitignore                          # Excludes the intentionally untracked 60GB raw dataset
├── README.md                           # Project documentation and key insights
└── requirements.txt                    # Python dependencies (pandas, jupyter)
```
**Please note:** To adhere to GitHub's file size limits and best practices, the 60GB raw database (toronto_transportation.db) and complete raw CSVs are excluded via .gitignore. Only the scripts, sample data, and aggregated outputs are tracked.

## Data Source & Reproducibility
The raw dataset utilized in this project is publicly available via the City of Toronto Open Data Portal.
Dataset Name: Vehicle Operating Data / Private Transportation Companies
Source: Toronto Open Data Portal [https://open.toronto.ca/dataset/private-transportation-companies-vehicle-operating-data/]