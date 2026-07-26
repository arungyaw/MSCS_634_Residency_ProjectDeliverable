# MSCS 634 Project Deliverable 4

## Final Insights, Recommendations, and Consolidated Analysis

### Group Members

- Arun Gyawali
- Kashif Ali Syed
- Jiwon Jung
- Hanuman Sai Chanukya Srinivas Chilamkuri
  
## Project Presentation

The recorded presentation for the complete final project is available at the link below:

**Presentation Video:**

https://cumber-my.sharepoint.com/:v:/g/personal/agyawali33472_ucumberlands_edu/IQB_iRQAJ0xJS6PXZ0eLlaxQAf47dmp9HianbqrY_om6Dk0?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=RfTwer&referrer=Outlook.Desktop&referrerScenario=email-linkwithembed

This presentation summarizes the complete project, including Deliverable 1 (Data Preparation and Exploratory Data Analysis), Deliverable 2 (Feature Engineering and Regression Modeling), Deliverable 3 (Classification, Clustering, and Association Rule Mining), and Deliverable 4 (Final Analysis, Recommendations, Ethical Considerations, and Future Work).
## Project Overview

Deliverable 4 consolidates the complete data-mining workflow developed in Deliverables 1, 2, and 3. The project uses the **Online Shoppers Purchasing Intention Dataset** to examine online shopping behavior, predict engagement and purchasing outcomes, identify behavioral session groups, and discover purchase-related patterns.

The same cleaned dataset was used throughout the project to maintain consistency across data preparation, regression, classification, clustering, and association rule mining.

## Dataset

**Dataset:** Online Shoppers Purchasing Intention Dataset  
**Source:** UCI Machine Learning Repository  
**Original shape:** 12,330 rows and 18 columns  
**Cleaned shape:** 12,205 rows and 18 columns  
**Regression target:** ProductRelated_Duration  
**Classification target:** Revenue  
**Purchase rate:** 15.63%

Each record represents one online shopping session. The attributes describe page visits, browsing durations, bounce rates, exit rates, page values, visitor characteristics, seasonal information, traffic source, and purchasing outcome.

## Consolidated Project Workflow

### Data Preparation and Exploration

- Inspected the original dataset structure and data types
- Checked for missing, invalid, inconsistent, and noisy values
- Removed 125 exact duplicate records
- Capped extreme duration values at their 99th-percentile limits
- Performed exploratory data analysis using distributions, boxplots, correlations, conversion rates, and engagement comparisons
- Saved the cleaned dataset for use in all later deliverables

### Feature Engineering and Regression

Five behavioral features were created:

| Engineered Feature | Description |
|---|---|
| Total_Pages | Total pages visited across the three page categories |
| NonProduct_Duration | Combined Administrative and Informational duration |
| Avg_NonProduct_Duration_Per_Page | Average time spent per non-product page |
| BounceExitRatio | Ratio of BounceRates to ExitRates |
| Engagement_Score | ProductRelated page count multiplied by PageValues |

Linear Regression, Ridge Regression, Lasso Regression, and Random Forest Regression were evaluated using R-squared, MSE, RMSE, and five-fold cross-validation.

### Classification and Hyperparameter Tuning

Revenue was predicted using:

1. Logistic Regression with standardized features and balanced class weights
2. Random Forest Classifier with balanced class weights and GridSearchCV tuning

Classification was evaluated using accuracy, F1 score, confusion matrices, and ROC-AUC.

### Clustering

K-Means clustering used nine standardized behavioral features without including Revenue. Silhouette scores were compared for two through five clusters. PCA was used only to visualize the final clusters in two dimensions.

### Association Rule Mining

Session behavior was converted into Boolean items using median-based thresholds and existing categorical conditions. A compact Apriori implementation identified frequent itemsets and purchase rules using support, confidence, and lift.

## Final Model Results

### Regression Results

| Model | Test R-squared | Test RMSE | CV R-squared | CV RMSE |
|---|---:|---:|---:|---:|
| Linear Regression | 0.7188 | 832.46 | 0.7318 | 803.28 |
| Ridge Regression | 0.7188 | 832.57 | 0.7318 | 803.28 |
| Lasso Regression | 0.7190 | 832.22 | 0.7321 | 802.96 |
| Random Forest | 0.7506 | 784.02 | 0.7702 | 742.97 |

Random Forest was the best regression model. Its stronger performance indicates that product-related browsing duration contains non-linear relationships.

### Classification Results

| Model | Accuracy | F1 Score | ROC-AUC |
|---|---:|---:|---:|
| Logistic Regression | 0.8484 | 0.6255 | 0.9084 |
| Tuned Random Forest | 0.8759 | 0.6759 | 0.9340 |

The tuned Random Forest correctly classified:

- 1,822 non-purchasing sessions
- 316 purchasing sessions

It produced 237 false positives and 66 false negatives.

### Clustering Results

Three clusters were selected because they produced the highest silhouette score of **0.4885**.

| Cluster | Sessions | Dataset Share | Purchase Rate | Interpretation |
|---|---:|---:|---:|---|
| 0 | 9,430 | 77.3% | 14.7% | Typical browsing sessions |
| 1 | 920 | 7.5% | 0.7% | Quick-exit sessions |
| 2 | 1,855 | 15.2% | 27.8% | Highly engaged sessions |

The two PCA components used for visualization explained approximately **56.54%** of the variance.

### Association Rule Results

Apriori identified **161 frequent itemsets**.

The strongest purchase rule combined:

- Positive PageValues
- Low bounce rate
- Low exit rate

The rule achieved:

- Support: **0.0738**
- Confidence: **0.6800**
- Lift: **4.3498**

This means sessions matching the pattern purchased at more than four times the overall purchase rate. The rule represents association rather than causation.

## Major Integrated Findings

- PageValues was the most consistent purchasing signal across EDA, classification, and association rule mining.
- Product-page count and total page activity were the strongest predictors of product-related browsing duration.
- Random Forest outperformed the linear regression and classification baselines, showing that important relationships in the dataset were non-linear.
- Purchasing sessions generally had greater engagement and lower bounce and exit rates.
- Quick-exit sessions rarely purchased, while highly engaged sessions had the highest cluster purchase rate.
- Revenue was imbalanced, so F1 score, ROC-AUC, stratified splitting, and confusion matrices were more informative than accuracy alone.
- Feature importance, clustering, and association rules identify patterns but do not prove causation.

## Practical Recommendations

- Use the tuned classifier as a decision-support tool for identifying high-intent sessions when the necessary features are available.
- Simplify landing pages and product discovery for quick-exit sessions.
- Provide product recommendations, comparison tools, or carefully timed promotions for highly engaged sessions.
- Treat positive PageValues combined with low bounce and exit rates as a strong high-intent pattern.
- Use November conversion patterns to support seasonal campaign and inventory planning.
- Monitor model performance and customer behavior over time.

## Ethical Considerations

- Protect session-level browsing information through data minimization, access controls, encryption, and appropriate retention policies.
- Evaluate performance across visitor groups because region, browser, traffic source, and similar attributes may act as indirect proxies for demographic or socioeconomic differences.
- Monitor false positives and false negatives because class imbalance may affect groups differently.
- Communicate predictions as probabilities rather than guaranteed outcomes.
- Use personalization to improve customer experience rather than manipulate customers.
- Do not interpret feature importance or association rules as proof of causation.

## Limitations

- The dataset contains sessions rather than identified customers.
- Product-level transaction baskets are unavailable.
- January and April are absent from the monthly data.
- PageValues may not be available early enough for every real-time application.
- Results from one historical dataset may not generalize to other websites or industries.
- K-Means assumes compact clusters and requires the number of clusters in advance.
- Median-based rule thresholds may not be optimal for every business context.

## Future Improvements

- Compare Gradient Boosting and other advanced ensemble models
- Tune classification thresholds using business costs
- Evaluate probability calibration
- Apply SHAP or another explainability method
- Use time-based validation to measure model drift
- Compare K-Means with Hierarchical and DBSCAN clustering
- Use product-level transaction data for traditional basket analysis
- Evaluate fairness across meaningful visitor groups

## Repository Files

- `Deliverable_4_Final_Project.ipynb` – Consolidated code, visualizations, results, insights, recommendations, ethics, and limitations
- `online_shoppers_cleaned.csv` – Cleaned dataset used throughout the project
- `Deliverable4_README.md` – Deliverable 4 summary
- `MSCS_634_Final_Report.docx` or `.pdf` – Comprehensive written report
- `MSCS_634_Final_Presentation.pptx` or `.pdf` – Presentation used for the 5–7-minute video

## How to Run

1. Place `Deliverable_4_Final_Project.ipynb` and `online_shoppers_cleaned.csv` in the same folder.
2. Open the notebook in Jupyter Notebook or Visual Studio Code.
3. Install the required libraries.
4. Restart the kernel and run all cells from top to bottom.
5. Review the generated tables, model results, visualizations, and final recommendations.

## Required Libraries

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipykernel
```

## Reference

Sakar, C., & Kastro, Y. (2018). *Online Shoppers Purchasing Intention Dataset* [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q
