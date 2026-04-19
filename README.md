# QVI Retail Chips Analysis

A two-part end-to-end data analysis project on the **Quantium Virtual Internship (QVI)** dataset, covering customer purchasing behaviour for chips and a controlled trial store performance evaluation.

---

## 📁 Project Structure

```
├── potato-chips-analysis.ipynb   # Part 1 — Customer & Product Analysis
├── Trail_Stores.ipynb            # Part 2 — Trial Store Experimentation
└── README.md
```

---

# Part 1 — Potato Chips Analysis (`potato-chips-analysis.ipynb`)

# Overview
Exploratory data analysis on chip sales across all stores, identifying the highest-revenue pack sizes, top-performing brands, key customer demographics, and best-performing store locations.

### Dataset
| File | Source | Description |
|------|--------|-------------|
| `QVI_transaction_data.xlsx` | Kaggle | Transaction-level sales records (Jul 2018 – Jun 2019) |
| `QVI_purchase_behaviour.csv` | Kaggle | Customer loyalty card segmentation by lifestage & tier |

### Key Steps
- **Data Loading & Cleaning** — Fixed Excel serial date format, merged transaction and behaviour datasets
- **Pack Size Analysis** — Segmented products into small (≤110g), medium (170–175g), and large (330g+) to compare revenue share
- **Brand Analysis** — Identified top-selling brands by volume and revenue
- **Customer Segmentation** — Used DuckDB SQL queries + a heatmap to find which lifestage & premium tier buys the most chips
- **Store Performance** — Ranked stores by chips revenue, transactions, and packets sold

# Key Findings
1. **Medium pack sizes (170–175g) account for over 67% of total chips revenue**, with large packs (330g+) contributing only 7.1% despite their higher unit price.

2. **Families and older customer segments are the biggest chip buyers** across both mainstream and budget tiers.

3. **Store #226 leads all stores** in chips revenue, transactions, and volume sold.

# Libraries Used

pandas | numpy | matplotlib | seaborn | duckdb | matplotlib-venn | re

# Part 2 — Trial Store Analysis (`Trail_Stores.ipynb`)

# Overview
Evaluated the effectiveness of an in-store intervention (trial) run across three pilot stores by comparing their sales performance against carefully selected control stores during the trial period (Feb–Apr 2019).

# Dataset
| File | Description |
|------|-------------|
| `QVI_data.csv` | Combined and pre-processed transaction + customer data |

# Methodology

**Step 1 — Data Cleaning**
- Removed null values and duplicate records
- Filtered out bulk/non-retail purchases (qty ≥ 100)
- Removed sales outliers using IQR (1.5× rule)
- Final clean dataset: **264,258 rows**

**Step 2 — Pre-Trial Baseline (Jul 2018 – Jan 2019)**
| Trial Store | Pre-Trial Sales |
|-------------|----------------|
| Store 77    | $1,693.60       |
| Store 86    | $6,091.45       |
| Store 88    | $9,293.60       |

**Step 3 — Control Store Matching**
Each trial store was paired with its closest control store by minimising the absolute difference in pre-trial sales.

| Trial Store | Control Store | Sales Difference |
|-------------|---------------|-----------------|
| 77          | 187           | $9.40            |
| 86          | 196           | $3.45            |
| 88          | 237           | $37.20           |

**Step 4 Scaling Factor**
A scaling factor was computed (trial ÷ control pre-trial sales) to normalise the control store's expected performance during the trial period.

**Step 5 — Trial Period Sales Comparison (Feb–Apr 2019)**

| Trial Store | Scaled Control (Expected) | Actual Trial Sales | Improvement |
|-------------|--------------------------|-------------------|-------------|
| 77          | $738.00                   | $777.00            | **+5.29%**  |
| 86          | $2,617.92                 | $2,788.20          | **+6.50%**  |
| 88          | $3,832.94                 | $4,286.80          | **+11.84%** |

#Key Finding
1 **All three trial stores outperformed their matched control stores**, with Store 88 showing the strongest uplift at nearly 12% — suggesting the trial intervention had a consistently positive effect on sales.

# Libraries Used

pandas | numpy | duckdb

# Setup & Usage

# Prerequisites
```bash
pip install pandas numpy duckdb matplotlib seaborn matplotlib-venn openpyxl
```

# Running the Notebooks

**Part 1** was originally run on Kaggle. To run locally:
1. Download `QVI_transaction_data.xlsx` and `QVI_purchase_behaviour.csv` from the [Kaggle dataset](https://www.kaggle.com/)
2. Update the file paths in the notebook to your local paths
3. Run all cells in order

**Part 2** runs locally with Jupyter:
1. Download `QVI_data.csv`
2. Update the CSV path in Cell 2
3. Run all cells in order

---

# Dataset Source

Both notebooks use the **Quantium Virtual Internship** dataset, publicly available on Kaggle. The data covers chip product transactions from a major Australian retailer across the financial year 2018–2019.

---

# Author

Uday Bisht  
B.Tech CSE Student | ADGIPS, GGSIPU Delhi  
Interested in Data Science, ML, and Retail Analytics
