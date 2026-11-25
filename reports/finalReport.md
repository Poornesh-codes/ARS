# ACTIVITY RECOGNITION SYSTEM (ARS)

---

## 1. Abstract

The Activity Recognition System (ARS) is a machine-learning-based project that identifies human physical activities using smartphone sensor data. It uses accelerometer and gyroscope measurements collected while people perform different activities.

The project uses the UCI Human Activity Recognition (HAR) Using Smartphones dataset, which contains sensor readings from 30 volunteers performing six activities: Walking, Walking Upstairs, Walking Downstairs, Sitting, Standing, and Laying.

Different machine-learning approaches were implemented and evaluated, including Random Forest classifiers and a one-dimensional Convolutional Neural Network (1D CNN). The experiments compare manually extracted statistical features, pre-engineered features supplied with the dataset, and raw sensor time-series data.

The best recorded result was **92.87% test accuracy**, achieved by the CNN trained on normalized sensor data.

## 2. Introduction

Human Activity Recognition (HAR) is the process of identifying physical activities using data collected from sensors. Smartphones contain inertial sensors such as accelerometers and gyroscopes that can capture movement and orientation.

These sensor readings can be processed using machine-learning algorithms to recognize activities automatically.

The objective of this project is to investigate how different machine-learning techniques can classify human activities from smartphone sensor measurements.

### 2.1 Problem Statement

To develop and evaluate a machine-learning system that classifies human physical activities using smartphone accelerometer and gyroscope data.

### 2.2 Objectives

- Understand and explore smartphone sensor data.
- Preprocess and prepare the dataset for model training.
- Implement Random Forest classification using different feature representations.
- Implement a 1D CNN to learn patterns from raw sensor sequences.
- Compare model performance using test accuracy and classification metrics.
- Identify the strengths and limitations of the implemented approaches.

## 3. Dataset Description

The project uses the **UCI Human Activity Recognition Using Smartphones dataset**.

The dataset was collected from 30 volunteers performing six different physical activities while carrying a waist-mounted smartphone.

### 3.1 Dataset Details

| Parameter | Description |
|---|---|
| Dataset | UCI HAR |
| Total observations | 10,299 |
| Participants | 30 |
| Activity classes | 6 |
| Training samples | 7,352 |
| Testing samples | 2,947 |
| Sampling frequency | 50 Hz |
| Window size | 128 time steps |
| Window duration | 2.56 seconds |
| Engineered features | 561 |

### 3.2 Activity Classes

1. Walking
2. Walking Upstairs
3. Walking Downstairs
4. Sitting
5. Standing
6. Laying

### 3.3 Sensor Data

The dataset contains measurements from:

- Accelerometer: measures acceleration along three axes.
- Gyroscope: measures angular velocity along three axes.

The raw sensor windows used by the CNN contain nine channels:

- Body acceleration (X, Y, Z)
- Body gyroscope (X, Y, Z)
- Total acceleration (X, Y, Z)

Each input window has a shape of **128 × 9**.

## 4. Methodology

The project follows a machine-learning workflow consisting of data exploration, preprocessing, model training, evaluation, and comparison.

### 4.1 Exploratory Data Analysis

The dataset was examined to understand its structure and quality.

The analysis included:

- Checking the distribution of the six activity classes.
- Inspecting sensor signals across different activities.
- Identifying missing and infinite values.
- Checking zero-variance and duplicate feature columns.
- Visualizing selected feature distributions.
- Verifying the separation of training and testing participants.

The analysis identified no missing values, infinite values, or zero-variance features in the supplied feature matrix.

### 4.2 Data Preprocessing

The dataset provides two main forms of input:

1. Engineered features: 561 features calculated from sensor measurements.
2. Raw sensor signals: sequential accelerometer and gyroscope readings.

For the CNN experiments, raw sensor windows were prepared in a format suitable for one-dimensional convolution.

A separate normalized version of the raw sensor data was also prepared. Standardization was performed using statistics calculated from the training data.

The official subject-wise train/test separation was preserved. This helps evaluate the models on participants not used during training.

### 4.3 Random Forest Classification

Random Forest is an ensemble machine-learning algorithm that combines multiple decision trees to make predictions.

Two Random Forest experiments were conducted:

- **Experiment 1:** Classification using 28 manually calculated statistical features.
- **Experiment 2:** Classification using the 561 engineered features provided by the UCI dataset.

The predictions from the decision trees are combined to produce the final activity classification.

### 4.4 Convolutional Neural Network

A one-dimensional Convolutional Neural Network (1D CNN) was implemented to learn patterns from sequential sensor measurements.

Unlike the Random Forest experiments, which use feature vectors, the CNN receives sensor time-series windows as input.

Two CNN experiments were conducted:

- CNN trained on raw sensor windows.
- CNN trained on normalized sensor windows.

Normalization brings sensor measurements to comparable numerical scales and can help neural networks learn more effectively.

## 5. Tools and Technologies Used

| Tool / Technology | Purpose |
|---|---|
| Python | Main programming language |
| Google Colab | Development and model training environment |
| NumPy | Numerical operations |
| Pandas | Dataset handling and analysis |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| Scikit-learn | Random Forest, preprocessing and evaluation |
| TensorFlow / Keras | CNN implementation and training |
| Jupyter Notebook | Experiment documentation and execution |
| GitHub | Source-code version control |

## 6. Experimental Results

Four model experiments were evaluated using the test dataset.

### 6.1 Model Comparison

| Model | Input Representation | Test Accuracy |
|---|---|---:|
| Random Forest | 28 custom statistical features | 72.51% |
| Random Forest | 561 engineered features | 92.60% |
| 1D CNN | Raw sensor data | 92.43% |
| 1D CNN | Normalized sensor data | **92.87%** |

### 6.2 Results Discussion

**Random Forest with 28 features**

The model achieved 72.51% accuracy. This experiment established a baseline using a smaller set of manually calculated statistical features.

**Random Forest with 561 features**

The model achieved 92.60% accuracy. The larger engineered feature representation provided substantially more information for distinguishing activities.

**CNN with raw sensor data**

The CNN achieved 92.43% accuracy by learning patterns directly from sequential sensor measurements.

**CNN with normalized sensor data**

The normalized CNN achieved the highest recorded accuracy of 92.87%. This indicates that standardizing the sensor measurements provided a small improvement in this experiment.

### 6.3 Overall Observation

The experiments demonstrate that both engineered features and raw sensor sequences can be used effectively for human activity recognition.

The normalized CNN achieved the best recorded test accuracy among the four experiments.

## 7. Database Requirements

The current project is an offline machine-learning experiment that uses a prepared dataset.

A traditional database is not required for the current implementation because the dataset is loaded and processed directly using Python.

The trained models are exported as model files for reuse.

A database could be introduced in a future application to store user information, sensor records, activity history, and prediction results.

## 8. Limitations

- The current implementation works with the prepared UCI HAR dataset.
- It does not currently collect live sensor readings from a smartphone.
- It does not include a deployed web or mobile application.
- Performance may vary when tested with sensor data collected from different devices or environments.
- Similar activities, such as Sitting and Standing or different walking movements, can be difficult to distinguish.

## 9. Future Scope

The project can be extended in several ways:

- Integrate smartphone sensors for real-time activity recognition.
- Develop a web or mobile interface for activity predictions.
- Evaluate the models on data collected from additional participants and devices.
- Explore additional deep-learning architectures such as LSTM.
- Optimize the model for mobile and edge-device deployment.
- Store activity predictions and historical records for analysis.

## 10. Conclusion

The Activity Recognition System demonstrates the use of machine-learning and deep-learning techniques to classify human physical activities using smartphone sensor data.

The project explored the UCI HAR dataset, performed exploratory data analysis, and implemented four classification experiments using Random Forest and 1D CNN models.

Among the implemented approaches, the CNN trained on normalized sensor data achieved the highest recorded test accuracy of **92.87%**.

The experiments show that sensor preprocessing and feature representation have an important influence on classification performance. The project establishes a foundation for future development of real-time human activity recognition systems.

## 11. References

1. UCI Machine Learning Repository — Human Activity Recognition Using Smartphones Dataset.  
   https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones

2. Scikit-learn Documentation.  
   https://scikit-learn.org/stable/

3. TensorFlow Documentation.  
   https://www.tensorflow.org/

4. NumPy Documentation.  
   https://numpy.org/doc/

5. Pandas Documentation.  
   https://pandas.pydata.org/docs/
