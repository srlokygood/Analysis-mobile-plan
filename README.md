# Customer Segmentation by Age and Call/Text Usage for a Telecom Operator

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black)

Exploratory analysis of Telecomm's customer demographics, call/text records and subscription plans to understand usage behavior and segment customers. Adults aged 30–60 are the largest age group, and most customers fall into the medium-usage segment (5–10 messages or calls).

![Main chart](images/main-chart.png) <!-- [MISSING: add a key chart, e.g. age distribution or usage segments] -->

## Business Question

How can a telecom company turn raw customer data into insights about customer behavior and service usage? Specifically, who are the customers (by age), how much do they call and text, and how reliable is the data used to answer those questions? Understanding this is the foundation for plan design and service optimization.

## Data

- **Source:** Telecomm customer data [MISSING: origin of the dataset, e.g. bootcamp project, public dataset].
- **Records and period:** [MISSING: number of users, usage records, and date range].
- **Tables used:**
  - `users`: `user_id`, `age`, `city`, `plan`, `reg_date`, `churn_date`
  - `usage`: `id`, `user_id`, `type` (call/text), `duration`, `length`, `date`
  - `plans`: `plan_name`, `messages_included`, `gb_per_month`, `minutes_included`, `usd_monthly_pay`, `usd_per_gb`, `usd_per_message`, `usd_per_minute`

## Process

- **Initial exploration:** reviewed data types, dimensions, missing values and unique values, and confirmed that the tables relate through `user_id`.
- **Cleaning (pandas/NumPy):**
  - Converted `reg_date` and `date` to datetime.
  - Replaced the sentinel value `-999` in `age` with the column mean.
  - Replaced `?` in `city` with missing values.
  - Checked for future dates (no records needed modification).
  - Validated `duration` for `call` records and `length` for `text` records, converting unexpected values to `NaN`.
- **Aggregation:** grouped usage records by `user_id` into `cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada` and `longitud_mensajes_total`, then merged them into `users`.
- **Statistics:** mean, standard deviation, min/max, quartiles and median, plus histograms and boxplots for distributions and outliers. Extreme values were kept when there was no evidence they were errors.
- **Segmentation:**

| Age segment | Range |
|---|---|
| Young customers | Under 30 |
| Adults | 30–60 |
| Older adults | Over 60 |

| Usage segment | Criteria |
|---|---|
| Low | Fewer than 5 messages or calls |
| Medium | 5–10 messages or calls |
| High | More than 10 messages or calls |

- **Data model:** three tables joined by `user_id` (`users` ↔ `usage`, and `users.plan` ↔ `plans.plan_name`).

![Data model](images/data-model.png) <!-- [MISSING: diagram of table relationships] -->

- **Key code:** [MISSING: 1–2 snippets, e.g. the `groupby` aggregation and the segmentation logic]

## Findings

1. Most customers are between 30 and 60 years old, making adults the largest age segment [MISSING: exact % or count].
2. Medium usage is the predominant segment, followed by low usage; high-usage customers are a smaller share [MISSING: % for each].
3. Total text message length shows high outliers reaching about 2,000 characters, and the message count is right-skewed (most customers send few messages) [MISSING: share of customers affected].
4. Call count is roughly bell-shaped, and call duration is right-skewed, with most calls being short.

## Recommendations

- Analyze which plans each age group uses and at which usage levels, to adjust plan design.
- Compare usage against plan allowances to detect overage charges and poor plan fit.
- Track monthly usage trends to spot changes in customer activity.
- Explore message length (characters) as a complement to message frequency.
- Address data quality at the source (sentinel values, `?` entries, mismatched `type`/`duration`/`length`) before further modeling.

## Limitations

- The analysis is exploratory and descriptive: it does not explain why usage differs or predict churn.
- Replacing `-999` ages with the mean may distort the age distribution.
- Usage segments are based on simple thresholds, not on plan allowances.
- Plan information and `churn_date` were not analyzed, so no conclusions about plan suitability, revenue or churn can be drawn.
- Outliers were kept without confirming whether they are genuine.

## How to Open It

- **Google Colab:** open the `.ipynb` notebook in [Google Colab](https://colab.research.google.com/) (File → Upload notebook), upload the datasets or update the file paths, and run the cells in order.
- **Local Jupyter:**
  ```bash
  git clone https://github.com/srlokygood/Analysis-mobile-plan.git
  cd Analysis-mobile-plan
  pip install -r requirements.txt   # [MISSING: add requirements.txt, or use: pip install pandas numpy matplotlib jupyter]
  jupyter notebook
  ```
  Then open the `.ipynb` file and run the cells in order.

## Tools

Python, pandas, NumPy, Matplotlib, Jupyter Notebook, Google Colab
