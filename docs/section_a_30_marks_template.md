# Section A Template (30 Marks) - Abiba Badmus

## 1) Executive Summary (10 marks)

### Business context (2 sentences)
I am Head of Alternative Crude Oil Evacuation, responsible for tracking daily production performance across multiple zones and ensuring evacuation logistics meet Nigeria's production targets — including OPEC's 1.5 million bpd allocation and a 2026 annual target of 18 million barrels. Production shortfalls against daily budgets across different flow stations and zones represent a direct financial and compliance exposure that requires data-driven intervention.

### Research question (1 sentence)
Which zone, station, and capacity factors most significantly explain the variance between budgeted and actual daily crude production, and what operational adjustments would close the gap?

### Three key findings (replace brackets with your computed numbers)
1. Zone [X] consistently underperforms budget by [Y] bbl/day on average, a difference that is statistically significant at p = [value].
2. Evacuation utilization rate shows a [positive/negative] correlation of r = [value] with actual production attainment, suggesting capacity [is/is not] a binding constraint.
3. Regression analysis identifies [top driver] as the strongest predictor of production shortfall, with a coefficient of [value] — each one-unit change corresponds to a [Z] bbl change in daily output.

### One recommendation (with projected impact)
Prioritize evacuation capacity reallocation to [Zone/Station], which is projected to improve daily throughput attainment by approximately [X%], contributing an estimated [Y million barrels] additional evacuated volume toward the 2026 annual target.

## 2) Professional Disclosure (10 marks)

**Job title:** Head, Alternative Crude Oil Evacuation
**Organisation sector:** Upstream oil and gas operations — national crude production, zone-level throughput management, and evacuation logistics

### Technique 1 — Exploratory Data Analysis
As Head of Alternative Crude Oil Evacuation, every working day begins with a review of the previous day's production figures: did each flow station meet its `BUDGET` target, and what is the gap in `ACTUAL`? Before any statistical test can be run, I need to understand the distributional shape of that gap across 625 daily records spanning four flow stations (ALK, CC1, CC2, CC3) and two zones. Are shortfalls concentrated in certain stations or spread evenly? Are there extreme outlier days — perhaps caused by pipeline maintenance or force majeure — that would distort any zone-level comparison? EDA answers these questions first and ensures that every downstream test and model rests on verified, understood data rather than unexamined assumptions. This mirrors the operational health-check I conduct before presenting production performance to senior management.

**Alternative considered:** Jumping directly to regression on the combined dataset. Rejected because undetected outliers in `ACTUAL` (including the blank/zero values in early January) would silently bias the regression coefficients and produce misleading conclusions about which zones are genuinely underperforming.

**Limitation:** EDA is descriptive only. A zone that visually appears to underperform may still not do so significantly once sample variance is accounted for. Formal tests are required before drawing operational conclusions.

### Technique 2 — Data Visualization
Upstream operations leadership does not make decisions from tables of numbers. The briefings I prepare for management are built around time-series charts of daily `ACTUAL` vs `BUDGET` production, zone-level comparison bar charts, and capacity utilization trend lines drawn from `evacuation_capacity` and `evacuation_utilization`. The `DATE` field in both datasets enables a full January–May 2026 timeline view, while `ZONE` and `FLOW_STATIONS` provide the categorical groupings needed for comparative charts. Visualization allows me to spot bottleneck periods — weeks where Zone 1 (CC2/CC3) and Zone 2 (ALK/CC1) diverge — in a format that a non-technical executive can act on immediately. These charts will be directly reusable in my next production performance presentation.

**Alternative considered:** Summary statistics tables only. Rejected because tables do not communicate temporal patterns or cross-zone divergence — precisely the patterns that matter most for evacuation scheduling decisions.

**Limitation:** Visual patterns can appear more decisive than they are. A chart showing Zone 2 consistently below budget could be driven by one outlier quarter. All visual findings in this analysis are followed by formal hypothesis tests before any policy action is recommended.

### Technique 3 — Hypothesis Testing
My organization operates four flow stations across two zones, and a persistent management question is whether Zone 1 and Zone 2 perform statistically differently against their respective `BUDGET` targets — or whether the apparent difference is within normal operational variance. If the difference is statistically significant (ANOVA or Welch t-test on production shortfall by `ZONE`), that is a resource allocation issue: it justifies redirecting evacuation capacity or maintenance attention to the underperforming zone. If it is not significant, the variability is systemic and calls for a different intervention. A p-value and effect size turn what is currently an informal management opinion into a defensible, data-backed operational directive.

**Alternative considered:** Kruskal-Wallis non-parametric test as the primary method, since daily production data often exhibits skew. This will be run as a robustness check alongside the parametric ANOVA.

**Limitation:** The dataset has approximately 312 records per zone on average. After splitting by both `ZONE` and `FLOW_STATIONS`, some station-level subgroups may have fewer than 30 observations, reducing statistical power for station-level comparisons. Zone-level comparisons are adequately powered; station-level results will be interpreted with explicit power caveats.

### Technique 4 — Correlation Analysis
Before including `evacuation_capacity` and `evacuation_utilization` from the evacuation dataset as predictors in a regression model, I need to establish whether they are actually related to production performance. My operational hypothesis is that low utilization relative to capacity (`evacuation_utilization / evacuation_capacity`) should correlate with better production attainment — meaning the pipeline has headroom and is not constraining output. Correlation analysis on the merged daily dataset (joined on `DATE` and `ZONE`) will confirm or refute this hypothesis and reveal which evacuation variables are worth including as regression predictors. It also guards against multicollinearity: if `evacuation_capacity` and `evacuation_utilization` are highly correlated with each other, entering both in the regression would produce unstable coefficients.

**Alternative considered:** Entering all four evacuation and production variables directly into a regression without prior screening. Rejected because this approach regularly produces inflated standard errors and misleading coefficient signs when predictors are correlated.

**Limitation:** Correlation measures linear association only. The relationship between evacuation utilization and production attainment may be non-linear — for example, utilization below 40% may have no impact on output, while utilization above 80% may sharply constrain it. This will be explored visually before the regression is specified.

### Technique 5 — Multiple Regression
The commercial and strategic purpose of this analysis is a daily production attainment model: given a station's `BUDGET` target, its `ZONE`, its `evacuation_capacity`, and its `evacuation_utilization`, what `ACTUAL` production should be expected? A regression equation with `ACTUAL - BUDGET` shortfall as the outcome variable provides coefficient-level answers to the question every evacuation planning meeting asks: *which factor, if improved by one unit, recovers the most daily barrels?* If `evacuation_utilization` has a coefficient of +150 (bbl per percentage point of utilization), that directly translates into a fleet-sizing recommendation. Nigeria's 2026 budget benchmark is 1.84 million bpd; every coefficient in this model maps to a recoverable share of that target.

**Alternative considered:** Random forest regression to capture non-linear interactions between zone, station, and capacity variables. Rejected on two grounds: the dataset (625 records) is too small to reliably generalize a tree ensemble, and the output would not be interpretable at the coefficient level — which is the format required for a management briefing or a policy recommendation to the operations director.

**Limitation:** The regression assumes approximately linear relationships between the predictors and the shortfall outcome. If the true relationship is threshold-based (e.g., output only suffers once capacity falls below a critical level), diagnostic plots will reveal this and a transformed specification will be applied.

## 3) Data Provenance (10 marks)
- **Source system:** Internal daily production reporting system, maintained by the Upstream Operations department.
- **Datasets used:**
  - `daily production report.csv` — 625 daily records covering flow-station-level budget vs. actual production by zone.
  - `evacuation_report.csv` — 250 daily records covering evacuation capacity and utilization by zone.
- **Collection method:** Operational data extracted directly from internal reporting systems. Records represent daily snapshots of throughput and logistical capacity across active evacuation zones.
- **Time period covered:** January 2026 to approximately May 2026 (confirm exact end date).
- **Sample frame:** All active flow stations and evacuation zones within the Alternative Crude Oil Evacuation program. Stations or zones with zero operational activity in the period are included as-is.
- **Selection bias:** No deliberate sampling was applied. The dataset represents the full operational population for the period. However, some ACTUAL values appear as zero or blank for early days — these will be treated as non-operational periods, not as missing data errors.
- **Anonymization approach:** Flow station identifiers and zone codes are internal operational designations. No employee or personal data is present. No additional masking is required.
- **Ethical considerations:** Dataset is extracted from internal company systems for which I hold operational accountability. Use is limited to this academic exercise. No external parties or third-party client data are involved.
- **Organizational approval:** [Confirm internal sign-off from line manager or data governance contact.]
