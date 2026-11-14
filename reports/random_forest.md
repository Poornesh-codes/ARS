# Activity Recognition System — Random Forest Experiment

## 1. Objective

The objective of this experiment was to establish a baseline activity classification model using the 561 engineered features provided by the UCI HAR dataset.

Random Forest was selected as the first model because it is an ensemble learning algorithm that combines multiple decision trees.

## 2. Input Data

| Property | Value |
|---|---|
| Training samples | 7,352 |
| Testing samples | 2,947 |
| Input features | 561 |
| Output classes | 6 |
| Training participants | 21 |
| Testing participants | 9 |

The original subject-wise training and testing split was preserved.

## 3. Model Configuration

Algorithm: Random Forest Classifier

Configuration:

| Parameter | Value |
|---|---:|
| Number of estimators | 200 |
| Random state | 42 |
| Number of jobs | -1 |

The model was trained using the training feature matrix and corresponding activity labels.

## 4. Model Performance

**Test accuracy: 92.57%**

The model correctly classified 2,728 out of 2,947 test samples.

### Classification Report

| Activity | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| Walking | 0.90 | 0.96 | 0.93 | 496 |
| Walking Upstairs | 0.89 | 0.91 | 0.90 | 471 |
| Walking Downstairs | 0.96 | 0.85 | 0.90 | 420 |
| Sitting | 0.92 | 0.89 | 0.90 | 491 |
| Standing | 0.90 | 0.92 | 0.91 | 532 |
| Laying | 1.00 | 1.00 | 1.00 | 537 |
| **Macro Average** | **0.93** | **0.92** | **0.92** | **2,947** |
| **Weighted Average** | **0.93** | **0.93** | **0.93** | **2,947** |

## 5. Confusion Matrix Analysis

The confusion matrix showed the following correct classifications:

| Actual Activity | Correct Predictions |
|---|---:|
| Walking | 476 / 496 |
| Walking Upstairs | 430 / 471 |
| Walking Downstairs | 358 / 420 |
| Sitting | 435 / 491 |
| Standing | 492 / 532 |
| Laying | 537 / 537 |

### Main Observations

**Walking activities**

- 35 walking-upstairs samples were classified as walking.
- 44 walking-downstairs samples were classified as walking upstairs.
- Similar movement patterns can make these activities difficult to distinguish.

**Stationary activities**

- 56 sitting samples were classified as standing.
- 40 standing samples were classified as sitting.
- Both activities have relatively stable sensor patterns.

**Laying**

- All 537 laying samples were correctly classified.

These observations indicate that the model performs well overall but has difficulty distinguishing certain physically similar activities.

## 6. Feature Importance Analysis

Random Forest feature importance was used to identify features that contributed most to impurity reduction across the decision trees.

### Top 10 Features

| Rank | Feature | Importance |
|---:|---|---:|
| 1 | `tGravityAcc-mean()-X` | 0.041767 |
| 2 | `tGravityAcc-min()-X` | 0.031873 |
| 3 | `tGravityAcc-mean()-Y` | 0.029814 |
| 4 | `angle(X,gravityMean)` | 0.026029 |
| 5 | `tGravityAcc-energy()-X` | 0.024059 |
| 6 | `angle(Y,gravityMean)` | 0.023229 |
| 7 | `tGravityAcc-max()-X` | 0.022452 |
| 8 | `tGravityAcc-min()-Y` | 0.022102 |
| 9 | `tGravityAcc-max()-Y` | 0.019056 |
| 10 | `tGravityAcc-energy()-Y` | 0.016208 |

### Observations

Gravity-related acceleration features appeared prominently among the most important features.

These features can help capture smartphone orientation and posture-related differences.

Feature importance represents the model's impurity-based importance scores. It does not establish causation or directly measure the accuracy contribution of an individual feature.

## 7. Experiment Conclusion

The Random Forest model achieved approximately 92.57% test accuracy using the 561 engineered features.

The experiment established a strong baseline for comparison with deep learning models.

The confusion matrix highlighted classification challenges involving:

- Walking upstairs and walking downstairs.
- Sitting and standing.

The feature importance analysis showed that gravity-related features played an important role in the trained model.

## 8. Limitations and Future Experiments

- Investigate the effect of identical feature columns.
- Compare Random Forest with other classification algorithms.
- Explore raw sensor sequences using a 1D CNN.
- Explore temporal dependencies using an LSTM.
- Compare all models using the same subject-wise test set.

---

**Project:** Activity Recognition System  
**Dataset:** UCI HAR Dataset  
**Experiment:** Random Forest baseline  
**Notebook:** `02_random_forest.ipynb`  
**Status:** Completed
