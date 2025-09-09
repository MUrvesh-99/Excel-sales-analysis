# Excel Analytics Project

This repository contains an **Excel-based analysis** including raw data, results, and charts. It’s organized so reviewers can quickly preview key tables on GitHub, download the full workbook, and see screenshots of the graphs.

## What's Inside
```
.
├─ data/
│  └─ Series_actual20.xlsx         # Full Excel workbook (data + results + charts)
├─ previews/                       # CSV previews of the workbook sheets (first 20 rows)
│  ├─ <SheetName>_preview.csv
│  └─ ...
├─ assets/
│  └─ screenshots/                 # Add PNG/JPG screenshots of your charts/dashboards
│     ├─ overview.png
│     ├─ results.png
│     └─ trends.png
└─ README.md
```

## Quick Preview (Sheets)
- **Raw Data** — 67 rows × 3 cols; sample cols: date, value, series_id
- **Series_actual20** — 67 rows × 10 cols; sample cols: Periods, Date, Demand, Series_id, Year , Month, Outlier, Unnamed: 7
- **Master sheet** — 79 rows × 31 cols; sample cols: Date, Year, Month, Demand, Periods, Jan, Feb, Mar
- **Regression - Matrix** — 101 rows × 9 cols; sample cols: SUMMARY OUTPUT, Unnamed: 1, Unnamed: 2, Unnamed: 3, Unnamed: 4, Unnamed: 5, Unnamed: 6, Unnamed: 7

> The **previews/** folder contains CSV snapshots of each sheet (first 20 rows) so GitHub can render tables right in the browser.

## How to Open
1. Download `data/Series_actual20.xlsx` and open in **Microsoft Excel** (or Excel Online).  
2. Navigate to the sheets named above for **Results**, **Dataset**, and **Charts**.  
3. If slicers/pivot charts exist, use them interactively inside Excel.

## Charts & Screenshots
Add a few image exports of your charts to `assets/screenshots/` and reference them here:
<p align="center">
  <img src="assets/screenshots/overview.png" alt="Overview Charts" width="900">
</p>
<p align="center">
  <img src="assets/screenshots/results.png" alt="Results Summary" width="900">
</p>
<p align="center">
  <img src="assets/screenshots/trends.png" alt="Trends & Comparisons" width="900">
</p>

## Tips
- For large workbooks, consider keeping raw data in a separate file (`data/raw/`) and the final analysis in a **clean** workbook.  
- If charts don’t show on GitHub, include a **PDF export** (e.g., `exports/report.pdf`) or screenshots as above.  
- Version notes (optional): track key changes in a `CHANGELOG.md`.

---

**License:** MIT (add a `LICENSE` file if you’d like others to reuse your work).