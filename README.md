SELIC Direction Classification — Machine Learning Project

This project predicts whether the next SELIC decision will be higher or not higher than the current rate.
Instead of forecasting the exact value, the goal is to classify the direction of monetary policy.

The pipeline includes:

Data preparation

Feature engineering

Three classification models

Threshold adjustment (0.25) to increase sensitivity

Performance evaluation with confusion matrices and ROC AUC

Tableau dashboard for visual insights

📌 Problem Definition

Target variable:
1 → SELIC will increase
0 → SELIC will stay the same or decrease

Central banks often move slowly, so the dataset is naturally imbalanced.
This impacts precision/recall — hence the need to evaluate multiple metrics.

📊 Dataset & Features

The dataset includes macro indicators such as:

Inflation indicators

Activity indicators

Previous SELIC levels

Lagged features

External expectations (if available)

After cleaning:

Missing values handled

Lags created

Train/test split applied

🤖 Models Evaluated (threshold = 0.25)
1. Logistic Regression

Confusion Matrix:

[[12  0]
 [ 9  2]]

Precision (class 1): 1.00

Recall (class 1): 0.18

F1-score (class 1): 0.31

ROC AUC: 0.68

Idea:
Very conservative — rarely predicts a SELIC hike, but when it does, it’s precise.
Low recall → misses many true hikes.

2. Random Forest

Confusion Matrix:

[[10  2]
 [ 6  5]]

Precision (class 1): 0.71

Recall (class 1): 0.45

F1-score (class 1): 0.56

ROC AUC: 0.70

Idea:
More balanced: catches more hikes but with some false alarms.
Best “practical” model depending on use-case.

3. XGBoost

Confusion Matrix:

[[12  0]
 [11  0]]

Precision (class 1): 0.00

Recall (class 1): 0.00

F1-score (class 1): 0.00

ROC AUC: 0.81

Idea:
High ROC AUC but collapses at threshold 0.25 → never predicts a hike.
Needs tuning or different threshold.

🧠 Interpretation

Logistic Regression: stable but under-sensitive

Random Forest: best balance between catching increases and limiting mistakes

XGBoost: strong ranking ability (AUC) but threshold-dependent

Because central bank decisions are rare events, recall becomes crucial depending on your scenario:

Analysts who want early signals → prefer recall

Analysts who want fewer false alarms → prefer precision
