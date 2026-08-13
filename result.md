# Results

## Baseline KNN

We initially trained KNN with:

```python
KNeighborsClassifier(n_neighbors=5)
```

The model achieved **100% test accuracy**.

Confusion matrix:

```text
[[842   0]
 [  0 783]]
```

This means:

- 842 edible mushrooms were correctly classified as edible.
- 783 poisonous mushrooms were correctly classified as poisonous.
- 0 edible mushrooms were classified as poisonous.
- 0 poisonous mushrooms were classified as edible.

The last error is particularly important because predicting a poisonous mushroom as edible is the most dangerous error for this problem.

---

## Testing Different Values of `k`

We initially tested `k` from 1 to 20:

```text
k=1:  1.0000
k=2:  1.0000
k=3:  1.0000
k=4:  1.0000
k=5:  1.0000
k=6:  1.0000
k=7:  1.0000
k=8:  1.0000
k=9:  1.0000
k=10: 0.9988
k=11: 0.9988
k=12: 0.9982
k=13: 0.9982
k=14: 0.9982
k=15: 0.9982
k=16: 0.9982
k=17: 0.9988
k=18: 0.9982
k=19: 0.9982
k=20: 0.9982
```

We did not use this test-set comparison to make the final hyperparameter decision. Instead, we used cross-validation on the training data.

---

## Final KNN Model

Five-fold cross-validation selected:

```text
Best k = 1
Mean CV accuracy = 1.0000
```

The selected model was then evaluated on the held-out test set.

### Final test performance

```text
Test Accuracy: 1.0000
```

Classification report:

```text
              precision    recall  f1-score   support

           e       1.00      1.00      1.00       842
           p       1.00      1.00      1.00       783

    accuracy                           1.00      1625
   macro avg       1.00      1.00      1.00      1625
weighted avg       1.00      1.00      1.00      1625
```

Final confusion matrix:

```text
[[842   0]
 [  0 783]]
```

Therefore:

- Accuracy = **100%**
- Precision = **100%** for both classes
- Recall = **100%** for both classes
- F1-score = **100%** for both classes
- False positives = **0**
- False negatives = **0**

---

## Baseline Comparison

A majority-class baseline achieved:

```text
Accuracy = 0.5181538461538462
```

or approximately **51.82%**.

KNN improved this to **100%** on the test set.

---

## Robustness Check

To check whether the result depended only on `random_state=42`, we repeated the train/test split with five different random seeds:

```text
Seed 1:   1.0000
Seed 10:  1.0000
Seed 21:  1.0000
Seed 42:  1.0000
Seed 100: 1.0000
```

KNN achieved 100% accuracy for all five tested splits.

---

## Conclusion

The KNN classifier performed exceptionally well on this mushroom dataset.

After cleaning, One-Hot Encoding, and a stratified train/test split, five-fold cross-validation selected **k=1**. The final model achieved **100% accuracy** on the held-out test set with no false positives or false negatives.

This result is specific to this dataset and evaluation setup. It should not be interpreted as evidence that KNN will always achieve perfect performance on real-world mushroom classification problems.

### Key learning outcomes

1. Missing values can appear as placeholders such as `?`, not only as `NaN`.
2. Constant features provide no useful variation and can be removed.
3. Rare categorical values should not automatically be treated as outliers.
4. Categorical input features should not be arbitrarily label-encoded for a distance-based algorithm such as KNN.
5. One-Hot Encoding is appropriate for these nominal categorical features.
6. Scaling is not automatically required when all encoded features already share the same `0–1` scale.
7. Hyperparameters should be selected using training data/cross-validation rather than repeatedly using the test set.
8. For this application, false negatives are particularly important because classifying a poisonous mushroom as edible is the most dangerous error.
