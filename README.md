# Sleep Quality & Lifestyle: Wearable Data Analysis

**Biomedical Engineering · Python · Exploratory Data Analysis · Statistical Modeling · Digital Health**

## Overview

Sleep quality depends on more than the number of hours spent asleep. This academic data-analysis project examines how **perceived stress, caffeine consumption, and screen exposure before bedtime** are associated with three dimensions of sleep:

- **Sleep quality:** `sleep_score`
- **Sleep-onset latency:** `sleep_latency_minutes`
- **Sleep duration:** `duration_minutes`

We used Python to explore wearable-related sleep records, formulate and evaluate statistical hypotheses, check model assumptions, compare groups, and communicate our findings in a research presentation. The study focuses on **statistical associations**, not causal effects or clinical recommendations.

## Dataset at a glance

| Item | Description |
| --- | --- |
| Observations analyzed | 20,000 |
| Variables in the original dataset | 45 |
| Unique pseudonymous user IDs | 2,000 |
| Main explanatory variables | `stress_score`, `caffeine_mg`, `screen_time_before_bed_min` |
| Sleep outcomes | `sleep_score`, `sleep_latency_minutes`, `duration_minutes` |
| Missing values in the supplied dataset | 0 |

The dataset is **not included in this public repository**. This is an intentional data-sharing decision, not a missing project file. The repository publishes the analysis code, documentation, and research presentation only. See [Running the analysis](#running-the-analysis) for instructions for users who already have legitimate access to a compatible dataset.

## Research questions

1. How is perceived stress associated with sleep quality, sleep latency, and sleep duration?
2. Do caffeine intake, pre-bedtime screen exposure, and stress have detectable individual or interaction effects on sleep outcomes?
3. Are the patterns consistent across exploratory visualizations, factorial statistical analyses, permutation tests, and multiple regression?

## Analytical workflow

1. **Data preparation:** Load the dataset with pandas, select six primary analytical variables, review missing values and duplicates, and prepare the analysis dataframe.
2. **Exploratory data analysis (EDA):** Examine descriptive statistics, histograms, density plots, boxplots, scatterplots, correlation and covariance matrices, parallel coordinates, and radar charts.
3. **Grouping:** Divide stress, caffeine intake, and screen exposure into **low, medium, and high groups using sample-based tertiles** (`pandas.qcut`). These groups are relative to the dataset and are not clinical thresholds.
4. **Assumption checks:** Apply Shapiro–Wilk and Levene tests, Henze–Zirkler multivariate normality testing, Box's M testing, and diagnostic plots.
5. **Factorial inference:** Fit three-way ANOVA models and a three-way MANOVA, including interactions, with Tukey HSD post-hoc comparisons where applicable.
6. **Permutation tests:** Use Freedman–Lane residual permutations to examine selected univariate and multivariate effects when conventional model assumptions are questionable.
7. **Multiple regression:** Analyze each sleep outcome using continuous stress, caffeine, screen time, and a caffeine × screen interaction, with standardized coefficients and HC3-robust inference.
8. **Communication:** Summarize the findings, figures, statistical interpretation, and study limitations in a research presentation.

## Key findings

### 1. Higher stress was associated with lower sleep-quality scores

- **Pearson correlation:** `r ≈ -0.489` between `stress_score` and `sleep_score`.
- **Standardized regression coefficient for stress:** `β ≈ -0.489` in the reported multivariable model.
- **Sleep-quality regression R²:** approximately `0.23889`, meaning the model accounted for about **23.9% of variation** in `sleep_score` within this dataset.

Across multiple analyses, stress showed the most consistent association with sleep-quality scores.

### 2. Stress was not significantly correlated with total sleep duration

- **Pearson correlation:** `r ≈ -0.005` between stress and sleep duration.
- **Reported p-value:** approximately `0.447`.

The analysis did not find sufficient evidence of a linear relationship between these two variables. Sleep duration and reported sleep quality should therefore not be treated as interchangeable measurements.

### 3. Caffeine and screen exposure showed a small interaction involving sleep latency

The factorial and permutation analyses detected a **caffeine × screen exposure** interaction in relation to sleep-onset latency. Its effect was small, so statistical significance should not be interpreted as evidence of a substantial real-world impact.

The continuous multiple-regression model for latency had **R² ≈ 0.00007**, while the model for duration had **R² ≈ 0.00033**. Both values indicate negligible explanatory power for those particular linear models.

### 4. Statistical diagnostics mattered

Several normality and variance-homogeneity checks indicated violations of classical assumptions. The analysis therefore included permutation-based testing and heteroscedasticity-robust regression inference as complementary approaches. Findings should be considered in light of those diagnostics rather than interpreted from p-values alone.

## Tools and techniques

| Area | Tools and methods |
| --- | --- |
| Programming | Python, Jupyter Notebook |
| Data handling | pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Statistical analysis | SciPy, statsmodels, Pingouin, Patsy |
| Supporting utilities | scikit-learn |
| Methods | EDA, correlation analysis, ANOVA, MANOVA, Tukey HSD, Freedman–Lane permutation testing, multiple linear regression, robust standard errors |

**Scope:** This is a statistical data-analysis and modeling project. It does **not** claim to implement a trained machine-learning or deep-learning prediction system.

## Repository structure

```text
Sleep-Quality-Wearable-Data-Analysis/
├── README.md
├── Sleep_Quality_Analysis.ipynb
├── Sleep_Quality_Presentation.pdf
└── requirements.txt
```

- **`Sleep_Quality_Analysis.ipynb`** — Python code, statistical procedures, diagnostic plots, and analysis results.
- **`Sleep_Quality_Presentation.pdf`** — Spanish-language research presentation covering the research questions, methodology, statistical results, and conclusions.
- **`requirements.txt`** — Python dependencies used by the notebook.

## Running the analysis

The notebook uses an input CSV named `smartwatch_sleep_dataset.csv`. **That file is intentionally not distributed with this repository.** Anyone who already has an authorized copy of the compatible dataset can run the analysis locally:

1. Clone or download the repository.
2. Install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

3. Place your authorized dataset copy in the repository's root directory under this exact filename:

   ```text
   smartwatch_sleep_dataset.csv
   ```

4. Start JupyterLab and open `Sleep_Quality_Analysis.ipynb`:

   ```bash
   python -m jupyter lab
   ```

5. Run the notebook cells in sequence.

The notebook references the CSV using a relative path:

```python
df = pd.read_csv("smartwatch_sleep_dataset.csv")
```

**Reproducibility note:** The complete numerical analysis cannot be independently rerun from the public repository alone because the raw dataset is intentionally excluded. The notebook and slides document the analysis and its reported results. Some permutation tests use **9,999 permutations**, so execution can be computationally intensive.

## Limitations and responsible interpretation

- This is an **observational statistical analysis**: associations do not establish causation.
- The original dataset's collection or generation process was not independently established in this project, limiting conclusions about external validity.
- Creating low/medium/high groups from continuous variables can conceal within-group variation.
- With a large dataset, small effects may be statistically significant without being practically important.
- Some classical model assumptions were not satisfied; robust and permutation analyses help assess sensitivity but do not remove every limitation.
- Findings are intended for educational and analytical purposes, **not medical diagnosis or personalized health advice**.
- Raw data are excluded from this public repository to avoid redistributing user-level and health-related records.

## Project team

Collaborative academic project by:

- **Ana Florez**
- **Emanuel Giraldo**
- **Alejandro Rojas**

The accompanying presentation credits all three collaborators.

---

**Portfolio skills:** Biomedical Engineering · Python · Data Analysis · Statistical Modeling · Data Visualization · Digital Health · Research Communication
