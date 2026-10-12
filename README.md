# Credit Score Classification

Predicting whether a client's credit score is **Good**, **Standard** or **Poor** from their financial and personal information, a classic risk-assessment task in banking.

*EDHEC Business School group project, by Anaïs Ferreira, Mithia Ratsimbarison and Laura Brulé.*

## Approach

1. **Data cleaning**: removal of identifiers, conversion of `Credit_History_Age` ("22 Years and 5 Months") into months, removal of parasite characters (`_`, `%`) in numeric columns, invalid ages set to missing
2. **Exploratory analysis**: distribution of every numeric variable by credit class, and credit-score mix by category (occupation, payment behaviour, credit mix…)
3. **Modelling**: one-hot encoding, most-frequent imputation, standardisation, multinomial **logistic regression**
4. **Evaluation**: log-loss (main metric, since a credit score is a risk probability), precision, recall and F1 per class
5. **Interpretation**: variable importance from the model coefficients

## Results (validation set, 20,000 clients)

| Metric | Value |
|---|---|
| Accuracy | 0.733 |
| Macro F1-score | 0.709 |
| Log-loss | 0.715 |

| Class | Precision | Recall | F1 |
|---|---|---|---|
| Good | 0.591 | 0.636 | 0.613 |
| Standard | 0.762 | 0.775 | 0.768 |
| Poor | 0.776 | 0.716 | 0.745 |

**Outstanding debt** and **delay from due date** are the most influential variables, followed by credit mix and credit history age.

## Next steps

- Encode `Type_of_Loan` as one binary column per loan type (it currently lists several loans in a single string)
- Cap corrupted extreme values (e.g. more than 1,000 bank accounts)
- Split train and validation **by customer**, since each customer appears once per month
- Compare with a baseline and with tree-based models (Random Forest, LightGBM)

## Run it

Data: [Credit score classification](https://www.kaggle.com/datasets/parisrohan/credit-score-classification) (Kaggle). Download `train.csv` and `test.csv` into a `data/` folder (not included in this repository).

```bash
pip install -r requirements.txt
jupyter notebook credit_scoring.ipynb
```

---

More projects on my portfolio: [anaisferreira.github.io/Personal-website](https://anaisferreira.github.io/Personal-website/)

