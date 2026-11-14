# Activity Recognition System — Exploratory Data Analysis

## 1. Dataset Overview

**Dataset:** UCI Human Activity Recognition (HAR) Using Smartphones

The dataset contains smartphone sensor measurements collected from 30 volunteers performing six physical activities.

| Property | Details |
|---|---|
| Total observations | 10,299 |
| Training observations | 7,352 |
| Testing observations | 2,947 |
| Features | 561 |
| Activity classes | 6 |
| Sensor sampling frequency | 50 Hz |
| Window size | 128 time steps |
| Window duration | 2.56 seconds |
| Overlap | 50% |

### Activity Classes

1. Walking
2. Walking Upstairs
3. Walking Downstairs
4. Sitting
5. Standing
6. Laying

## 2. Dataset Structure

The dataset contains:

- `X_train.txt` and `X_test.txt`: Feature matrices.
- `y_train.txt` and `y_test.txt`: Activity labels.
- `subject_train.txt` and `subject_test.txt`: Participant identifiers.
- `Inertial Signals`: Raw accelerometer and gyroscope signals.

The training feature matrix has dimensions `(7352, 561)`, while the testing feature matrix has dimensions `(2947, 561)`.

Each raw sensor window contains 128 time steps.

## 3. Training and Testing Distribution

All six activity classes are represented in both training and testing datasets.

### Training distribution

| Activity | Samples |
|---|---:|
| Laying | 1,407 |
| Sitting | 1,286 |
| Standing | 1,374 |
| Walking | 1,226 |
| Walking Upstairs | 1,073 |
| Walking Downstairs | 986 |

### Testing distribution

| Activity | Samples |
|---|---:|
| Laying | 537 |
| Sitting | 491 |
| Standing | 532 |
| Walking | 496 |
| Walking Upstairs | 471 |
| Walking Downstairs | 420 |

The class distribution is reasonably balanced. No class-balancing technique was applied during the initial experiments.

## 4. Participant Separation

The training and testing datasets contain different participants.

- Training participants: 21
- Testing participants: 9
- Participants appearing in both sets: 0

This separation is important because it allows evaluation on participants that the model did not encounter during training.

## 5. Feature Inspection

The dataset contains 561 engineered features derived from accelerometer and gyroscope signals.

Feature categories include:

- Time-domain measurements.
- Frequency-domain measurements.
- Mean and standard deviation.
- Signal energy and magnitude.
- Correlation and angle measurements.

### Duplicate Feature Names

The feature-name inspection identified:

- 84 repeated feature-name entries.
- 126 rows involved in those repeated-name entries.
- No missing feature names.

These are repeated names in the feature metadata. They do not necessarily indicate identical feature values.

### Duplicate Feature Columns

A separate comparison identified 21 identical feature columns.

These columns were retained in the initial experiment. Their impact can be investigated in future experiments.

## 6. Data Quality Analysis

| Check | Result |
|---|---|
| Missing values | 0 |
| Infinite values | 0 |
| Zero-variance features | 0 |
| Identical feature columns | 21 |
| Overall minimum | -1.0 |
| Overall maximum | 1.0 |

The supplied feature matrix was already normalized to approximately the range [-1, 1].

No additional scaling or automatic outlier removal was applied for the initial Random Forest experiment.

## 7. Sensor Signal Visualization

Sensor signals were visualized across the six activities.

The visualizations included:

- Body acceleration along X, Y and Z axes.
- Body gyroscope along X, Y and Z axes.

The plots showed different signal patterns across activities.

Dynamic activities generally showed more variation in the sensor signals, while stationary activities showed relatively stable patterns.

## 8. Feature Distribution Analysis

Four features were selected for boxplot comparison:

1. `tBodyAcc-mean()-X`
2. `tBodyAcc-std()-X`
3. `tBodyGyro-mean()-X`
4. `tBodyGyro-std()-X`

### Observations

- Body acceleration mean alone showed substantial overlap between activities.
- Body acceleration standard deviation showed differences between stationary and dynamic activities.
- Gyroscope mean and standard deviation provided additional information about rotational movement.
- Some activities had overlapping distributions, suggesting that multiple features are needed for reliable classification.

## 9. EDA Conclusions

The dataset was found to be suitable for the initial machine-learning experiment.

Key conclusions:

- All six activity classes were represented.
- No missing or infinite values were found.
- No zero-variance features were identified.
- The supplied feature matrix was already normalized.
- Training and testing participants were completely separate.
- Identical feature columns were identified and retained initially.
- Outliers were not removed automatically.

The next stage was to train a Random Forest classifier using the 561 engineered features.

---

## 10. Experiment Information

**Project:** Activity Recognition System  
**Dataset:** UCI HAR Dataset  
**EDA notebook:** `01_data_exploration.ipynb`  
**Next stage:** Random Forest classification

