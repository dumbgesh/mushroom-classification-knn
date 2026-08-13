# Important Notes

## EDA & Data Cleaning

- A feature that never changes cannot help KNN distinguish between classes. In our dataset, `veil-type` has only one unique value, so we remove it.
- Missing data does not always appear as `NaN`. Sometimes it is represented by a placeholder. In our dataset, `?` appears in `stalk-root` and represents an unknown/missing value.
- We found no duplicate rows.
- We found no `NaN` values.
- Rare categorical values were kept because rare does not automatically mean incorrect.
- There are no numerical features in the original dataset, so applying IQR or another numerical outlier-removal technique is not appropriate here.

## KNN & Preprocessing

### Encoding categorical data

KNN calculates distances between observations. Therefore, categorical values cannot be given arbitrary numerical labels because that would create a false ordering between categories.

We use **One-Hot Encoding** for the features.

Each encoded feature is either `0` or `1`.

### Scaling

Do not scale just because "KNN requires scaling."

Scaling is important when numerical features have meaningfully different ranges. In our case, after one-hot encoding, all feature values are already on the same `0–1` scale.

Therefore, we do **not** use `StandardScaler`.

### Target encoding

The target contains:

- `e` → edible
- `p` → poisonous

We encode the target as:

- `e` → `0`
- `p` → `1`

This is appropriate because the target labels are not used to calculate distances.

## Evaluation

For this problem, accuracy alone is not enough conceptually. A particularly important error is:

**Poisonous → predicted as edible**

This is a false negative for the poisonous class and is the most dangerous type of error in this application.
