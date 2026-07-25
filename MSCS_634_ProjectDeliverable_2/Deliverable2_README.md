# MSCS 634 Project Deliverable 2

## Regression Modeling and Performance Evaluation

### Group Members :

Arun Gyawali

Kashif Ali Syed

Jiwon Jung

Hanuman Sai Chanukya Srinivas Chilamkuri

### Project Overview

This deliverable builds on the cleaned **Online Shoppers Purchasing Intention Dataset** from Deliverable 1. New features were engineered from the existing behavioral columns, multiple regression models were trained to predict a continuous outcome, and their performance was evaluated and compared using R-squared, MSE, RMSE, and 5-fold cross-validation.

The cleaned dataset produced in Deliverable 1 (`online_shoppers_cleaned.csv`) was used directly as the input for this deliverable, so no additional cleaning was required.

## Dataset

**Dataset name:** Online Shoppers Purchasing Intention Dataset
**Source:** UCI Machine Learning Repository
**Input shape:** 12,205 rows and 18 columns (cleaned dataset from Deliverable 1)
**Regression target:** ProductRelated_Duration

## Selecting a Regression Target

`Revenue`, the dataset's primary target, is Boolean and is reserved for the classification task in Deliverable 3, so a continuous target was needed for this deliverable.

`PageValues` was the target originally proposed in the Deliverable 1 plan, but further inspection showed that it is **zero for about 77.6% of sessions**, making it too zero-inflated for standard regression models to fit well.

**ProductRelated_Duration** (total time spent on product-related pages in a session) was selected instead. Only about 5% of sessions have a value of zero, so it behaves as a genuine continuous variable, and it remains closely tied to customer engagement and purchasing intent — Deliverable 1 found this value was substantially higher for purchasing sessions (1,797.8s) than non-purchasing sessions (1,047.3s).

## Feature Engineering

New features were created to capture behavior patterns not directly present in the raw columns. None of the engineered features were built using `ProductRelated_Duration` itself, to avoid leaking the target into the predictors.

| Engineered Feature | Description |
|---|---|
| Total_Pages | Total pages visited across Administrative, Informational, and ProductRelated categories |
| NonProduct_Duration | Total time spent on Administrative and Informational pages |
| Avg_NonProduct_Duration_Per_Page | Average time spent per non-product page |
| BounceExitRatio | Ratio of BounceRates to ExitRates |
| Engagement_Score | ProductRelated page count multiplied by PageValues |

`Month` and `VisitorType` were one-hot encoded, and `Weekend` was converted to an integer. `Revenue` was excluded from the feature set entirely to keep this deliverable independent of the Deliverable 3 classification target.

## Modeling Approach

Data was split into training (80%) and test (20%) sets, and features were standardized with `StandardScaler` fit only on the training data. Four regression models were built and compared:

1. **Linear Regression** – baseline model with no regularization
2. **Ridge Regression** – L2-regularized linear model
3. **Lasso Regression** – L1-regularized linear model
4. **Random Forest Regressor** – non-linear ensemble model, included as a benchmark

Each model was evaluated on the held-out test set using R-squared, MSE, and RMSE, and then re-evaluated with 5-fold cross-validation on the training data to check generalization.

## Model Performance

### Test Set Results

| Model | R-squared | MSE | RMSE |
|---|---:|---:|---:|
| Linear Regression | 0.7188 | 693,011.65 | 832.47 |
| Ridge Regression | 0.7188 | 693,007.47 | 832.47 |
| Lasso Regression | 0.7188 | 693,002.75 | 832.47 |
| Random Forest | 0.7499 | 616,435.41 | 785.13 |

### 5-Fold Cross-Validation Results (Training Data)

| Model | CV R-squared (mean) | CV RMSE (mean) |
|---|---:|---:|
| Linear Regression | 0.7303 | 805.60 |
| Ridge Regression | 0.7303 | 805.59 |
| Lasso Regression | 0.7304 | 805.44 |
| Random Forest | 0.7694 | 744.15 |

Cross-validation results were close to the single train/test split results for every model, indicating the models generalize reasonably well and the initial split was not unusually easy or hard.

## Key Findings

- The three linear models (Linear Regression, Ridge, Lasso) performed almost identically, all reaching a cross-validated R-squared of roughly **0.73**. This similarity indicates multicollinearity was not severe enough for L1/L2 regularization to meaningfully change the linear fit.
- The **Random Forest Regressor** outperformed all linear models, reaching a cross-validated R-squared of roughly **0.77** and a lower RMSE of about **744 seconds**, suggesting the relationship between browsing behavior and product-page engagement time is at least partly non-linear.
- The most influential features for the Random Forest model were **Total_Pages** (0.559) and **ProductRelated** page count (0.312), together accounting for most of the model's predictive power. **ExitRates** (0.025) and the engineered **Avg_NonProduct_Duration_Per_Page** (0.014) contributed smaller but meaningful amounts.
- Feature engineering added value: the **Engagement_Score** and **BounceExitRatio** interaction features contributed to prediction beyond what the raw columns provided alone.

## Challenges Encountered

One challenge was choosing an appropriate regression target. `PageValues`, the dataset's most business-relevant continuous variable, turned out to be too zero-inflated for regression, so `ProductRelated_Duration` was used instead after checking its distribution.

Another challenge was avoiding target leakage. Several duration and page-count columns are closely related to `ProductRelated_Duration`, so engineered features such as `NonProduct_Duration` and `Avg_NonProduct_Duration_Per_Page` were deliberately built to exclude the target variable.

A minor technical challenge was that the default number of iterations for `Lasso` was insufficient on the scaled feature set, producing convergence warnings; increasing `max_iter` to 10,000 resolved this.

## Repository Files

- `Deliverable_2.ipynb` – Feature engineering, regression modeling, evaluation, and comparison
- `online_shoppers_cleaned.csv` – Cleaned dataset from Deliverable 1, used as input for this notebook
- `Deliverable2_README.md` – Project summary and findings for this deliverable

## How to Run

1. Place the notebook and `online_shoppers_cleaned.csv` in the same folder.
2. Open `Deliverable_2.ipynb` in Jupyter Notebook or Visual Studio Code.
3. Ensure the notebook's kernel points to the Python environment where the required libraries are installed.
4. Run the notebook cells from top to bottom.
5. Review the printed metrics, comparison table, and plots for each model.

## Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipykernel
```
