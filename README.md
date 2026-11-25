# Activity Recognition System (ARS)

A machine-learning project that classifies six human activities from smartphone inertial-sensor data using the UCI Human Activity Recognition (HAR) Using Smartphones dataset.

## Objective

Recognize the activity represented by a short window of smartphone motion data. The experiments compare manually calculated statistical features, the dataset-provided engineered features, and raw time-series sensor signals.

## Activities

1. Walking
2. Walking Upstairs
3. Walking Downstairs
4. Sitting
5. Standing
6. Laying

## Dataset

**UCI Human Activity Recognition Using Smartphones**

- 30 volunteers and 6 activity classes.
- 10,299 labelled windows in total.
- Each window contains 128 readings sampled at 50 Hz (2.56 seconds).
- Official split: 7,352 training windows and 2,947 test windows.
- The official training and test sets contain different participants (21 and 9 respectively).

The notebook downloads the dataset from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones) if it is not already present. The raw dataset is not stored in this repository.

## Implemented experiments

| Experiment | Input representation | Recorded test accuracy |
|---|---|---:|
| Random Forest | 28 custom statistical features | 72.51% |
| Random Forest | 561 UCI-provided engineered features | 92.60% |
| 1D CNN | 9-channel raw sensor windows | 92.43% |
| 1D CNN | 9-channel normalized sensor windows | 92.87% |

The CNN input contains nine channels: body acceleration (X/Y/Z), body gyroscope (X/Y/Z), and total acceleration (X/Y/Z). Each window has shape `(128, 9)`. The CNN validation split is participant-wise and is created from the official training set. The official test participants remain separate.

These are the results recorded in the notebook outputs. Re-running the experiments may produce slightly different results depending on the runtime, library versions, and training conditions.

## Repository contents

- `Explore_data.ipynb`: exploratory notebook.
- `notebooks/ARS_Cleaned_Analysis_and_Conclusions (1).ipynb`: main experiment notebook.
- `reports/eda_report.md`: exploratory data analysis report.
- `reports/random_forest.md`: Random Forest experiment report.
- `docs/LLD.md`: low-level design.

The Random Forest and CNN models are trained in notebook memory. The current repository does not contain exported, reusable model files. The `src/` and `models/` directories are placeholders.

## Run the project

### Google Colab (recommended)

1. Open [Google Colab](https://colab.research.google.com/).
2. Open or upload `notebooks/ARS_Cleaned_Analysis_and_Conclusions (1).ipynb`.
3. Select **Runtime → Run all**.
4. The notebook downloads and extracts the UCI HAR dataset into `/content/ars_data` if it is not already available.
5. Allow the EDA, Random Forest experiments, CNN training, and evaluation cells to complete.

The notebook trains several models, so execution time depends on the runtime hardware. A GPU runtime can accelerate CNN training.

### Local execution

The notebook currently sets `DATA_DIR` to `/content/ars_data`, which is a Google Colab path. For local execution, change `DATA_DIR` in the setup cell to a writable local directory before running the notebook.

Create and activate a virtual environment, install the dependencies, and launch Jupyter:

```bash
python -m venv .venv

# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate

python -m pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook
```

Run the main notebook from top to bottom.


## Current limitations and next steps

- Trained models are not yet exported as reusable model files.
- The project is notebook-based; it does not currently include a deployed application or real-time smartphone integration.
- Further work can investigate model tuning, class-specific errors (particularly Sitting vs Standing), model export, and a prediction interface for new sensor windows.

## References

- [UCI HAR Dataset](https://archive.ics.uci.edu/dataset/240/human+activity+recognition+using+smartphones)
- [Scikit-learn documentation](https://scikit-learn.org/stable/)
- [TensorFlow/Keras documentation](https://www.tensorflow.org/)
