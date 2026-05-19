# Case Study Recommendation - Abiba Badmus

## Recommended case
- Best-fit case: `CS1 - Exploratory & Inferential Analytics`
- Fit score: `9/10`

## CSV evidence profile
| File | Rows | Cols | Key fields |
|---|---|---|---|
| `daily production report.csv` | 625 | 5 | DATE, BUDGET, ACTUAL, FLOW_STATIONS, ZONE |
| `evacuation_report.csv` | 250 | 4 | DATE, evacuation_capacity, evacuation_utilization, ZONE |
    
## Data requirement check
- Row depth: `Met` (875 combined records, daily frequency)
- Numeric variables: `Met` (BUDGET, ACTUAL, evacuation_capacity, evacuation_utilization)
- Categorical variables: `Met` (ZONE, FLOW_STATIONS)
- Date field: `Met` (daily DATE column, Jan–May 2026)
- Joinable across files on DATE + ZONE: `Met`
- Requirement status: `Full — ready to code`

## Why CS1 is the strongest route and not CS2 or CS3
- Your business question is fundamentally inferential: which zones and conditions drive production shortfalls against budget?
- Prediction alone without explanation adds little operational value here.
- CS1 allows EDA, zone/station hypothesis testing, correlation, and regression in a direct sequence that maps to evacuation planning decisions.
- Every technique has a clear defence answer tied to daily crude logistics.

## Best outcome and target framing for maximum marks
- Primary question: which combination of zone, station, and capacity factors explains the gap between budgeted and actual daily production?
- Target variable for regression: `ACTUAL - BUDGET` (budget shortfall) or `evacuation_utilization / evacuation_capacity` (utilization rate)
- High-mark output set:
  1. EDA of production distribution and budget-actual variance by zone and station
  2. Zone/station comparison using significance testing
  3. Correlation between evacuation utilization and production attainment
  4. Multiple regression quantifying shortfall drivers
  5. One actionable capacity or scheduling recommendation with numeric impact estimate

## No additional data needed
Both CSVs are present and structurally complete. The files should be joined on DATE and ZONE before analysis.

## Minor pre-analysis data check to perform
- Verify whitespace/formatting in BUDGET/ACTUAL columns (some rows may contain `  -   ` as zero)
- Confirm whether ZONE labels are consistent across both files before joining
