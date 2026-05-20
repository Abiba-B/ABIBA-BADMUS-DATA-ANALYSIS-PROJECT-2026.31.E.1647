# Crude Oil Production and Evacuation Analytics (Abiba Badmus)

EMBA Capstone project focused on identifying operational drivers of crude oil production shortfalls and evaluating evacuation-capacity interventions for throughput improvement.

## Project Overview

This project analyzes OML 18 operational data to answer:

1. What factors are most associated with daily production shortfalls?
2. Which capacity interventions are linked to the strongest shortfall recovery outcomes?

The report is built with Quarto using both R and Python code blocks.

## Business Objectives

- Quantify zone- and station-level performance gaps versus budget.
- Test whether performance differences are statistically meaningful.
- Measure the relationship between evacuation capacity and shortfall.
- Build regression-based scenario estimates for capacity expansion decisions.

## Methods Used

- Exploratory Data Analysis (EDA)
- Data visualization
- Hypothesis testing (ANOVA / non-parametric comparison)
- Correlation analysis
- Regression modeling (including robust inference)

## Tech Stack

- Quarto
- R
- Python
- CSS (custom report styling)

Python dependencies are listed in `requirements.txt`.

## Repository Structure

```text
.
|-- abiba_capstone_v2.qmd
|-- abiba_capstone_v2.html
|-- abiba_report.css
|-- requirements.txt
|-- data/
|   `-- .gitkeep
|-- docs/
`-- oml18-capstone-abiba/
```

## Setup

From this folder:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Install Quarto and ensure R is available on your machine.

## How to Render

```bash
QUARTO_PYTHON=".venv/bin/python" quarto render abiba_capstone_v2.qmd
```

Generated output:

- `abiba_capstone_v2.html`

## Data & Privacy Notes

- Raw source datasets are not to be pushed to GitHub.
- Keep input files local inside `data/`.
- The folder structure is preserved in Git using `.gitkeep`.

## Author

Abiba Badmus  
LBS EMBA Candidate (2026)
