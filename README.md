# Customer Segmentation by Age and Call/Text Usage for a Telecom Operator

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black)

Exploratory analysis of Telecomm's customer demographics, call/text records and subscription plans to understand usage behavior and segment customers. Adults aged 30–60 are the largest age group [MISSING: % of customers], and most customers fall into the medium-usage segment (5–10 messages or calls) [MISSING: % of customers].

![Main chart](images/main-chart.png) <!-- [MISSING: add a key chart, e.g. age distribution or usage segments] -->

## Business Question

How can a telecom company turn raw customer data into insights about customer behavior and service usage? Specifically, who are the customers (by age), how much do they call and text, and how reliable is the data used to answer those questions? Understanding this is the foundation for plan design and service optimization.

## Data

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

- **Key code:** [MISSING: 1–2 snippets, e.g. the `groupby` aggregation
