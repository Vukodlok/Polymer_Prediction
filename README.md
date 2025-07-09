# Polymer Property Prediction - NeurIPS 2025 Challenge

This repository contains my submission for the [NeurIPS 2025 Open Catalyst Polymer Property Prediction Challenge](https://www.kaggle.com/competitions/neurips-open-polymer-prediction-2025/), focused on predicting five key polymer properties from SMILES strings and computed molecular descriptors.

## Project Overview

The goal of this challenge was to build machine learning models that accurately predict the following polymer properties:

- Free Volume Fraction (`FFV`)
- Glass Transition Temperature (`Tg`)
- Crystallization Temperature (`Tc`)
- Density
- Radius of Gyration (`Rg`)

Given the molecular structure of polymers in the form of SMILES strings, the task was to extract meaningful features and train models to predict the five continuous target variables.

## Approach

The project follows a structured modeling pipeline:

1. **Data Cleaning & Preprocessing**
   - Imputation of missing and infinite values
   - Feature alignment between training and test sets
   - Standard scaling

2. **Feature Engineering**
   - Computation of traditional molecular descriptors
   - Generation of SMILES-based features (e.g. RDKit-based statistics)

3. **Model Training**
   - Trained individual models for each target using:
     - Random Forest
     - XGBoost
     - CatBoost
     - MultiOutputRegressor with RandomForest

4. **Ensembling**
   - Weighted average ensemble of model predictions
   - Explored various weight combinations to minimize validation RMSE

## Key Results

| Version | Description           | Public Score |
|---------|------------------------|--------------|
| 22      | Final tuned ensemble   | 0.072        |
| 21      | Optimal blend (XGB + CB)| 0.066        |
| 17      | Equal-weight ensemble  | 0.078        |
| 16      | Multi-target model     | 0.130        |
| 15      | External baseline      | 0.064        |

The best-performing submissions resulted from carefully tuned ensembling of XGBoost and CatBoost models with SMILES-derived features gained using external data.

## Reflections

### What Worked Well

- Model ensembling using optimized weights significantly improved prediction accuracy.
- Incorporating SMILES-derived features alongside traditional descriptors enhanced model performance.
- Careful preprocessing and feature alignment ensured stability and generalization.

### What Could Be Improved

- Multi-output regression did not generalize well across targets.
- Manual weight tuning was limited; automated ensemble optimization would be more efficient.

### Future Work

- Implement automated ensemble weight optimization using cross-validated RMSE as an objective.
- Explore per-target ensemble weighting strategies.
- Incorporate graph neural networks (GNNs) for more in-depth polymer representation.
- Use uncertainty estimation techniques to quantify model confidence.
