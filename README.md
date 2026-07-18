# 📈 Twitter (TWTR) Stock Market Analysis

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=python&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-1D9E75?style=for-the-badge)

A complete end-to-end **exploratory data analysis and statistical study** of Twitter's (TWTR) stock market performance from **January 2018 to March 2024** — covering data cleaning, hypothesis testing, time-series visualization, and a multi-panel Python dashboard.

---

## 🖥️ Dashboard Preview

> *4-panel Python dashboard built with Matplotlib*

| Panel | Focus Area |
|---|---|
| **Panel 1 — Close Price Timeline** | Full price arc from 2018 to 2024 |
| **Panel 2 — Yearly Average Close** | Year-over-year average comparison |
| **Panel 3 — Daily Trading Volume** | Volume spikes aligned with key events |
| **Panel 4 — Daily Price Spread** | Intraday High − Low volatility over time |

---

## 📁 Project Structure

```
twitter-stock-analysis/
│
├── 📂 data/
│   └── TWTR.xlsx                        # Raw dataset (2,264 rows)
│
├── 📂 notebooks/
│   └── Twitter_Stock_Analysis.ipynb     # Complete Jupyter Notebook
│
├── 📂 charts/
│   ├── plot1_stock_prices_over_years.png
│   ├── plot2_close_vs_date.png
│   ├── plot3_time_period_buttons.png
│   ├── plot4_complete_timeline.png
│   ├── plot5_wordcloud.png
│   └── plot6_dashboard.png
│
├── 📂 report/
│   └── Twitter_Stock_Market_Analysis_Report.docx
│
└── README.md
```

---

## 📌 Problem Statement

Twitter, Inc. was listed on the NYSE from November 2013 until October 2022, when it was taken private following Elon Musk's acquisition. This project analyses Twitter's complete stock market history within the dataset period to answer:

- How did Twitter's stock price evolve over 2018–2024?
- What were the statistical relationships between daily High, Low, and Close prices?
- Did trading volume and price level move dependently or independently?
- Which external events had the most visible impact on price and volume?

---

## 🗂️ Dataset Overview

| Property | Detail |
|---|---|
| **File** | TWTR.xlsx |
| **Raw Rows** | 2,264 |
| **Valid Rows (after cleaning)** | 2,259 |
| **Date Range** | 01 Jan 2018 – 08 Mar 2024 |
| **Null Rows Removed** | 5 (trailing Excel rows) |
| **Stock Ticker** | TWTR (Twitter, Inc.) |
| **Exchange** | NYSE (delisted October 2022) |

### Columns

| Column | Type | Description |
|---|---|---|
| `Date` | datetime64 | Trading date |
| `Open` | float64 | Opening price (USD) |
| `High` | float64 | Intraday highest price (USD) |
| `Low` | float64 | Intraday lowest price (USD) |
| `Close` | float64 | Closing price (USD) |
| `Adj Close` | float64 | Adjusted closing price (= Close; no dividends paid) |
| `Volume` | float64 | Total shares traded |

---

## ⚙️ Tech Stack

| Library | Purpose |
|---|---|
| **Python 3.x** | Core programming language |
| **Pandas** | Data loading, cleaning, and manipulation |
| **NumPy** | Numerical operations |
| **Matplotlib** | All charts, subplots, and dashboard |
| **Seaborn** | Enhanced statistical styling |
| **SciPy (stats)** | T-Test and Chi-Square hypothesis testing |
| **WordCloud** | Word cloud generation |
| **OpenPyXL** | Reading `.xlsx` dataset |

---

## 🔧 Data Cleaning Steps

- Loaded `.xlsx` with `pd.read_excel()`
- Identified **5 trailing null rows** (Excel export artefact) — removed with `df.dropna()`
- Verified `Adj Close == Close` throughout (no dividends, no splits)
- Extracted `Year` column from `Date` for year-wise grouping
- Reset index after cleaning for sequential ordering

---

## 📊 Statistical Description

| Statistic | Open | High | Low | Close | Volume |
|---|---|---|---|---|---|
| Count | 2,259 | 2,259 | 2,259 | 2,259 | 2,259 |
| Mean | $36.02 | $36.70 | $35.34 | $36.00 | 21,751,860 |
| Std Dev | $14.12 | $14.37 | $13.83 | $14.09 | 19,099,880 |
| Min | $13.95 | $14.22 | $13.73 | $14.01 | 0 |
| 25% | $25.55 | $26.22 | $24.91 | $25.41 | 12,335,300 |
| Median | $35.42 | $36.10 | $34.82 | $35.49 | 16,913,050 |
| 75% | $44.21 | $45.02 | $43.33 | $44.14 | 24,280,820 |
| Max | $78.36 | $80.75 | $76.05 | $77.63 | 269,213,100 |

---

## 🧪 Statistical Tests

### T-Test (Independent Two-Sample)

Null Hypothesis (H₀): No significant difference exists between the means of the two columns being compared. Significance level: **α = 0.05**

| Test Pair | T-Statistic | P-Value | Decision | Conclusion |
|---|---|---|---|---|
| High vs Low | 3.2419 | 0.001196 | **Reject H₀** | Significant difference exists ✓ |
| High vs Close | 1.6442 | 0.100205 | Accept H₀ | No significant difference |
| Low vs Close | −1.5989 | 0.109904 | Accept H₀ | No significant difference |

### Chi-Square Test (Close Price Category vs Volume Category)

| Parameter | Value |
|---|---|
| Chi-Square Statistic | 8.3938 |
| P-Value | 0.0782 |
| Degrees of Freedom | 4 |
| Decision | **Accept H₀** (p > 0.05) |
| Conclusion | Close Price and Volume are statistically **independent** |

> Note: 96%+ of trading days fell in the "Low Volume" bin, limiting the test's sensitivity. Rare high-volume spikes do align with major events but are too infrequent to reach significance.

---

## 📈 Visualizations

### 1. Stock Prices Over the Years
All four price lines (Open, High, Low, Close) plotted together from 2018 to 2024, revealing the full price arc including the COVID dip and acquisition spike.

### 2. Close Price vs Date (Area Chart)
Isolated Close price with a fill-area to highlight prolonged periods of high and low valuation.

### 3. Year-wise Time Period Breakdown
Individual yearly subplots for precise trend analysis within each calendar year.

### 4. Complete Annotated Timeline
Full Close price line with vertical markers for four key events:
- 📅 Jan 2018 — Dataset period begins
- 🔴 Mar 2020 — COVID-19 market crash (all-time low ~$14)
- 🟢 Apr 2022 — Musk acquisition offer ($54.20/share; stock surged to ~$70+)
- ⚫ Oct 2022 — Twitter delisted from NYSE

### 5. Word Cloud
Visual summary of dominant analysis themes — market, price, trend, volatility, acquisition, decline, COVID, delisted.

### 6. Python Dashboard (4-Panel)
Matplotlib dashboard combining the Close timeline, yearly averages bar chart, daily volume bars, and daily High−Low spread.

---

## 💡 Key Insights

| # | Insight |
|---|---|
| 1 | Twitter's Close price ranged from **$14.01 (Mar 2020)** to **$77.63 (Apr 2022)** — a 5.5× swing |
| 2 | **High vs Low means are significantly different** (p = 0.001); Close sits in the same band as both over time |
| 3 | **Close price and Volume are statistically independent** — price was event/sentiment-driven, not volume-driven |
| 4 | The **COVID-19 crash** (Mar 2020) caused the largest single-period price decline in the dataset (~60% from 2018 peak) |
| 5 | The **Musk acquisition offer** (Apr 2022) triggered the highest-ever price spike and a record volume day (~269M shares) |
| 6 | **2020 had the lowest yearly average** close (~$20); **2023 had the highest** (~$53) driven by post-delisting OTC trading |
| 7 | **Adj Close = Close throughout** — Twitter never paid dividends or executed stock splits |
| 8 | Daily price spread (High − Low) averaged under $2 during calm periods, spiking to **~$14** during extreme volatility |
| 9 | Post-delisting (2023–2024) OTC trading continued in the **$30–$80 range**, suggesting continued investor interest |
| 10 | Volume exceeded 100M shares on only a handful of days — confirming event-driven spikes over sustained high activity |

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/your-username/twitter-stock-analysis.git
cd twitter-stock-analysis
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy wordcloud openpyxl
```

### 3. Launch the notebook
```bash
jupyter notebook notebooks/Twitter_Stock_Analysis.ipynb
```

### 4. Run all cells in order
The notebook is structured task-by-task:
- **Task 1** — Cells 1–6 (Data Analysis)
- **Task 2** — Cells 7–9 (Statistical Tests)
- **Task 3** — Cells 10–16 (Visualizations & Dashboard)
- **Final** — Cell 17 (Summary Conclusion)

---

## 📋 Task Completion Summary

| Task | Sub-Tasks | Status |
|---|---|---|
| Task 1 — Data Analysis | Load data, column insights, null check, describe(), missing values | ✅ Complete |
| Task 2 — Statistical Tests | T-Test (3 pairs), Chi-Square, insights | ✅ Complete |
| Task 3 — Visualization | 6 plots including dashboard and word cloud | ✅ Complete |
| Documentation | Full Word report (12 pages) | ✅ Complete |
| **Total** | **All tasks** | **✅ Done** |

---

## 👨‍💻 Author

**Vaibhavi Hambire**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/vaibhavi-hambire)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:hambirevaibhavi21@gmail.com)
---

## 📄 License

This project is open source under the [MIT License](LICENSE).

---

⭐ **If you found this project useful, consider giving it a star!**
