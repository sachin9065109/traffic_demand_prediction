# 🚦 Flipkart Gridlock Hackathon 2.0

## Overview

This repository contains my solution for the Flipkart Gridlock Hackathon 2.0, where the objective was to predict traffic demand using temporal, geographical, and environmental factors. The solution leverages advanced feature engineering and Gradient Boosting models to achieve strong predictive performance 


---

## Solution Approach

### 1. Data Exploration & Preprocessing

#### Data Integration

* Combined Train and Test datasets temporarily to ensure consistent preprocessing and encoding.

#### Missing Value Handling

* Filled missing values in **Temperature** using the median strategy to reduce the impact of outliers.
* Filled missing values in **RoadType** and **Weather** with a dedicated **"Unknown"** category.

#### Categorical Encoding

* Converted binary categorical features:

  * LargeVehicles → 0/1
  * Landmarks → 0/1
* Applied Label Encoding on:

  * geohash
  * RoadType
  * Weather

---

### 2. Feature Engineering

#### Temporal Features

Extracted useful information from the timestamp column:

* Hour
* Minute

#### Time Index Feature

Created a custom feature:

time_index = hour × 4 + (minute // 15)

This feature effectively captures 15-minute intervals throughout the day and significantly improved model performance.

#### Feature Reduction

Dropped:

* timestamp
* Index

to avoid redundancy and potential data leakage.

---

### 3. Model Selection

The following gradient boosting algorithms were evaluated:

* CatBoost Regressor
* XGBoost Regressor
* LightGBM Regressor

Performance was initially validated using an 80:20 train-validation split.

After comparison, **CatBoost Regressor** was selected due to:

* Higher R² Score
* Better generalization
* Strong handling of encoded categorical variables

---

### 4. Hyperparameter Tuning & Validation

#### Randomized Search

Used RandomizedSearchCV with 3-Fold Cross Validation to optimize:

* iterations
* learning_rate
* depth
* l2_leaf_reg

#### K-Fold Cross Validation

Applied:

* KFold (n_splits = 5)

Results showed stable performance across all folds, indicating good model generalization and minimal overfitting.

#### Feature Importance Analysis

Top contributing features included:

1. time_index
2. hour
3. geohash
4. Weather
5. Temperature

These insights confirmed the strong influence of temporal and location-based information on traffic demand prediction.

---

### 5. Final Prediction & Submission

* Retrained the optimized CatBoost model on the complete training dataset.
* Generated predictions for the test dataset.
* Carefully formatted the final submission file according to the competition requirements.
* Verified prediction alignment and output consistency before submission.

---

## Technologies Used

### Programming Language

* Python

### Libraries

* Pandas
* NumPy
* Matplotlib
* Scikit-Learn
* CatBoost
* XGBoost
* LightGBM

---

## Project Workflow

Data Collection
↓
Data Cleaning
↓
Feature Engineering
↓
Model Training
↓
Hyperparameter Tuning
↓
Cross Validation
↓
Feature Importance Analysis
↓
Final Model Training
↓
Prediction Generation
↓
Competition Submission

---

## Key Learnings

* Advanced feature engineering techniques for time-series traffic data.
* Practical experience with Gradient Boosting models.
* Hyperparameter optimization using RandomizedSearchCV.
* Model validation using K-Fold Cross Validation.
* Importance of temporal and geographical features in demand forecasting.

---

## Acknowledgements

I would like to sincerely thank the evaluation team and judges for reviewing my work.

A special thanks to Flipkart and the organizers of the Gridlock Hackathon 2.0 for creating an engaging and challenging competition. The experience provided valuable insights into machine learning, feature engineering, model optimization, and real-world predictive analytics.

This hackathon was an excellent learning opportunity and helped strengthen my understanding of practical machine learning workflows.
