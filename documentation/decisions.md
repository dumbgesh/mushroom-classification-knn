# Decisions

## Handling `?` in `stalk-root`

The dataset contains 2,480 `?` values in `stalk-root`, about 30.5% of the dataset.

| Option | Problem |
|---|---|
| Delete `?` rows | Lose ~30.5% of the data |
| Mode imputation | Artificially creates a large number of one category |
| Random/other imputation | Invents information |
| Treat `?` as `unknown` | Preserves observations without inventing a stalk-root value |

### Decision

Keep the rows and treat `?` as an explicit `unknown` category.

```python
df['stalk-root'] = df['stalk-root'].replace('?', 'unknown')
```

---

## Removing `veil-type`

`veil-type` contains only one unique value across all 8,124 observations.

A constant feature provides no variation and therefore cannot help distinguish the target classes.

### Decision

Remove `veil-type`.

```python
df = df.drop('veil-type', axis=1)
```

---

## Cleaning decisions

| Issue | Finding | Decision |
|---|---|---|
| Missing `NaN` | None found | No action |
| Duplicates | None found | No action |
| Constant feature | `veil-type` | Remove |
| Placeholder missing value | `?` in `stalk-root` | Replace with `unknown` |
| Rare categories | Present | Keep |
| Numerical outliers | No numerical features | No IQR/outlier removal |

---

## Encoding decision

We use **One-Hot Encoding** instead of Label Encoding for the input features.

Label Encoding would assign arbitrary numbers to categories. KNN would then treat those numbers as distances and imply an ordered relationship between categories that does not actually exist.

One-Hot Encoding avoids this artificial relationship.

---

## Train/Test Split

We split the processed dataset into:

- 80% training data
- 20% test data

We use `stratify=y` so the edible/poisonous class proportions remain approximately consistent between training and test sets.

The test set is kept separate for final evaluation.

---

## Scaling decision

KNN is distance-based, so feature scale can matter.

However, our input features are categorical and are converted through One-Hot Encoding into `0` and `1`.

### Decision

Do not use `StandardScaler`.

---

## KNN Hyperparameter Decision

We initially tested `k` from 1 to 20 as an exploratory experiment. Values `k=1–9` achieved 1.0000 accuracy, while values from 10 onward produced a very small drop.

We then used **5-fold cross-validation on the training data** to select `k` rather than choosing it from the test set.

### Final decision

`k = 1`

Best mean cross-validation accuracy: **100%**.
