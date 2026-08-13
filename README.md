# Mushroom Classification using KNN

A machine learning project that classifies mushrooms as **edible or poisonous** using the **K-Nearest Neighbors (KNN)** algorithm.

## Dataset

* 8,124 observations
* 23 columns
* 22 categorical features
* Target: `class`

  * `e` → Edible
  * `p` → Poisonous

## Workflow

```text
Raw Data
   ↓
EDA
   ↓
Data Cleaning
   ↓
One-Hot Encoding
   ↓
Train/Test Split
   ↓
KNN + Cross-Validation
   ↓
Evaluation
```

### Data Cleaning

* No duplicate rows found
* `?` values in `stalk-root` were treated as `unknown`
* `veil-type` was removed because it had only one unique value
* Rare categories were retained
* No numerical outlier removal was applied because the dataset contains categorical features

### Preprocessing

Categorical features were **One-Hot Encoded** because KNN relies on distance and arbitrary numerical labels would create a false ordering between categories.

Standard scaling was not required because the encoded features are already `0–1`.

## Model

**Algorithm:** K-Nearest Neighbors
**Best `k`:** 1
**Selection method:** 5-fold cross-validation

## Results

| Metric    |    Score |
| --------- | -------: |
| Accuracy  | **100%** |
| Precision | **100%** |
| Recall    | **100%** |
| F1-score  | **100%** |

Confusion Matrix:

```text
[[842   0]
 [  0 783]]
```

The model made **0 false-negative predictions**, meaning no poisonous mushroom in the test set was classified as edible.

For comparison, a majority-class baseline achieved **51.82% accuracy**.

## Key Takeaway

This project demonstrates an end-to-end classification workflow, from EDA and data cleaning to preprocessing, KNN model selection, and evaluation.

The perfect score is specific to this dataset and should not be interpreted as guaranteed performance on real-world mushroom classification.

## Project Structure

```text
mushroom-classification-knn/
├── data/
├── eda.ipynb
├── knn_model.ipynb
├── important.md
├── decisions.md
├── result.md
├── requirements.txt
├── README.md
└── .gitignore
```

## Run Locally

```bash
python -m venv .venv
pip install -r requirements.txt
```

Open `eda.ipynb` and `knn_model.ipynb` in Jupyter/VS Code and run the notebooks.
