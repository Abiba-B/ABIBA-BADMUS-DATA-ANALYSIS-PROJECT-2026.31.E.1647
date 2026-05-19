# OML 18 Capstone Analysis — Abiba Badmus

**LBS EMBA Cohort | AI-Powered Business Analytics Capstone**

---

## Business Question

What are the primary operational drivers of the production shortfall on OML 18 assets between January and May 2026, and what capacity interventions are associated with the most meaningful shortfall recovery?

---

## Dataset

| File | Description |
|------|-------------|
| `daily production report.csv` | Station-level daily actual and budgeted production (Jan–May 2026) |
| `evacuation_report.csv` | Daily evacuation capacity and utilization by zone (Zone 1 / Zone 2) |

> **Data governance note:** Raw CSV files contain commercially sensitive production data and are **not committed** to this repository. Contact the author for access subject to organisational data-governance approval.

---

## Repository Structure

    oml18-capstone-abiba/
    ├── README.md          ← this file
    ├── .gitignore
    ├── code/              ← Quarto source document
    │   └── abiba_capstone_v2.qmd
    ├── data/              ← data governance note only; raw files excluded
    │   └── README.md
    ├── notes/             ← working notes and exploratory scratch files
    └── outputs/           ← rendered HTML report
        └── abiba_capstone_v2.html

---

## How to Render

1. Clone the repository.
2. Place the raw CSV files in `data/` (see data governance note above).
3. Ensure R packages are installed: `tidyverse`, `ggplot2`, `patchwork`, `knitr`, `sandwich`, `lmtest`
4. Ensure Python packages are installed: `pip install -r requirements.txt` (file in `code/`)
5. Set the Python environment if needed:
   ```
   export QUARTO_PYTHON=/path/to/your/venv/bin/python
   ```
6. Render the document:
   ```
   quarto render code/abiba_capstone_v2.qmd
   ```

Rendered HTML is written to the document's working directory (move to `outputs/` as needed).

---

## Key Outputs

- Rendered HTML report with 5 analytical techniques: EDA, Visualization, Hypothesis Testing, Correlation, Regression
- Executive dashboard (KPI summary table)
- Scenario bounds table: 5,000 / 10,000 / 15,000 bbl/day capacity increase projections with HAC-robust confidence intervals
- OLS vs Newey-West HAC robust regression comparison
- Train-test split validation (Jan–Mar / Apr–May)

---

## Techniques Applied

| # | Technique | Key Finding |
|---|-----------|-------------|
| 1 | Exploratory Data Analysis | 86.4% of station-days below budget; CC2 highest mean deficit, CC3 highest persistence |
| 2 | Data Visualization | Shortfall worsens each month Jan–Apr; Jan–Apr trend formally significant |
| 3 | Hypothesis Testing | Station-level differences significant (η² ≈ 0.14); zone-level non-significant under K-W |
| 4 | Correlation | Evacuation capacity: Spearman ρ ≈ −0.33 with shortfall; robust across Pearson/Spearman/Kendall |
| 5 | Multiple Regression | 10k bbl/day capacity increase → ~5,602 bbl/day expected recovery (HAC scenario bounds included) |

---

## Author

Abiba Badmus  
Head of Alternative Crude Oil Evacuation, OML 18  
LBS EMBA Candidate, 2026

*Dataset citation:*  
Badmus, A. (2026). *OML 18 daily production and alternative evacuation dataset — January to May 2026* [Dataset]. Upstream Operations Department, OML 18. Available on request subject to organisational data-governance approval.
