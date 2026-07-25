# MSCS 634 Project Deliverable 3

## Classification, Clustering, and Pattern Mining

### Group Members :

Arun Gyawali

Kashif Ali Syed

Jiwon Jung

Hanuman Sai Chanukya Srinivas Chilamkuri

### Project Overview

This deliverable continues the analysis of the **Online Shoppers Purchasing Intention Dataset** used in Deliverables 1 and 2. The cleaned dataset was used to classify purchasing sessions, identify customer-session groups, and discover behavioral association rules.

The five behavioral features created in Deliverable 2 were reused to maintain consistency across the project.

## Dataset

**Dataset name:** Online Shoppers Purchasing Intention Dataset  
**Source:** UCI Machine Learning Repository  
**Input shape:** 12,205 rows and 18 columns  
**Classification target:** Revenue  
**Purchase rate:** 15.63%

Revenue indicates whether an online shopping session resulted in a purchase. Because purchases represent the minority class, stratified splitting, balanced class weights, F1 score, confusion matrices, and ROC-AUC were used.

## Feature Preparation

The following engineered features from Deliverable 2 were recreated:

| Engineered Feature | Description |
|---|---|
| Total_Pages | Total Administrative, Informational, and ProductRelated pages |
| NonProduct_Duration | Combined Administrative and Informational duration |
| Avg_NonProduct_Duration_Per_Page | Average duration per non-product page |
| BounceExitRatio | BounceRates divided by ExitRates |
| Engagement_Score | ProductRelated page count multiplied by PageValues |

Month, VisitorType, OperatingSystems, Browser, Region, and TrafficType were one-hot encoded. Redundant component variables were removed after creating Total_Pages and NonProduct_Duration.

The final classification matrix contained 69 predictors. A stratified 80/20 split produced 9,764 training sessions and 2,441 testing sessions.

## Classification Models

Two classification models were developed:

1. **Logistic Regression** with StandardScaler and balanced class weights
2. **Random Forest Classifier** with balanced class weights and hyperparameter tuning

### Hyperparameter Tuning

GridSearchCV used three-fold stratified cross-validation and optimized F1 score. The focused search tested:

- max_depth: 8 and 12
- min_samples_leaf: 1 and 3
- min_samples_split: 2
- max_features: sqrt
- class_weight: balanced

The Random Forest used 150 trees. The best settings were:

- max_depth: 12
- min_samples_leaf: 3
- min_samples_split: 2
- max_features: sqrt
- class_weight: balanced

The best cross-validated F1 score was **0.6743**.

## Classification Results

| Model | Accuracy | F1 Score | ROC-AUC |
|---|---:|---:|---:|
| Logistic Regression | 0.8484 | 0.6255 | 0.9084 |
| Tuned Random Forest | 0.8763 | 0.6637 | 0.9331 |

The tuned Random Forest achieved the strongest overall performance.

### Confusion Matrix Summary

| Model | True Negatives | False Positives | False Negatives | True Positives |
|---|---:|---:|---:|---:|
| Logistic Regression | 1,762 | 297 | 73 | 309 |
| Tuned Random Forest | 1,841 | 218 | 84 | 298 |

Logistic Regression detected slightly more purchasing sessions, but the Random Forest reduced false positives and achieved the better F1 score.

### Important Classification Features

The most influential Random Forest features were:

- PageValues: approximately 0.294
- Engagement_Score: approximately 0.260
- ProductRelated_Duration: approximately 0.059
- ExitRates: approximately 0.058
- Total_Pages and ProductRelated: approximately 0.037 each

PageValues remained the strongest individual signal, which is consistent with the Deliverable 1 exploratory findings.

## K-Means Clustering

K-Means clustering used nine standardized behavioral features without including Revenue. Silhouette scores were compared for two through five clusters.

| Number of Clusters | Silhouette Score |
|---:|---:|
| 2 | 0.4658 |
| 3 | 0.4885 |
| 4 | 0.4025 |
| 5 | 0.4418 |

Three clusters were selected because they produced the highest silhouette score.

| Cluster | Sessions | Dataset Share | Purchase Rate | Interpretation |
|---|---:|---:|---:|---|
| 0 | 9,430 | 77.3% | 14.7% | Typical browsing sessions |
| 1 | 920 | 7.5% | 0.7% | Quick-exit sessions |
| 2 | 1,855 | 15.2% | 27.8% | Highly engaged sessions |

Cluster 1 had very high bounce and exit rates and almost no PageValues. Cluster 2 averaged approximately 91.4 product pages and 3,348.6 seconds of product-related duration.

PCA was used only to visualize the clusters in two dimensions. The two components explained approximately 56.54% of the variance.

## Association Rule Mining

The dataset contains session behavior rather than product baskets, so selected measures were converted into Boolean items using median-based thresholds. A compact Apriori implementation used a minimum support of 5% and generated frequent itemsets up to length four.

A total of 161 frequent itemsets were identified. Purchase rules were filtered to require at least 30% confidence and a lift of at least 1.20.

| Antecedent | Support | Confidence | Lift |
|---|---:|---:|---:|
| Low Bounce + Low Exit + Positive PageValues | 0.0738 | 0.6800 | 4.3498 |
| Low Bounce + Positive PageValues | 0.0818 | 0.6757 | 4.3222 |
| Long Product Duration + Low Bounce + Positive PageValues | 0.0560 | 0.6170 | 3.9467 |
| Low Exit + Positive PageValues | 0.1014 | 0.6126 | 3.9184 |
| Positive PageValues | 0.1260 | 0.5634 | 3.6037 |

The strongest patterns combined positive PageValues with low abandonment behavior. These rules describe co-occurrence and do not prove causation.

## Practical Applications

- Use the tuned classifier to prioritize high-intent sessions for assistance, offers, or remarketing.
- Simplify landing pages and product discovery for quick-exit sessions.
- Use product recommendations or targeted promotions for highly engaged sessions.
- Treat positive PageValues with low bounce and exit behavior as a strong high-intent signal.
- Use the patterns as decision support rather than guaranteed purchase predictions.

## Challenges Encountered

- **Class imbalance:** Purchases represented only 15.63% of sessions. Stratified splitting, balanced class weights, and multiple evaluation metrics were used.
- **Hyperparameter cost:** A focused grid was selected to improve the model without making the notebook unnecessarily expensive to run.
- **Cluster interpretation:** Numerical labels were translated into practical groups using behavioral profiles and purchase rates.
- **Association-rule preparation:** Continuous session measurements were converted into transparent Boolean items because the dataset was not a traditional product-basket dataset.
- **Causal interpretation:** Model importance and association rules were interpreted as patterns rather than causal effects.

## Repository Files

- `Deliverable_3.ipynb` – Classification, tuning, evaluation, clustering, and association rule mining
- `online_shoppers_cleaned.csv` – Cleaned dataset from Deliverable 1
- `Deliverable3_README.md` – Summary of methods, results, insights, and challenges

## How to Run

1. Place the notebook and `online_shoppers_cleaned.csv` in the same folder.
2. Open `Deliverable_3.ipynb` in Jupyter Notebook or Visual Studio Code.
3. Ensure the Python environment contains the required libraries.
4. Run the notebook cells from top to bottom.
5. Review the classification metrics, confusion matrices, ROC curves, cluster profiles, and association rules.

## Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipykernel
```

## Reference

Sakar, C., & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q
