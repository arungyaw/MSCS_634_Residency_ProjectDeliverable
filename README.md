# MSCS 634 Advanced Data Mining Project

### Group Members :

Arun Gyawali

Kashif Ali Syed

Jiwon Jung

Hanuman Sai Chanukya Srinivas Chilamkuri

## Project Overview

This project applies data mining techniques to the **Online Shoppers Purchasing Intention Dataset**. The goal is to clean and explore the data, develop predictive models, identify customer groups, discover behavioral patterns, and provide practical recommendations.

The same dataset will be used throughout all project deliverables.

## Dataset

**Dataset:** Online Shoppers Purchasing Intention Dataset  
**Source:** UCI Machine Learning Repository  
**Original Records:** 12,330  
**Original Attributes:** 18  
**Cleaned Records:** 12,205  
**Main Target Variable:** Revenue

Each record represents an online shopping session. The dataset includes page visits, page durations, bounce rates, exit rates, page values, visitor type, month, weekend status, traffic information, and purchasing outcome.

## Project Deliverables

### Deliverable 1: Data Collection, Cleaning, and Exploration

- Selected and described the dataset
- Inspected the dataset structure
- Checked for missing and invalid values
- Removed duplicate records
- Addressed extreme duration values
- Performed exploratory data analysis
- Identified important customer behavior patterns

**Status:** Completed

### Deliverable 2: Regression Modeling and Performance Evaluation

- Engineered five behavioral features
- Encoded categorical variables and removed redundant predictors
- Built Linear Regression, Ridge Regression, Lasso Regression, and Random Forest models
- Evaluated the models using R-squared, MSE, and RMSE
- Applied five-fold cross-validation using preprocessing pipelines
- Compared model performance and feature importance

**Status:** Completed

### Deliverable 3

- The tuned Random Forest was the best classifier.
- It achieved an accuracy of **0.8759**, an F1 score of **0.6759**, and a ROC-AUC of **0.9340**.
- It correctly identified 316 purchasing sessions and missed 66.
- PageValues and Engagement_Score were the two most influential classification features.
- K-Means selected three clusters with a silhouette score of **0.4885**.
- The clusters represented typical browsing, quick-exit, and highly engaged sessions.
- Highly engaged sessions had a purchase rate of **27.8%**, while quick-exit sessions had a purchase rate of only **0.7%**.
- Apriori identified **161 frequent itemsets**.
- The strongest purchase rule combined positive PageValues with low bounce and low exit behavior and achieved a lift of **4.35**.

**Status:** Completed

### Deliverable 4: Final Insights and Recommendations

- Combine findings from all deliverables
- Summarize preprocessing and modeling results
- Provide practical recommendations
- Discuss data privacy, fairness, and possible bias
- Prepare the final report and presentation

**Status:** Not started

## Current Key Findings

**Deliverable 1**

- The cleaned dataset contains 12,205 unique sessions.
- Only 15.63% of sessions resulted in a purchase, showing that Revenue is imbalanced.
- PageValues had the strongest positive relationship with Revenue.
- Purchasing sessions had greater product engagement and lower bounce and exit rates.
- November had the highest monthly conversion rate.
- Weekend sessions had a slightly higher conversion rate than weekday sessions.

**Deliverable 2**

- ProductRelated_Duration was selected as the regression target because PageValues was highly zero-inflated.
- Five engineered behavioral features were created, and the final models used 68 predictor features.
- Random Forest was the best-performing model.
- Random Forest achieved a test R-squared of 0.7506 and a test RMSE of 784.02 seconds.
- Its mean five-fold cross-validation R-squared was 0.7702, with an RMSE of 742.97 seconds.
- Total_Pages and ProductRelated page count were the two most influential predictors.
- The stronger Random Forest performance suggests that the relationship between browsing behavior and product-related duration is partly non-linear.

### Deliverable 3: Classification, Clustering, and Pattern Mining

- Logistic Regression and Random Forest classification models were developed to predict Revenue.
- The Random Forest was tuned using GridSearchCV with stratified cross-validation and F1 score as the optimization metric.
- The tuned Random Forest was the best classifier, with an accuracy of **0.8759**, an F1 score of **0.6759**, and a ROC-AUC of **0.9340**.
- It correctly identified **316 purchasing sessions** and missed **66 purchasing sessions**.
- PageValues and Engagement_Score were the two most influential classification features.
- K-Means clustering selected a three-cluster solution with a silhouette score of **0.4885**.
- The clusters represented typical browsing sessions, quick-exit sessions, and highly engaged sessions.
- Highly engaged sessions had a purchase rate of approximately **27.8%**, while quick-exit sessions had a purchase rate of only **0.7%**.
- Apriori association rule mining identified **161 frequent itemsets**.
- The strongest purchase rule combined positive PageValues with low bounce and low exit behavior.
- This rule had **68.00% confidence** and a lift of approximately **4.35**.
- The classification, clustering, and association results describe behavioral patterns and should be used as decision-support information rather than proof of causation.

## Repository Structure

````text
MSCS_634_Project/
│
├── MSCS_634_ProjectDeliverable_1/
│   ├── Deliverable_1.ipynb
│   ├── online_shoppers_intention.csv
│   ├── online_shoppers_cleaned.csv
│   └── Deliverable1_README.md
│
├── MSCS_634_ProjectDeliverable_2/
│   ├── Deliverable_2.ipynb
│   ├── online_shoppers_cleaned.csv
│   └── Deliverable2_README.md
│   └── .gitignore
│
├── MSCS_634_ProjectDeliverable_3/
│   ├── Deliverable_2.ipynb
│   ├── online_shoppers_cleaned.csv
│   └── Deliverable2_README.md
|
├── MSCS_634_ProjectDeliverable_4/
└── README.md

## Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipykernel
````

Additional libraries may be added in later deliverables.

## How to Run

1. Clone or download the repository.
2. Open the folder for the required deliverable.
3. Open the Jupyter Notebook in Jupyter Notebook or Visual Studio Code.
4. Install the required libraries.
5. Run the notebook cells from top to bottom.

## Future Updates

This README will be updated after Deliverables 4 to include final recommendations, ethical considerations, and presentation materials.

## Reference

Sakar, C., & Kastro, Y. (2018). _Online Shoppers Purchasing Intention Dataset_ [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q
