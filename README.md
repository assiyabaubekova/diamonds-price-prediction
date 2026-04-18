# Diamonds for Sara: Price Prediction & Deal Finder
> A machine learning pipeline that predicts fair diamond prices and surfaces underpriced stones using Random Forest Regression.

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-RandomForest-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![MAPE](https://img.shields.io/badge/MAPE-5.54%25-2ea44f?style=flat)
![Dataset](https://img.shields.io/badge/Dataset-6%2C000%20diamonds-blueviolet?style=flat)

---

## Overview

The goal: given a dataset of 6,000 certified diamonds, train a model to predict each stone's fair market price, then flag diamonds where the **actual listing price is below the prediction** i.e. genuine deals.

The model is then filtered by a buyer's specific quality criteria (cut, color, clarity, carat weight) to produce a ranked shortlist of the best purchases.

## Results at a Glance

| Metric | Value |
|--------|-------|
| MAE | $673.72 |
| MAPE | **5.54%** |
| Algorithm | Random Forest Regressor (100 trees) |
| Train/Test split | 80% / 20% |


## Feature Importance

Carat Weight dominates price prediction with ~77% importance — consistent with how the real diamond market works. Clarity and Color each contribute 11%. Cut, Polish, Symmetry, and Report have minimal individual predictive power.

<img src="images/feature_importance.png" alt="Feature importance bar chart" width="550"/>

## Exploratory Analysis
### Price Distribution
Diamond prices follow a strong right-skewed distribution, with most stones priced between 2,000–15,000 USD and a long tail extending to 100,000 USD.

<img src="images/price_distribution.png" alt="Diamond price distribution histogram" width="700"/>

### Price vs. Carat Weight — Good Deals Highlighted
Orange dots = diamonds where the actual price is **below** the model's predicted fair value. Underpriced stones exist across all weight ranges.

<img src="images/price_vs_carat.png" alt="Scatter plot of price vs carat weight with good deals highlighted" width="580"/>

## Top 5 Recommendations

Filtered by quality criteria: **Cut** = Ideal or Very Good · **Color** = G or H · **Clarity** = VS1 or VS2 · **Carat** = 0.9–1.5
All five top picks are 1.5-carat diamonds priced **595–1,013 USD below** their predicted fair value.

<img src="images/top5_results.png" alt="Table of top 5 recommended diamonds" width="650"/>

## Pipeline

```
data.xlsx
    │
    ▼
OrdinalEncoder
    │
    ▼
Train/Test Split (80/20)
    │
    ▼
RandomForestRegressor
    │
    ├─ Evaluate: MAE, MAPE, R², RMSE
    ├─ Feature importance
    │
    ▼
Predict on test set
    │
    ▼
Flag Good Deals
    │
    ▼
Filter by buyer criteria
    │
    ▼
Top 5 Recommendations
```

---

## Dataset Features

| Feature | Type | Description |
|---------|------|-------------|
| Carat Weight | Numeric | Physical weight of the stone |
| Cut | Ordinal | Fair - Good - Very Good - Ideal |
| Color | Ordinal | J (least colorless) - D (most colorless) |
| Clarity | Ordinal | I2 - FL (fewest inclusions) |
| Polish | Ordinal | Surface finish quality |
| Symmetry | Ordinal | Facet alignment quality |
| Report | Nominal | Certifying lab (GIA, AGSL, etc.) |
| Price | Numeric | Target variable (USD) |


## Files

```
├── Diamond_model_fixed.ipynb   # Full ML pipeline (fixed)
├── data.xlsx                    # Source dataset (6,000 diamonds)
├── images/                      # Visualizations used in this README
│   ├── feature_importance.png
│   ├── model_code.png
│   ├── price_distribution.png
│   ├── price_vs_carat.png
│   └── top5_results.png
└── README.md
```

---

## Stack

- **Python 3.12**
- **scikit-learn** - RandomForestRegressor, OrdinalEncoder, train_test_split
- **pandas / numpy** - data manipulation
- **matplotlib / seaborn** - visualizations

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/diamonds-price-prediction.git
cd diamonds-price-prediction

# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl jupyter

# Launch notebook
jupyter notebook Diamonds_model_fixed.ipynb
```

---

*Project built as part of a data science portfolio*
