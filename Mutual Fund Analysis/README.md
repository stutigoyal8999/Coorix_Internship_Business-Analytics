# Mutual Fund Overview & Insights

**Project 1, Business Analytics Internship, Coorix**
**Author:** Stuti Goyal 

## Goal
Help a first-time investor compare mutual funds fairly by balancing return, cost, consistency and fund age, and deliver the results as a Python notebook, an Excel shortlist and a Power BI dashboard.

## Project structure
| File | Purpose |
|---|---|
| `notebook/Mutual Fund Analysis.ipynb` | Cleaning, description, normalization, scoring, insights |
| `data/comprehensive_mutual_funds_data.csv` | Raw dataset (814 funds) |
| `data/funds_clean.csv` | Cleaned data |
| `data/funds_powerbi.csv` | Data prepared for Power BI (adds Score, Rank, Top 30) |
| `Top_30_Funds.xlsx` | Top 30 funds, a lower-risk Top 10 sheet and a method sheet |
| `dashboard/Mutual Fund Dashboard.pbix` | Power BI dashboard |
| `dashboard/dashboard_preview.png` | Screenshot of the dashboard |

## Method
1. **Cleaning:** "-" placeholders and zeros that mean "not available" were converted to missing values; 14 funds with copy-pasted placeholder returns were excluded from ranking; no values were imputed.
2. **Description:** summary statistics, distributions, skewness and IQR outliers.
3. **Normalization:** MinMaxScaler (0 to 1) on 3-year return, expense ratio and fund age.
4. **Scoring:** `Score = 0.50 x Return + 0.20 x Cost + 0.20 x Consistency + 0.10 x Age`.
   - Return = scaled 3-year return
   - Cost = 1 minus scaled expense ratio
   - Consistency = 1 if the 1-year return is positive, else 0
   - Age = 1 for 5 to 10 years, falling linearly to 0 at the minimum (3) and maximum (17) in the data
   - Ties are broken by the lower expense ratio
5. **Risk** is analysed separately (not in the score) because adding it made the Top 30 collapse into only arbitrage/overnight or only high-risk equity funds. A lower-risk shortlist is provided in the Excel file.
6. **Sensitivity check:** four alternative weightings were tested to see how much the Top 30 changes.

## Key results
- 776 funds were ranked; the top-ranked fund is Quant Small Cap Fund (score 0.952).
- Equity holds the most AUM (Rs 1,354,232 Cr, 43.6%), followed by Debt (Rs 1,179,876 Cr, 38.0%).
- Debt is the cheapest fund type (0.36% average expense ratio); Equity averages 1.05%.
- Typical minimum: Rs 500 for a SIP and Rs 5,000 for a lumpsum.
- Median 3-year return rises with risk: 3.9% at level 1 to 26.2% at level 6.

## Limitations
- The dataset has 814 funds, not the 2,500+ mentioned in the brief.
- Returns are from one three-year window; past returns do not guarantee future results.
- Bank of India Credit Risk Fund (130.8% 1-year return) is an extreme value and was excluded from ranking.

## How to run
```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
jupyter notebook
```
Open the notebook and choose **Kernel → Restart & Run All**. The scripts read from `data/` and write `Top_30_Funds.xlsx` to the project folder.