# Laptop Price Analysis

Exploratory Data Analysis (EDA) and feature extraction on a laptop pricing dataset to understand key price drivers.

## Overview

This project analyzes 1,274 laptop records (after deduplication) to identify which hardware specifications and brand factors most influence laptop prices. The analysis includes data cleaning, feature engineering from messy text columns, and exploratory visualizations.

## Dataset

- **Source**: Kaggle "Laptop Price" dataset
- **Original size**: 1,303 rows × 12 columns
- **Cleaned size**: 1,274 rows × 11 columns (29 duplicates removed)
- **Target variable**: Price (in INR - Indian Rupees)

## Features Extracted

| Original Column | Parsed Features |
|----------------|-----------------|
| `RAM` | `RAM_gb` (numeric: 2, 4, 6, 8, 12, 16, 24, 32, 64) |
| `Weight` | `Weight_kg` (numeric: 0.69–4.7) |
| `CPU` | `CPU_brand` (Intel / AMD / Samsung) |
| `GPU` | `GPU_brand` (Intel / Nvidia / AMD / ARM), `GPU_model` |
| `Company` | Categorical (Apple, Dell, HP, Lenovo, Asus, Acer, etc.) |
| `Type_Name` | Categorical (Workstation, Gaming, Ultrabook, 2 in 1 Convertible, Notebook, Netbook) |
| `Inches` | Numeric (10.1–18.4) |

*Columns not parsed in this analysis: `Screen_Resolution`, `Memory` (storage), `Operating_System` — kept as raw strings.*

## Key Findings

Based on the deduplicated dataset (1,274 rows):

1. **Laptop Type drives price**: Workstations (~₹121K) > Gaming (~₹92K) > Ultrabooks (~₹83K) > 2-in-1 Convertibles (~₹69K) > Notebooks (~₹42K) > Netbooks (~₹36K)
2. **Weight positively correlates with price** (r = +0.21): heavier laptops tend to be more expensive, as they often house dedicated GPUs, larger batteries, and better cooling for gaming/workstation performance
3. **Intel CPUs average higher prices** than AMD (Intel ~₹62K vs AMD ~₹30K); Samsung appears once at ~₹35K
4. **Nvidia GPUs carry a significant premium** over integrated options (Nvidia ~₹80K vs Intel ~₹54K, AMD ~₹41K, ARM ~₹35K)
5. **Screen size has only a weak correlation with price** (r ≈ 0.07) — not a strong driver alone
6. **RAM is strongly correlated with price** (r ≈ 0.74): higher RAM drives price up, though the jumps are non-linear (larger ~₹30K–₹64K steps at 16GB+).

## Project Structure

```
laptop-price-case-study/
├── code/
│   └── eda.ipynb          # Main analysis notebook
├── dataset/
│   └── laptop_data (1).csv # Raw dataset
└── README.md
```

## Requirements

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

## How to Run

```bash
# Activate virtual environment (optional)
source .venv/bin/activate

# Launch notebook
jupyter notebook code/eda.ipynb
```

## Notebook Sections

1. **Import & Load** — Libraries and data loading
2. **Data Structure** — Shape, columns, dtypes, descriptive stats
3. **Data Preparation** — Drop unused columns, rename, remove duplicates
4. **Feature Engineering** — Parse RAM, Weight, CPU brand, GPU brand/model
5. **EDA** — Correlation heatmap, categorical boxplots, RAM/Weight/Inches vs Price, price distribution, and IQR-based outlier analysis (28 outliers)

## Next Steps (Optional)

- Parse remaining columns: `Screen_Resolution` (resolution, PPI, touchscreen), `Memory` (SSD/HDD, capacity), `Operating_System` (normalized)
- Build baseline ML models (Linear Regression, Random Forest, XGBoost)
- Feature importance analysis for model-driven feature selection
- Hyperparameter tuning and cross-validation

## License

This project uses the **Kaggle Laptop Price dataset (CC0 - Public Domain)**.

The analysis code and documentation in this repository are also released under **CC0** - you may freely use, modify, and distribute without attribution.