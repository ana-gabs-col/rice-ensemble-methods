# Rice Classification — Custom Ensemble & Boosting Methods

Developed together with Stephanny Frasser Sanchez.

Implementation from scratch of two ensemble algorithms (boosting with kNN as weak learner, and a custom "Perturbed Forest"), benchmarked against XGBoost, CART and Random Forest on the UCI Rice (Cammeo and Osmancik) dataset — 3,810 observations, 7 morphological features.

## Result

| Model | Accuracy | AUC |
|---|---|---|
| Boosting-kNN (from scratch) | 0.917 | 0.9746 |
| Random Forest | 0.930 | 0.9737 |
| XGBoost | 0.914 | 0.9666 |
| Perturbed Forest (from scratch) | 0.886 | 0.9523 |
| CART | 0.934 | 0.9294 |

## What's interesting here

Boosting-kNN replaces the usual weak learner (a small tree) with a k-NN smoother over cross-entropy pseudo-residuals — with only 2 hyperparameters instead of the usual 3, it matches a 500-tree Random Forest.

Perturbed Forest is an alternative to bagging: diversity across trees comes from perturbing each subsample (points shifted toward their nearest neighbors, labels smoothed by local mean) instead of bootstrap sampling.

## Verification note

This repository was independently rebuilt and verified. Two honest caveats: the original source code for Perturbed Forest was not available, only the algorithm description, so it was reconstructed from that description (AUC obtained is in the same range as originally reported, not identical). XGBoost was cross-checked with Python's xgboost library since R's package was unavailable in the verification environment; the code here is in R for consistency with the rest of the project.

## Methodology

1,000 random observations for training and 1,000 for test (fixed seed). Evaluated by accuracy and AUC-ROC on the test set.

## Stack

R, FNN (boosting-kNN), rpart (CART, base of Perturbed Forest), randomForest, pROC
