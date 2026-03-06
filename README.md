# HCT Survival Prediction — Tabular ML for Clinical Decision Support

> Predicting post-transplant survival outcomes for Hematopoietic Cell Transplantation patients using ensemble ML

---

## Overview

A machine learning system for predicting survival outcomes in patients undergoing **Hematopoietic Cell Transplantation (HCT)** — a high-stakes medical procedure where early outcome prediction directly impacts clinical management. Built on the CIBMTR dataset from the Kaggle Equity in Healthcare AI competition.

---

## Technical Approach

### Feature Engineering

```
Raw Clinical Data
├── Continuous: age, lab values, days-to-transplant
├── Categorical: disease type, donor match, conditioning regimen
├── Ordinal: comorbidity scores, disease risk index
└── Derived: interaction terms (age × disease risk), missingness indicators
```

Key decisions:
- **Missing values**: Missingness indicators + median imputation (missingness is clinically informative)
- **Encoding**: Target encoding for high-cardinality categoricals
- **Scaling**: RobustScaler to handle outliers in lab values

### Models

| Model | CV c-statistic | Notes |
|---|---|---|
| LightGBM | **0.692** | Best single model |
| XGBoost | 0.681 | Strong on dense features |
| CatBoost | 0.678 | Handles categoricals natively |
| Random Forest | 0.661 | Baseline |
| Balanced RF | 0.659 | Better minority class recall |

Final predictions: stacked ensemble (LightGBM + XGBoost → logistic meta-learner).

---

## Results

- Best CV c-statistic: **0.692**
- Outperforms HCT-CI clinical scoring baseline (~0.61 in literature)

---

## Technical Stack

- **ML**: LightGBM, XGBoost, CatBoost, scikit-learn
- **Evaluation**: Stratified k-fold, calibration curves, subgroup analysis
- **Platform**: Kaggle notebooks

---

## Repo Structure

```
HCT-survival-prediction/
├── data/processed/
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_feature_eng.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_ensemble.ipynb
└── README.md
```

---

## License

GPL-3.0
