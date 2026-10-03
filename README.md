# NovaRetail+ Customer Behavior: Correlation Analysis of Annual Revenue
Correlation analysis of 15,000 NovaRetail+ customers with Python: Pearson, Spearman, point-biserial and Cramér's V to explore which behavior factors are associated with annual revenue.

## Objective
Answer the question from the Growth & Retention team: **which customer behavior factors are most strongly associated with the annual revenue generated?** This is an exploratory, correlational analysis: correlation does not imply causation.

## Dataset
15,000 customers and 12 columns (2024), with no missing values.

| Type | Columns |
|---|---|
| Numeric | `edad`, `nivel_ingreso`, `visitas_mes`, `compras_mes`, `gasto_publicidad_dirigida`, `satisfaccion`, `ingreso_anual` |
| Binary | `miembro_premium`, `abandono` |
| Categorical | `id_cliente`, `tipo_dispositivo`, `region` |

Baseline: 13.9% premium members, 15.1% churn, 65.5% of customers on mobile, and about 25% of customers with no purchases and zero annual revenue.

## Tools
Python · Pandas · NumPy · Seaborn · Matplotlib · SciPy · Jupyter Notebook

## Process
1. Loaded and explored the dataset (types, ranges, distributions).
2. Converted `edad` from float to integer and documented the analysis assumptions.
3. Visualized relationships with a Pearson correlation heatmap and scatterplots with trend lines for the key pairs.
4. Quantified them with the right coefficient for each variable type:
   - **Pearson / Spearman** for numeric pairs
   - **Point-biserial** for numeric vs. binary variables
   - **Cramér's V** for categorical and binary pairs
5. Interpreted each finding without causal language, stating what cannot be claimed and the business implication.

## Results
| Pair | Method | Result |
|---|---|---|
| `compras_mes` - `ingreso_anual` | Pearson / Spearman | 0.97 / 0.97 |
| `visitas_mes` - `gasto_publicidad_dirigida` | Pearson / Spearman | 0.58 / 0.56 |
| `visitas_mes` - `compras_mes` | Pearson / Spearman | 0.35 / 0.33 |
| `visitas_mes` - `ingreso_anual` | Pearson / Spearman | 0.34 / 0.32 |
| `gasto_publicidad_dirigida` - `compras_mes` | Pearson | 0.21 |
| `miembro_premium` - `ingreso_anual` | Point-biserial | 0.09 |
| `abandono` - `ingreso_anual` | Point-biserial | -0.00 (p = 0.73) |
| `edad`, `nivel_ingreso`, `satisfaccion` - other variables | Pearson | about 0 |
| Categorical pairs (device, region, premium, churn) | Cramér's V | 0.007 to 0.020, except premium vs. churn (0.12) |

## Key Findings
1. **Monthly purchases and annual revenue are almost perfectly associated** (r = 0.97). `ingreso_anual` was probably built from `compras_mes`, so this is collinearity rather than an independent business finding.
2. **Targeted ad spend is associated more with visits (0.58) than with purchases (0.21).** Ad budget may have been assigned to customers who already visited more, so this does not show that ads drive traffic.
3. **Visits show a modest association** with purchases (0.35) and with annual revenue (0.34).
4. **Age, income level, satisfaction, device type and region show no relevant association** with annual revenue. Average revenue is similar across devices and regions.
5. **Premium membership has a very weak association with revenue** (0.09), and churn shows none (-0.00).

## Limitations
- Correlation does not imply causation.
- The formula behind `ingreso_anual` is unknown, which limits how the variable can be used in predictive models.
- Data covers a single period (2024) with no date column, so trends and seasonality cannot be analyzed.
- Relationships were measured on the full dataset, without segmenting by region, device or ad spend level.

## Next Steps
- Ask the data team how `ingreso_anual` is calculated to confirm or rule out the collinearity with `compras_mes`.
- Check whether the visits-to-purchases relationship changes by region, device type or ad spend level.
- Obtain monthly or quarterly data to confirm that the relationships are stable over time.

## How to Run
1. Open the notebook in Google Colab or Jupyter.
2. Install the requirements: `pandas`, `numpy`, `seaborn`, `matplotlib`, `scipy`.
3. Place `novaretail_comportamiento_clientes_2024.csv` in a `/datasets/` folder (or change the path in the loading cell).
4. Run all cells in order.

## Files
- `sprint_8_-_cuaderno_de_jupiter_-_S8_Student_Version-Project-NovaRetail.ipynb`: full analysis notebook (exploration, correlation analysis and business interpretation).
- `images/`: screenshots of the charts.
  
- [Download the Power BI dashboard (.pbix) from Google Drive](https://drive.google.com/file/d/1EFNhJx2Qx-u7Y7nCvOB0xOWwHfq0iiz7/view?usp=sharing)

- [Download the notebook from Google Drive](https://drive.google.com/file/d/1YhZGXb_6jyP1V5Pu4U0b8H-kHsfpyvx4/view?usp=sharing)
