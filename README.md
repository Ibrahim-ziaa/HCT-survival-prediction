# HCT survival prediction: data preparation

Work in progress on the CIBMTR "Equity in post-HCT Survival Predictions" Kaggle competition: predicting outcomes for patients receiving a hematopoietic cell transplant.

## What is in this repository today

`notebooks/model.ipynb` contains the data preparation stage only:

- Drops identifier and leakage prone columns (`ID`, `efs_time`, and sparse match and cytogenetic detail columns).
- One hot encodes eight categorical clinical fields (for example conditioning intensity, graft type, primary disease, donor relation).
- Label encodes sixteen HLA match fields.
- Imputes and standardises four numeric fields (patient age, donor age, comorbidity score, Karnofsky score).
- Holds out 500 rows as an unseen check set before fitting the pipeline.
- Wraps all of it in a reusable scikit-learn `ColumnTransformer` pipeline.

The output is a fully numeric table of 28,300 rows and 94 columns, ready for modelling.

## What is not here yet

No model has been trained in this repository, so there are no scores to report. Planned next steps: gradient boosted models (LightGBM, XGBoost, CatBoost) with stratified cross validation, scored with the competition's stratified concordance index, plus SHAP feature importance.

## Data

The competition data is not included, because the competition rules do not allow redistributing it. Download `train.csv`, `test.csv` and `data_dictionary.csv` from the [competition page](https://www.kaggle.com/competitions/equity-post-HCT-survival-predictions/data) and place them in `data/`.

## Stack

Python, pandas, scikit-learn.

## License

GPL-3.0
