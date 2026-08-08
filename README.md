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
| `RAM` | `RAM_gb` (numeric: 2, 4, 6, 8, 16, 32) |
| `Weight` | `Weight_kg` (numeric: 0.92–2.6) |
| `CPU` | `CPU_brand` (Intel / AMD) |
| `GPU` | `GPU_brand` (Intel / Nvidia / AMD), `GPU_model` |
| `Company` | Categorical (Apple, Dell, HP, Lenovo, Asus, Acer, etc.) |
| `Type_Name` | Categorical (Ultrabook, Notebook, 2 in 1 Convertible, Netbook) |
| `Inches` | Numeric (10.1–18.4) |

*Columns not parsed in this analysis: `Screen_Resolution`, `Memory` (storage), `Operating_System` — kept as raw strings.*

## Key Findings

1. **Laptop Type drives price**: 2-in-1 Convertibles (~₹75K) > Ultrabooks (~₹68K) > Notebooks (~₹42K) > Netbooks (~₹25K)
2. **Weight negatively correlates with price** (r = -0.45): lighter laptops command premium prices
3. **Intel CPUs average higher prices** than AMD (Intel ~₹65K vs AMD ~₹35K)
4. **Nvidia GPUs carry significant premium** over Intel/AMD integrated graphics
5. **Screen size weakly correlates with price** (r = 0.18) — not a strong driver alone
6. **RAM has strong price relationship**: each additional 8GB adds ~₹15K–₹20K on average

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
5. **EDA** — Correlation heatmap, categorical boxplots, RAM/Weight/Inches vs Price

## Next Steps (Optional)

- Parse remaining columns: `Screen_Resolution` (resolution, PPI, touchscreen), `Memory` (SSD/HDD, capacity), `Operating_System` (normalized)
- Build baseline ML models (Linear Regression, Random Forest, XGBoost)
- Feature importance analysis for model-driven feature selection
- Hyperparameter tuning and cross-validation

## License

MIT License — feel free to use and modify.