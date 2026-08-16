# Driver_Behaviour_Analysis
# Driver Behaviour & Road Safety AI

## Overview

This project analyzes vehicle acceleration and braking behaviour to identify potentially aggressive or risky driving events.

The pipeline includes data cleaning, EDA, feature engineering, Random Forest classification, threshold optimization, error analysis, unseen-data testing, and driver/trip-level safety scoring.

## Dataset

The dataset contains 54 unique CSV files with 32,987 raw rows.

The target variable is:

* `0` = Non-Aggressive
* `1` = Aggressive

The model uses 13 acceleration and braking features, including acceleration components, acceleration magnitude, horizontal/vertical acceleration, short-term acceleration statistics, and acceleration changes.

## Machine Learning

A Random Forest classifier was trained to detect aggressive driving behaviour.

A probability threshold of `0.15` was selected to prioritize detection of aggressive events.

Held-out test performance:

* Accuracy: 44.75%
* Precision: 27.35%
* Recall: 87.55%
* F1 Score: 41.67%
* ROC-AUC: 63.75%
* PR-AUC: 32.37%

The model has high recall but a high false-positive rate, so it should currently be considered a prototype rather than a production-ready system.

## Key Findings

Short-term acceleration behaviour was particularly important for classification. `acc_mean_5` was the most important feature, followed by `acc_std_5`.

Sudden acceleration had the highest average acceleration magnitude among the analyzed driving events, followed by sudden braking.

Error analysis showed that some non-aggressive events have acceleration patterns similar to aggressive events, contributing to false positives.

## Unseen-Data Testing

The model was tested on a genuinely unseen CSV file that was excluded from training.

Results:

* Accuracy: 53.62%
* Precision: 50.41%
* Recall: 83.26%
* F1 Score: 62.80%
* ROC-AUC: 61.86%

These results show that the model can detect aggressive events in unseen data, although further validation is required.

## Driver Safety Score

A driver/trip-level Safety Score was developed using indicators such as aggressive-event rate, harsh braking, rapid acceleration, acceleration variability, acceleration changes, and driving smoothness.

The proposed score ranges from 0–100:

* 80–100: Safe
* 60–79: Moderate
* 40–59: Risky
* 0–39: High Risk

This is a project prototype and requires further validation before real-world deployment.

## Project Structure

```text
data/
notebooks/
models/
results/
reports/
README.md
requirements.txt
```

The repository should contain the cleaned/engineered data, notebooks, trained model, evaluation results, final report, and presentation materials.

## Future Improvements

Future work should include more diverse drivers and vehicles, additional road conditions, longer temporal features, driver-level validation, probability calibration, and comparison with models such as XGBoost or LightGBM.

The Safety Score should also be validated against independently labelled driving sessions.

## Conclusion

The project provides an end-to-end prototype for detecting aggressive acceleration and braking behaviour and converting behavioural indicators into a driver/trip-level safety score.

The current model prioritizes sensitivity and detects a large proportion of aggressive events. Reducing false positives and improving generalization are the main areas for future development.
