Chicago Traffic Congestion Analysis
Overview

This project analyzes traffic congestion across Chicago roadway segments using the City of Chicago Traffic Tracker dataset. The goal is to identify which roadway segments should be prioritized for congestion mitigation by comparing observed traffic speeds against each segment's typical operating conditions.

Rather than relying solely on raw traffic speed, this analysis establishes a segment-specific baseline speed and measures congestion relative to that baseline. A composite Priority Score is then calculated by combining congestion severity and recurrence, providing a data-driven framework for prioritizing roadway improvements.

Project Objective

Develop a repeatable analytical workflow that:

Cleans and validates roadway traffic data
Establishes a baseline operating speed for each roadway segment
Quantifies congestion severity relative to normal traffic conditions
Identifies recurring congestion patterns
Prioritizes roadway segments using a composite congestion score
Dataset

Source: Chicago Traffic Tracker

Time Period:

June 11, 2024 – December 31, 2024

The dataset contains hourly traffic observations for roadway segments across Chicago, including:

Roadway segment ID
Street name
Date and hour
Average traffic speed
Data quality classification
Tools Used
Tool	Purpose
Python	Data acquisition and preprocessing
DuckDB SQL	Data transformation and analysis
Jupyter Notebook	Workflow documentation
Power BI (coming soon)	Interactive dashboard and visualization
Methodology
1. Data Cleaning
Imported traffic observations
Filtered to High Quality records
Standardized timestamps
Removed invalid observations

Output:

traffic_clean
2. Baseline Speed

Each roadway segment has a different normal operating speed.

Instead of comparing all streets using the same benchmark, a baseline speed was calculated individually for every segment using weekday midday traffic conditions (10 AM–1 PM), representing relatively uncongested operating conditions.

Output:

baseline

3. Slowdown Calculation

Congestion was measured as the percentage reduction from the baseline speed:

Slowdown (%) =
(Baseline Speed − Observed Speed)
÷ Baseline Speed × 100

Output:

slowdown

4. Segment Summary

Traffic observations were aggregated by roadway segment to calculate:

Average slowdown (%)
Frequency of significant congestion (≥20% slowdown)
Observation counts

Output:

segment_summary

5. Priority Ranking

Both congestion metrics were normalized to a 0–100 scale using Min-Max normalization.

The final Priority Score equally weights:

Congestion Severity
Congestion Frequency
Priority Score =
0.5 × Severity Score
+
0.5 × Frequency Score

Segments are ranked from highest to lowest priority.

Output:

priority_ranking
Project Workflow
Raw Traffic Data
        │
        ▼
Data Cleaning
        │
        ▼
Baseline Speed Calculation
        │
        ▼
Slowdown Analysis
        │
        ▼
Segment Summary
        │
        ▼
Priority Ranking
        │
        ▼
Power BI Dashboard
Key Insights

The analysis found that:

Traffic congestion peaks during the afternoon commute, with the greatest average slowdowns occurring around 4–5 PM.

Chicago-Traffic-Congestion-Analysis/

│── Chicago_Traffic_Congestion_Analysis.ipynb
│── README.md
│
├── data/
│     ├── priority_ranking.csv
│     ├── segment_summary.csv
│     └── slowdown.csv
│
├── dashboard/
│     └── Chicago_Traffic_Dashboard.pbix
│
└── images/
      ├── dashboard_overview.png
      ├── dashboard_priority.png
      └── dashboard_hourly.png
Measuring congestion relative to each roadway segment's baseline provides a more meaningful comparison than using raw traffic speeds alone.
Combining congestion severity with the frequency of recurring slowdowns identifies roadway segments that consistently experience operational challenges.
The resulting Priority Score provides a transparent and repeatable framework for identifying roadway segments that may benefit from congestion mitigation strategies.

Future Improvements
Develop an interactive Power BI dashboard
Incorporate geographic visualization of roadway segments
Analyze seasonal and weekday/weekend congestion patterns
Evaluate alternative weighting schemes for the Priority Score
Compare congestion trends across multiple years

Skills Demonstrated
SQL
Common Table Expressions (CTEs)
Window Functions
Views
Aggregations
Ranking Functions
Conditional Logic
Data Cleaning
Min-Max Normalization
Data Analytics
Feature Engineering
Baseline Development
Congestion Analysis
KPI Design
Composite Scoring Methodology
Business Intelligence
Dashboard Design
KPI Reporting
Decision Support Analytics
Data Storytelling
