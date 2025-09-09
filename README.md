# Excel Analytics Project – Results, Dataset & Interactive Charts

This project delivers a complete **Excel-based analysis** that combines raw data, a curated results summary, and interactive charts.This workbook contains a monthly time-series (Series 20) with cleaning, descriptive analysis, forecasting, and a regression summary.

## 🎯 Objectives
- Provide a **Excel workbook** that contains the **dataset**, **results/KPIs**, and **visual analysis** (graphs & charts).

## Quick Preview (Sheets)
### 1) `Raw Data`
- **Purpose:** Source time series used for all downstream analysis.
- **Rows:** 67  
- **Date span:** **Feb-2017 → Aug-2022** (monthly)
- **Columns:**  
  - `date` (month start)  
  - `value` (numeric)  
  - `series_id` (always “Series 20”)
- **Notes:** Contains occasional blanks; the cleaned sheet below standardizes types and fills structure.

---

### 2) `Series_actual20` (Clean + Descriptive stats)
- **Purpose:** Cleaned series with helpers for analysis and a built-in “Descriptive Analysis & Findings” block.
- **Rows:** 67
- **Key columns:**  
  - `Periods` (1…67 index)  
  - `Date` (monthly)  
  - `Demand` (numeric series used for analysis)  
  - `Series_id` (Series 20)  
  - `Year`, `Month` (derived)  
  - `Outlier` (all entries marked **Ok**)
- **Descriptive Analysis (in-sheet table):**  
  - Mean, Median, Mode  
  - Standard Deviation & Sample Variance  
  - Kurtosis, Skewness  
  - Range, Min, Max, Sum, Count (= **67**)  
  - Quartiles **Q1**, **Q3**, **IQR**, **Upper/Lower bounds**  
  - **Trend (slope & intercept):** slope ≈ **−0.158** per period; intercept ≈ **4.695**  
    > Interpretation: a mild downward linear trend over time.

---

### 3) `Master sheet` (Modeling, Forecasts & Error Metrics)
- **Purpose:** Builds features and calculates forecasts + residual diagnostics.
- **Rows:** ~79 | **Columns:** 31
- **What’s inside:**  
  - **Feature engineering:** month dummies `Jan…Nov` (December as baseline) + `Periods` index.  
  - **Forecast:** linear regression with **trend + seasonal dummies** → `Forecast` column.  
  - **Residuals:** `Deviation`, `Abs. Dev.`, `% Abs. Dev / Data`, `Sq. Dev`.  
  - **Alternative model:** `Exponential Smoothing method` with its own residuals (`Deviation.1`, etc.).  
  - **Accuracy metrics:** in-sheet **MSE / MAD / MAPE** entries provided for both models.
- **How to read it:**  
  - Compare **Forecast** vs **Demand** and check residual columns for error patterns.  
  - Use the metric cells (MSE/MAD/MAPE) embedded in the sheet to compare **Regression** vs **Exponential Smoothing** performance.

---

### 4) `Regression - Matrix` (Excel ToolPak output)
- **Purpose:** Full regression summary table (Excel Data Analysis ToolPak).
- **Setup (inferred):** Dependent variable = **Demand**; predictors = **Periods** + **11 month dummies (Jan–Nov)**; **n = 67** observations.
- **Headline stats:**  
  - **Multiple R:** ~ **0.362**  
  - **R²:** ~ **0.131** (Adjusted R² ≈ **−0.062**)  
  - **ANOVA:** **F ≈ 0.679**, **Significance F ≈ 0.764** (model not statistically significant at 0.05)  
- **Coefficients table:** Intercept + `Periods` + monthly dummies; many monthly coefficients are negative relative to the **December** baseline (the omitted month), reflecting seasonal differences.

### Executive Summary
- **Date span:** Feb 2017 – Aug 2023 (monthly)
- **Overall trend:** mild **downward** linear trend (slope ≈ **−0.158** per period)
- **Models evaluated:** Linear Regression (trend + monthly seasonality) vs **Exponential Smoothing**
- **Best short-term fit:** **Exponential Smoothing** (lower error on MAD/MSE and sMAPE)

### Forecast Accuracy (Actual vs Forecast)
| Model                     | MSE    | MAD   | MAPE (%) | sMAPE (%) |
|--------------------------|--------|-------|----------|-----------|
| Regression (trend+month) | **160.00** | **10.31** | 160.34   | 68.64     |
| Exponential Smoothing    | **128.60** | **9.20**  | 285.03   | **53.42** |

> **Why sMAPE?** series has very small (near-zero) values at times. This makes **MAPE** unreliable (it can explode). **sMAPE** is symmetric and robust around zeros—use it (and **MAD/MSE**) to compare models.



### Key Findings
1. **Signal:** The series shows **small negative trend** and **noticeable month-to-month volatility**; seasonality exists but is **not strongly explanatory** on its own.
2. **Modeling:**  
   - **Exponential Smoothing** handles short-term dynamics better here (lower **MSE**, **MAD**, **sMAPE**).  
   - The linear + seasonal regression explains limited variance (low practical R² in ToolPak output), so treat it as a **baseline** rather than a production model.
3. **Error profile:** Residuals are **heterogeneous** (size varies over time). Prefer **sMAPE/MAD** for monitoring; avoid relying solely on MAPE due to zeros.
4. **Data hygiene:** The workbook uses a clean, tabular structure with derived time fields—good foundation for BI tools or automation later.

### Conclusions
- For **operational forecasts**, adopt **Exponential Smoothing** as the default baseline and track **sMAPE** and **MAD** weekly/monthly.  
- Keep the **regression view** for interpretability (trend + seasonal effects), but don’t rely on it for accuracy-critical decisions.  
- Where feasible, enrich with external drivers (price/promos, weather, macro-indexes) if you want a step-change in accuracy.

### How this helps the business
- **Inventory & Procurement:** Use the ES forecast to set **order quantities** and **safety stock**; trigger review when sMAPE spikes above a threshold (e.g., **>60%**).  
- **Staffing & Operations:** Align rosters with the **weekly/monthly forecast** and observed seasonal pockets; dampen schedules when the model signals downturns.  
- **Budgeting & Targets:** Build **rolling forecasts**; compare actuals vs forecast (**MAD** and **sMAPE** trends) to detect drift early and re-plan.  
- **Promotions & Timing:** If certain months consistently underperform, **time promos or discounts** to smooth demand or protect margin.  
- **Exception Management:** Flag **anomalies** (e.g., |residual| > 2× MAD) for root-cause analysis (data errors, supply issues, one-off events).

---

**License:** MIT (add a `LICENSE` file if you’d like others to reuse your work).
