# Data

This project uses IBM's **Telco Customer Churn** sample dataset (7,043 customers, 21 columns).

The CSV is not stored in this repository. To run the notebook:

1. Download `WA_Fn-UseC_-Telco-Customer-Churn.csv` from Kaggle:
   https://www.kaggle.com/datasets/blastchar/telco-customer-churn
2. Put the file in this folder, so the path is
   `data/WA_Fn-UseC_-Telco-Customer-Churn.csv`.

The notebook reads it with `pd.read_csv("../data/WA_Fn-UseC_-Telco-Customer-Churn.csv")`,
so it must be run from the `notebooks/` folder (this is the default when you open it in Jupyter or VS Code).
