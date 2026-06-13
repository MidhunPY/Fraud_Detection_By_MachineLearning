# Fraud Detection using Machine Learning

## Project Overview

This project focuses on detecting fraudulent financial transactions using Machine Learning classification algorithms. The complete ML pipeline includes Exploratory Data Analysis (EDA), data preprocessing, feature engineering, feature scaling, handling class imbalance, model comparison, cross-validation, hyperparameter tuning, and model evaluation.

## Goal

The objective was to build an effective fraud detection system capable of identifying fraudulent transactions while minimizing false alarms. Multiple classification models were evaluated and compared to select the best-performing model.

---

# Project Workflow

## Exploratory Data Analysis (EDA)

### Univariate Analysis
- Transaction Amount
- Transaction Hour
- Device Trust Score
- Transaction Velocity
- Cardholder Age

### Bivariate Analysis
- Device Trust Score vs Fraud
- Transaction Velocity vs Fraud
- Foreign Transaction vs Fraud
- Location Mismatch vs Fraud
- Merchant Category vs Fraud

### Key Findings
- Fraud transactions were more common when Device Trust Score was low.
- Fraudulent transactions generally occurred at higher transaction velocities.
- Foreign transactions showed higher fraud rates.
- Location mismatch was positively associated with fraud.
- Merchant categories exhibited different fraud rates.

---

## Data Preprocessing

- Removed unnecessary feature (`transaction_id`)
- Performed Train-Test Split (80:20)
- Used Stratified Sampling to preserve class distribution

---

## Feature Engineering

### One-Hot Encoding

Applied One-Hot Encoding on:

```python
merchant_category
```

Generated Features:

```python
merchant_category_Electronics
merchant_category_Food
merchant_category_Grocery
merchant_category_Travel
```

---

## Feature Scaling

Used RobustScaler due to the presence of outliers.

Scaled Features:

```python
amount
transaction_hour
device_trust_score
velocity_last_24h
cardholder_age
```

---

## Handling Imbalanced Data

Dataset Distribution:

```text
Fraud Transactions     ≈ 1.5%
Non-Fraud Transactions ≈ 98.5%
```

Techniques Evaluated:

- Class Weighting
- SMOTE (Synthetic Minority Oversampling Technique)

---

# Models Implemented

## 🔹 Logistic Regression

Baseline classification model.

## 🔹 Logistic Regression + Class Weight

Applied class weighting to improve fraud detection recall.

## 🔹 Logistic Regression + SMOTE

Evaluated synthetic oversampling.

## 🔹 Random Forest Classifier

Tree-based ensemble model capable of capturing non-linear relationships.

## 🔹 Random Forest + Class Weight

Evaluated class weighting with Random Forest.

## 🔹 Random Forest + SMOTE

Evaluated oversampling with Random Forest.

## 🔹 XGBoost Classifier

Gradient Boosting-based ensemble model.

Achieved the best overall performance.

---

# Model Evaluation

Evaluation Metrics Used:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix
- Cross Validation

### Why F1-Score?

Since the dataset was highly imbalanced, F1-Score was selected as the primary evaluation metric because it balances Precision and Recall.

---

# Cross Validation

Performed 5-Fold Stratified Cross Validation.

| Model | Mean CV F1 |
|---------|---------|
| Random Forest | 0.715 |
| XGBoost | 0.956 |
| Tuned XGBoost | 0.988 |

---

# Hyperparameter Tuning

Applied:

```python
RandomizedSearchCV
```

with:

```python
StratifiedKFold(n_splits=5)
```

### Tuned Parameters

- n_estimators
- max_depth
- learning_rate
- subsample
- colsample_bytree

### Best Parameters

```python
{
 'subsample': 1.0,
 'n_estimators': 300,
 'max_depth': 3,
 'learning_rate': 0.1,
 'colsample_bytree': 0.8
}
```

### Best Cross Validation Score

```python
F1 Score = 0.988
```

---

# Final Model Selection

🏆 Tuned XGBoost Classifier

Reason:
- Highest Test Performance
- Highest Cross Validation F1 Score
- Better Generalization compared to Random Forest

---

# Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Imbalanced-Learn (SMOTE)
- XGBoost
- Joblib

---

# Outcome

Successfully developed a fraud detection model capable of accurately identifying fraudulent transactions. Among all evaluated models, Tuned XGBoost achieved the best performance and was selected as the final deployment model.
