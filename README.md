📊 Telecommunications Customer Usage Analysis

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black)

🎯 Project Overview

How can telecommunications companies turn raw customer data into meaningful insights about customer behavior and service usage?

This project demonstrates an end-to-end exploratory data analysis (EDA) workflow focused on telecommunications customer behavior. Using Python, Pandas, NumPy, and Matplotlib, I processed and analyzed customer demographics, call records, text message activity, and subscription plan information to identify usage patterns, assess data quality, investigate statistical distributions, and segment customers by age and communication activity.

The project showcases practical data analytics skills, including data cleaning, quality assurance, data transformation, aggregation, statistical analysis, outlier detection, data visualization, and customer segmentation.

🔍 What I Did

- Data Cleaning and Quality Assurance: Identified and handled missing values, sentinel values, unexpected entries, and potential date inconsistencies.
- Exploratory Data Analysis: Examined dataset structures, data types, customer demographics, and communication patterns.
- Statistical Analysis: Calculated descriptive statistics and evaluated distributions, variability, and potential outliers.
- Data Aggregation and Integration: Consolidated individual call and text message records into customer-level metrics and integrated the results with demographic information.
- Customer Segmentation: Classified customers by age and usage levels to identify the most represented customer groups.
- Data Visualization: Used histograms and boxplots to investigate distributions, identify potential anomalies, and communicate analytical findings.
- Analytical Documentation: Organized the workflow in a Jupyter Notebook to support transparency and reproducibility.

💼 Business Value

The analysis provides a structured view of customer demographics and communication habits, establishing a foundation for further investigation into customer segmentation, subscription plan usage, and service optimization.

The findings help identify customer groups with different communication patterns and highlight opportunities for deeper analysis of the relationship between customer characteristics, usage behavior, and subscription plans.

Key deliverable: A documented and reproducible data analysis workflow that transforms raw telecommunications records into organized customer-level metrics, statistical findings, visual insights, and recommendations for further investigation.

---

🎯 Project Objective

The objective of this project is to conduct an exploratory analysis of customer behavior for Telecomm's telecommunications services, using demographic information, call and text message records, and subscription plan details.

The analysis aims to understand customer usage patterns, identify potential data quality issues, and segment customers according to their age and level of call and text message usage.

---

📂 Datasets Used

The project uses three main datasets:

"users"

Contains customer information:

- "user_id": Unique customer identifier.
- "age": Customer's age.
- "city": Customer's city of residence.
- "plan": Subscribed plan.
- "reg_date": Service registration date.
- "churn_date": Date the customer canceled the service.

"usage"

Contains service usage records:

- "id": Unique usage record identifier.
- "user_id": Customer identifier.
- "type": Type of communication ("call" or "text").
- "duration": Call duration.
- "length": Number of characters in text messages.
- "date": Date of the usage record.

"plans"

Contains information about the available subscription plans:

- "plan_name": Plan identifier.
- "messages_included": Number of text messages included in the plan.
- "gb_per_month": Number of gigabytes included per month.
- "minutes_included": Number of call minutes included.
- "usd_monthly_pay": Monthly subscription fee in USD.
- "usd_per_gb": Cost per additional gigabyte in USD.
- "usd_per_message": Cost per additional text message in USD.
- "usd_per_minute": Cost per additional call minute in USD.

---

🔎 Analysis Workflow

1. Initial Data Exploration

An initial review of the tables was performed to:

- Identify the data types of each column.
- Examine the structure and dimensions of the datasets.
- Check for missing values.
- Identify unique values and potential inconsistencies.
- Understand the relationships between tables using "user_id".

2. Data Cleaning and Preparation

Several data quality issues were identified and addressed during this stage:

- The "reg_date" and "date" columns were converted to appropriate date data types.
- The sentinel value "-999" was identified in the "age" column and replaced with the column's statistical mean.
- Question marks ("?") found in the "city" column were replaced with missing values.
- Dates later than the current date were checked to identify potentially invalid records. No records requiring modification were found.

Missing values in "duration" and "length" were also analyzed in relation to the "type" column. These values were evaluated according to the type of record:

- "call" records should contain "duration" information.
- "text" records should contain "length" information.

Unexpected values were converted to "NaN" to facilitate further analysis.

3. Statistical Analysis

Descriptive statistics were calculated for the following variables:

- Customer age.
- Number of text messages.
- Number of calls.
- Total call duration.
- Total text message length.

The following statistical measures were examined:

- Mean.
- Standard deviation.
- Minimum and maximum values.
- Quartiles.
- Median.

Histograms and boxplots were also used to examine data distributions and identify potential outliers.

4. Data Aggregation

Usage records were grouped by "user_id" to calculate customer-level metrics:

- "cant_mensajes": Total number of text messages.
- "cant_llamadas": Total number of calls.
- "cant_minutos_llamada": Total call duration.
- "longitud_mensajes_total": Total number of characters sent through text messages.

The aggregated information was subsequently combined with the "users" table.

5. Distribution and Outlier Analysis

The distributions of the main variables were examined using histograms and boxplots.

Key findings included:

- Age: Most customers were between 30 and 60 years old.
- Text message count: The distribution was right-skewed, with a higher concentration of customers sending relatively few messages.
- Call count: The distribution was approximately bell-shaped, with a slight right skew.
- Call duration: The distribution was right-skewed, with most records corresponding to shorter calls.
- Total text message length: High outlier values were observed, reaching approximately 2,000 characters.

Outliers were evaluated carefully, recognizing that an extreme value does not necessarily indicate an error. When there was insufficient evidence to classify a value as incorrect, it was retained to avoid losing information about customers with higher usage levels.

6. Customer Segmentation

Two main segmentation approaches were implemented.

👥 Age-Based Segmentation

Customers were grouped into the following age categories:

Segment| Age Range
Young customers| Under 30 years old
Adults| 30–60 years old
Older adults| Over 60 years old

The largest customer group consisted of adults between 30 and 60 years old.

📊 Usage-Based Segmentation

Customers were classified according to their number of text messages and calls:

Segment| Criteria
Low usage| Fewer than 5 messages or calls
Medium usage| Between 5 and 10 messages or calls
High usage| More than 10 messages or calls

The predominant segment was medium usage, followed by low usage. High-usage customers represented a smaller proportion of the customer base.

---

💡 Conclusions

The results indicate that most customers exhibit a medium level of call and text message usage. Adults between 30 and 60 years old represent the largest age group in the customer base.

Analyzing the total number of characters sent through text messages complemented the message frequency analysis and provided a more detailed understanding of how customers use the messaging service.

The analysis also demonstrates the importance of data quality assessment before interpreting statistical results. Identifying sentinel values, handling unexpected entries, evaluating missing values, and investigating outliers help establish a more reliable foundation for customer behavior analysis.

These findings provide a starting point for further analysis of customer behavior, subscription plan usage, and potential service optimization opportunities.

---

🚀 Recommendations for Further Analysis

The following analyses are proposed as next steps:

- Examine which subscription plans are used by each age group and their corresponding usage levels.
- Compare call and text message usage across different age groups.
- Investigate the relationship between subscription plans and customer usage behavior.
- Explore the number of characters sent by customers who use text messaging services.
- Analyze usage patterns over time to identify monthly trends and changes in customer activity.
- Compare customer usage against the allowances included in each subscription plan to investigate potential overage charges and plan suitability.

---

🛠️ Technologies Used

Technology| Purpose
Python| Data processing and analytical workflows.
Pandas| Data manipulation, cleaning, transformation, aggregation, and integration.
NumPy| Numerical operations and missing-value handling.
Matplotlib| Statistical visualization and exploratory analysis.
Jupyter Notebook| Interactive analysis, code execution, and documentation.
Google Colab| Cloud-based notebook execution and analysis.

---

▶️ How to Run the Project

Option 1 — Google Colab

1. Clone or download this repository.
2. Open the ".ipynb" notebook file.
3. Go to "Google Colab" (https://colab.research.google.com/).
4. Select File → Upload notebook.
5. Upload the project's notebook.
6. Upload the datasets to the Colab session or update the file paths accordingly.
7. Run the notebook cells in order.

Option 2 — Local Jupyter Notebook

1. Make sure Python is installed.

2. Install the required libraries:
   
   pip install pandas numpy matplotlib jupyter

3. Clone the repository:
   
   git clone https://github.com/srlokygood/Analysis-mobile-plan.git

4. Navigate to the project directory:
   
   cd Analysis-mobile-plan

5. Launch Jupyter Notebook:
   
   jupyter notebook

6. Open the ".ipynb" file and execute the cells in order.

---

🔁 Reproducibility Guide

To reproduce the complete analysis, follow these steps:

1. Load the "users", "usage", and "plans" datasets.
2. Examine the data structure and data types.
3. Identify and handle missing values and sentinel values.
4. Convert date variables to the appropriate data types.
5. Analyze missing values in "duration" and "length" according to "type".
6. Correct or handle unexpected values.
7. Create aggregated metrics grouped by "user_id".
8. Merge the relevant information using "user_id".
9. Calculate descriptive statistics.
10. Generate histograms and boxplots.
11. Analyze and evaluate outliers.
12. Create age-based customer segments.
13. Create usage-based customer segments.
14. Interpret the results and formulate conclusions.

---

👤 Author

Jair — Aspiring Data Analyst

This project was developed as part of my data analytics training, demonstrating practical skills in data exploration, data cleaning, quality assurance, statistical analysis, visualization, data aggregation, and customer segmentation.
