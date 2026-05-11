# Customer Behavior & Revenue Analysis â€” NovaRetail+ (2024)

Exploratory correlation analysis identifying the behavioral factors most strongly associated with annual revenue per customer on a Latin American e-commerce platform.

---

## Business Problem

The Growth & Retention team at **NovaRetail+** needed to understand which customer behaviors drive annual revenue, in order to prioritize strategic initiatives for 2024 year-end planning.

**Core business question:**
> *What customer behavioral factors are most strongly associated with annual revenue generated per user?*

---

## Project Objective

Conduct a structured correlational analysis across 15,000 customer records to identify, quantify, and interpret the behavioral signals most relevant to revenue performance â€” and to distinguish statistically significant associations from practically meaningful ones.

---

## Dataset

| Attribute | Detail |
|---|---|
| Records | 15,000 customers |
| Features | 12 variables |
| Missing values | None |
| Source | Internal platform data (NovaRetail+, 2024) |

**Variable overview:**

| Variable | Type | Description |
|---|---|---|
| `id_cliente` | Identifier | Unique customer ID |
| `edad` | Numeric | Customer age |
| `nivel_ingreso` | Numeric | Estimated customer income |
| `visitas_mes` | Numeric | Monthly platform visits |
| `compras_mes` | Numeric | Monthly purchases |
| `gasto_publicidad_dirigida` | Numeric | Targeted ad spend attributed to user |
| `satisfaccion` | Numeric | Satisfaction score (1â€“5 scale) |
| `miembro_premium` | Binary | Premium membership (1 = Yes, 0 = No) |
| `abandono` | Binary | Churn indicator (1 = Churned, 0 = Active) |
| `tipo_dispositivo` | Categorical | Device type (mobile, desktop, tablet) |
| `region` | Categorical | Geographic region (north, south, east, west) |
| `ingreso_anual` | Numeric | **Target variable** â€” Annual revenue per customer |

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.9-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Manipulation-lightblue)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-teal)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-green)
![SciPy](https://img.shields.io/badge/SciPy-Statistical%20Analysis-purple)

---

## Methodology

This project follows a structured EDA and correlation analysis pipeline:

**1. Data Loading & Inspection**
Validated dataset structure, dtypes, null counts, and shape.

**2. Data Cleaning**
Corrected `edad` dtype from `float64` to `int64`. No null imputation required.

**3. Exploratory Analysis**
Descriptive statistics and distribution diagnostics across numeric, binary, and categorical variables.

**4. Correlation Visualization**
Heatmap and scatterplot matrix to identify visual patterns before applying statistical methods.

**5. Statistical Correlation Testing**

| Method | Applied To |
|---|---|
| Pearson | Linear relationships between continuous variables |
| Spearman | Monotonic relationships with non-normal distributions or outliers |
| Point-Biserial | Binary vs. continuous variable pairs |
| CramÃ©r's V | Categorical variable pairs |

**6. Business Interpretation**
Five structured findings with visual evidence, numerical evidence, interpretation, and business implication.

**7. Limitations & Next Steps**
Explicit acknowledgment of correlation vs. causation, large-sample p-value inflation, and Simpson's Paradox risk.

---

## Key Findings

### Finding 1 â€” Monthly Purchases: Dominant Revenue Driver
`compras_mes` is the only variable with a **strong** association with `ingreso_anual` (Pearson r = **0.967**, p < 0.0001). Purchase frequency explains approximately 93.5% of the joint variation with annual revenue.

> **Business implication:** Strategies targeting purchase frequency are the highest-leverage behavioral lever for revenue growth.

### Finding 2 â€” Ad Spend and Visit Frequency: Moderate Signal
Targeted advertising spend shows a **moderate** monotonic association with monthly visits (Spearman Ï = **0.559**, p < 0.0001). High individual-level variability limits its predictive strength.

> **Business implication:** Advertising investment is positively linked to traffic, but returns vary significantly by customer segment.

### Finding 3 â€” Premium Membership: No Meaningful Behavioral Differentiator
`miembro_premium` shows no practically relevant linear association with any continuous variable. All Point-Biserial coefficients fall below |r| = 0.10.

> **Business implication:** Premium status alone does not distinguish customers by behavior or revenue contribution in this dataset.

### Finding 4 â€” Churn: No Linear Characterization via Available Variables
`abandono` shows negligible linear association with all continuous variables. The sole statistically significant pair (`abandono` vs `satisfaccion`, r = âˆ’0.024) has a negligible effect size.

> **Business implication:** Linear correlation is insufficient to profile churned customers. Non-linear or clustering approaches are recommended.

### Finding 5 â€” Premium Membership vs. Churn: Weak but Detectable Signal
`miembro_premium` vs `abandono` is the only categorical pair with a meaningful CramÃ©r's V (V = **0.120**, p < 0.0001). Low magnitude; not a robust churn predictor.

> **Business implication:** Merits further investigation â€” specifically a cross-tabulation of premium churn rates disaggregated by satisfaction level.

---

## Correlation Summary Table

| Variable Pair | Method | Coefficient | Magnitude |
|---|---|---|---|
| `compras_mes` vs `ingreso_anual` | Pearson | r = 0.967 | Very Strong |
| `gasto_publicidad_dirigida` vs `visitas_mes` | Spearman | Ï = 0.559 | Strong |
| `compras_mes` vs `visitas_mes` | Pearson | r = 0.350 | Moderate |
| `ingreso_anual` vs `visitas_mes` | Pearson | r = 0.340 | Moderate |
| `ingreso_anual` vs `gasto_publicidad_dirigida` | Pearson | r = 0.200 | Weak |
| `miembro_premium` vs `abandono` | CramÃ©r's V | V = 0.120 | Low |
| All other binary/categorical pairs | Point-Biserial / CramÃ©r's V | < 0.10 | Negligible |

---

## Limitations

- **Correlation â‰  Causation.** No finding in this analysis supports a causal interpretation.
- **Large sample effect.** n = 15,000 produces significant p-values even for negligible effect sizes. Statistical significance and practical relevance are evaluated independently throughout.
- **Simpson's Paradox risk.** Global correlations have not been verified within subgroups (`region`, `tipo_dispositivo`, `miembro_premium`).
- **Variables not included.** Seasonality, promotional campaigns, and macroeconomic context are outside the scope of the available data.

---

## Next Steps

**Step 1 â€” Simpson's Paradox verification**
Disaggregate primary correlations by `region`, `tipo_dispositivo`, and `miembro_premium`. Prioritize the `compras_mes` vs `ingreso_anual` pair.

**Step 2 â€” Customer segmentation**
Apply K-Means or hierarchical clustering to behavioral variables to identify differentiated customer profiles. Evaluate whether global correlation patterns hold within segments.

**Step 3 â€” Predictive modeling**
Develop a regression model using `ingreso_anual` as the dependent variable, with `compras_mes`, `visitas_mes`, and `gasto_publicidad_dirigida` as predictors. Evaluate multicollinearity before including correlated features simultaneously.

---

## Project Structure

```
novaretail-customer-behavior-eda/
â”‚
â”œâ”€â”€ novaretail_customer_behavior_eda.ipynb   # Main analysis notebook
â”œâ”€â”€ README.md                                 # Project documentation
â””â”€â”€ data/
    â””â”€â”€ novaretail_comportamiento_clientes_2024.csv
```

---

## How to Run

```bash
# Clone the repository
git clone https://github.com/your-username/novaretail-customer-behavior-eda.git
cd novaretail-customer-behavior-eda

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy

# Launch notebook
jupyter notebook novaretail_customer_behavior_eda.ipynb
```

---

## Skills Demonstrated

**Technical**
`Python` Â· `Pandas` Â· `NumPy` Â· `Seaborn` Â· `Matplotlib` Â· `SciPy`
`Exploratory Data Analysis` Â· `Correlation Analysis` Â· `Statistical Testing`
`Data Cleaning` Â· `Data Visualization` Â· `Analytical Documentation`

**Analytical**
`Statistical Thinking` Â· `Effect Size vs. P-value Interpretation` Â· `Business Insight Communication`
`Structured Problem Solving` Â· `Findings Reporting` Â· `Analytical Limitation Awareness`

---

*Analysis conducted for the Growth & Retention team, NovaRetail+ Â· 2024*
