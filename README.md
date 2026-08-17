# Driver Behaviour & Road Safety AI

## Overview

This project analyzes vehicle acceleration and braking behaviour to identify potentially aggressive or risky driving events.

The pipeline includes data cleaning, exploratory data analysis, feature engineering, Random Forest classification, threshold optimization, error analysis, unseen-data testing, and driver/trip-level safety scoring.

## Dataset

The dataset contains 54 unique CSV files with 32,987 raw rows.

The target variable is:

* 0 = Non-Aggressive
* 1 = Aggressive

The model uses 13 engineered acceleration and braking features, including acceleration components, acceleration magnitude, horizontal and vertical acceleration, rolling acceleration statistics, and acceleration changes.

## Machine Learning

A Random Forest classifier was trained to detect aggressive driving behaviour.

A classification threshold of **0.15** was selected to prioritize detection of aggressive events.

Final test-set performance:

* Accuracy: 45.51%
* Precision: 26.83%
* Recall: 86.20%
* F1 Score: 40.93%
* ROC-AUC: 64.75%
* PR-AUC: 32.30%

The model prioritizes recall, successfully detecting most aggressive events. However, the relatively low precision indicates a high number of false positives. Therefore, the current model should be considered a research/prototype system rather than a production-ready safety system.

## Key Findings

Short-term acceleration behaviour was highly important for classification. `acc_mean_5` was the most important feature in the Random Forest model.

Other important indicators included acceleration variation, acceleration components, horizontal acceleration, and changes in acceleration.

The model's errors show that some non-aggressive driving conditions have acceleration patterns similar to aggressive events, resulting in false-positive predictions.

## Unseen-Data Testing

The model was also tested on a genuinely unseen CSV file that was excluded from model training.

This evaluation is used to assess whether the model can generalize to a driving session that it has not previously seen.

The unseen-data results are documented separately in the final evaluation report.

## Driver Safety Score

A driver/trip-level Safety Score was developed using behavioural indicators such as aggressive-event rate, harsh braking, rapid acceleration, acceleration variability, acceleration changes, and driving smoothness.

The proposed score ranges from 0–100:

* 80–100: Safe
* 60–79: Moderate
* 40–59: Risky
* 0–39: High Risk

The Safety Score is a project prototype and requires additional validation before real-world deployment.

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

The repository contains the data-processing pipeline, engineered features, trained model, evaluation results, reports, and presentation materials.

## Future Improvements

Future work should include more diverse drivers and vehicles, additional road and traffic conditions, improved temporal features, driver-level validation, probability calibration, and comparison with other machine learning models.

The Safety Score should also be validated against independently labelled driving sessions.

## Conclusion

The project provides an end-to-end prototype for detecting aggressive acceleration and braking behaviour and converting behavioural indicators into a driver/trip-level safety score.

The final Random Forest model prioritizes sensitivity, achieving **86.20% recall** for aggressive driving events. Reducing false positives and improving generalization to unseen driving sessions are the primary areas for future improvement.
