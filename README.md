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

- Perform feature engineering
- Build at least two regression models
- Evaluate models using R-squared, MSE, and RMSE
- Apply cross-validation
- Compare model performance

**Status:** Not started

### Deliverable 3: Classification, Clustering, and Pattern Mining

- Build at least two classification models
- Perform hyperparameter tuning
- Evaluate models using accuracy, F1 score, confusion matrix, and ROC curve
- Develop a clustering model
- Apply association rule mining
- Explain practical applications of the findings

**Status:** Not started

### Deliverable 4: Final Insights and Recommendations

- Combine findings from all deliverables
- Summarize preprocessing and modeling results
- Provide practical recommendations
- Discuss data privacy, fairness, and possible bias
- Prepare the final report and presentation

**Status:** Not started

## Current Key Findings

- The cleaned dataset contains 12,205 unique sessions.
- Approximately 15.63% of sessions resulted in a purchase.
- PageValues had the strongest positive relationship with Revenue.
- Purchasing sessions had greater product engagement.
- Purchasing sessions had lower bounce and exit rates.
- November had the highest monthly conversion rate.
- Weekend sessions had a slightly higher conversion rate than weekday sessions.

## Repository Structure

```text
MSCS_634_Project/
│
├── MSCS_634_ProjectDeliverable_1/
│   ├── Project_Deliverable_1.ipynb
│   ├── online_shoppers_intention.csv
│   ├── online_shoppers_cleaned.csv
│   └── Deliverable1_README.md
│
├── MSCS_634_ProjectDeliverable_2/
├── MSCS_634_ProjectDeliverable_3/
├── MSCS_634_ProjectDeliverable_4/
└── README.md