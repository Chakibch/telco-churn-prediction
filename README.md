# Telco Customer Churn Prediction

Predicting which telecom customers are likely to leave, and choosing a decision threshold from an illustrative business cost so that retention offers reach the right customers.

## Summary

- **Data:** IBM's *Telco Customer Churn* sample dataset: 7,043 customers, 20 features, about 26.5% churn.
- **Approach:** cleaning and EDA, stratified 80/20 split, scikit-learn pipelines (scaling and one-hot encoding fitted on training data only), 5-fold stratified cross-validation to compare four models, cost-based threshold chosen from out-of-fold predictions, and one final evaluation on the held-out test set.
- **Final model:** Gradient Boosting (400 depth-1 trees), threshold 0.10.

| Model (tuned, 5-fold CV on the training set) | ROC-AUC |
|---|---:|
| Gradient Boosting | 0.847 |
| Logistic Regression | 0.842 |
| Random Forest | 0.841 |
| Decision Tree | 0.827 |

**Test set (1,409 customers), threshold 0.10:** ROC-AUC 0.862, recall 0.95, precision 0.42, 60% of customers flagged.

Under the assumed costs (a missed churner costs 600, an unnecessary offer costs 50), the model's total cost is about 29% lower than contacting every customer. Those costs are assumptions, and the notebook shows how the saving shrinks if retention offers work less often than assumed.

## Repository structure

```
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── telco_churn_analysis.ipynb
└── data/
    └── README.md          # how to get the dataset (the CSV itself is not included)
```

## How to run

1. Create and activate a virtual environment, then install the dependencies:
   ```
   python -m venv .venv
   .venv\Scripts\activate          # Windows (on macOS/Linux: source .venv/bin/activate)
   pip install -r requirements.txt
   ```
2. Download the dataset as described in [`data/README.md`](data/README.md) and place it in `data/`.
3. Open `notebooks/telco_churn_analysis.ipynb` (keep `notebooks/` as the working folder) and run all cells. Everything uses `random_state=19`, and a full run takes several minutes because of the grid searches.

### Pinning versions

To record the exact versions you used, run this in your environment and copy the output into `requirements.txt`:

```
python -c "import pandas, numpy, sklearn, matplotlib, seaborn; print(f'pandas=={pandas.__version__}\nnumpy=={numpy.__version__}\nscikit-learn=={sklearn.__version__}\nmatplotlib=={matplotlib.__version__}\nseaborn=={seaborn.__version__}')"
```

## Limitations

- The cost figures are illustrative assumptions, not real business data.
- The results are associations, not causal effects.
- The test set is small, so the test figures are uncertain; the notebook reports bootstrap intervals.
- The differences between the tuned models are small, and a simple Logistic Regression is almost as good as the final model.
- Single data snapshot with no time dimension; a real deployment would need validation on later data.

## Data source

IBM sample dataset *Telco Customer Churn*, available on Kaggle: https://www.kaggle.com/datasets/blastchar/telco-customer-churn
