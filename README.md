# CA03 – Decision Tree Income Classification

## Overview
This project builds and optimizes a Decision Tree classification model to predict whether an individual's income is **≤50K** or **>50K** using a processed census dataset. The goal is to understand how decision trees work, evaluate model performance, and analyze the impact of hyperparameter tuning on prediction accuracy and generalization.

---

## Dataset
The dataset contains approximately 48,000 observations derived from census data. Continuous variables were discretized into categorical bins prior to modeling to simplify decision rules and improve interpretability.

### Target Variable
- `y`
  - `0` → Income ≤ 50K  
  - `1` → Income > 50K

### Features (Binned)
- `age_bin`
- `workclass_bin`
- `education_bin`
- `education_num_bin`
- `occupation_bin`
- `msr_bin` (marital status & relationship)
- `race_sex_bin`
- `capital_gl_bin`
- `hours_per_week_bin`

---

## Project Workflow

### 1. Data Preparation
- Removed duplicates and missing values
- Used pre-binned categorical features
- Split data using provided `flag` column into:
  - Training dataset
  - Testing dataset

### 2. Encoding
Categorical variables were converted to numeric values using `LabelEncoder` so they could be used by the decision tree model.

### 3. Baseline Model
A baseline decision tree was trained using moderate regularization:
- `max_depth = 10`
- `min_samples_leaf = 15`
- `random_state = 101`

This served as a reference model before tuning.

---

## Hyperparameter Tuning

Four sequential experiments were performed:

### Run 1 — Split Criteria
- Tested: `gini`, `entropy`
- Result: Similar performance across both criteria.

### Run 2 — Minimum Samples per Leaf
- Tested values from 5–40
- Controlled model complexity and reduced overfitting.

### Run 3 — Maximum Features
- Tested: `sqrt`, `None`, and fractional values (0.3–0.8)
- Evaluated feature restriction as a form of regularization.

### Run 4 — Maximum Depth
- Tested depths from 2–16
- Identified optimal balance between underfitting and overfitting.

---

## Best Model
The final model was selected based on highest test accuracy after sequential tuning.

Key characteristics:
- Controlled depth
- Regularized leaf size
- Balanced bias–variance tradeoff
- Fast training time (< 1 second)

---

## Model Evaluation
Performance was evaluated using:
- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

The optimized tree demonstrated strong class separation and good generalization to unseen data.

---

## Tree Visualization
The final decision tree visualization shows:
- Important features appearing near the root
- Clear decision boundaries
- Mostly pure leaf nodes
- Interpretable if–then decision rules

Regularization prevented the tree from becoming fully grown, reducing overfitting risk.

---

## New Individual Prediction
A new individual was created using assignment-provided characteristics:

- Hours worked per week: 48  
- Occupation: Mid–Low  
- Marriage & relationship: High  
- Capital gain: Yes (>0)  
- Race–Sex group: Mid  
- Education years: 12  
- Education category: High  
- Work class: Income  
- Age: 58  

After encoding and prediction:

**Predicted Income:** `>50K`  
**Prediction Probability:** `94.74%`

---

## Key Insights
- Regularization parameters (`max_depth`, `min_samples_leaf`) had the greatest effect on performance.
- Split criterion choice had minimal impact.
- Decision trees remain highly interpretable compared to many ML models.
- Proper hyperparameter tuning significantly improves generalization.
