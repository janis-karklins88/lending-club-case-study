# Lending Club Loan Analysis

This project analyzes Lending Club loans from 2018 Q2. The work covers data inspection, cleaning, exploratory data analysis, non-performing loan analysis, and a simple predictive model for identifying non-performing loans.

## Objectives

1. Create a chart showing issued loans by issue month and loan type (`title`).
2. Choose three loan types and describe their borrower profile and portfolio characteristics.
3. Analyze variables that may help identify non-performing loans.
4. Build a model to predict non-performing loans and describe model quality.

For this project, a loan is treated as non-performing when `loan_status` is one of:

- `Late (16-30 days)`
- `Late (31-120 days)`
- `Default`
- `Charged Off`

## Project Structure

```text
data/
  raw/                         Raw Lending Club files
  processed/                   Cleaned dataset used by later notebooks
notebooks/
  01_Data_Inspection.ipynb     Initial data inspection and data-quality checks
  02_Data_Cleaning.ipynb       Type conversion, feature creation, and cleaned export
  03_EDA.ipynb                 Loan issue trends and loan-type profile analysis
  04_NPL_Analysis.ipynb        Non-performing loan analysis and useful variables
  05_Modeling.ipynb            Logistic Regression model for NPL prediction
outputs/                       Optional exported charts or outputs
```

Data files are ignored by git. To reproduce the full workflow, place the raw Lending Club files in `data/raw/` and run the notebooks in order.

## Setup

Recommended Python version: `3.11+`. The project was developed with Python `3.14.2`.

Create and activate a virtual environment, then install the pinned dependencies:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

If using macOS or Linux, activate the environment with:

```bash
source .venv/bin/activate
```

## Data Setup

The raw data files are not included in this repository because data files are ignored by git. Before running the notebooks, create the data folders and place the Lending Club CSV file here:

```text
data/raw/LoanStats_2018Q2.csv
```

From inside the `notebooks/` folder, the notebooks read the raw file using this relative path:

```text
../data/raw/LoanStats_2018Q2.csv
```

Notebook `02_Data_Cleaning.ipynb` creates the cleaned file used by later notebooks:

```text
data/processed/loan_2018q2_clean.csv
```

## Notebook Order

Run the notebooks in this order:

1. `01_Data_Inspection.ipynb`
2. `02_Data_Cleaning.ipynb`
3. `03_EDA.ipynb`
4. `04_NPL_Analysis.ipynb`
5. `05_Modeling.ipynb`

For a fresh run, execute all cells in each notebook before moving to the next notebook. Notebooks `03_EDA.ipynb`, `04_NPL_Analysis.ipynb`, and `05_Modeling.ipynb` depend on the cleaned CSV produced by notebook `02_Data_Cleaning.ipynb`.

## Analysis Summary

The EDA notebook analyzes issued loans by month and loan title, then focuses on three loan types: debt consolidation, credit card refinancing, and home improvement. It compares borrower characteristics such as income, employment length, home ownership, state distribution, debt-to-income ratio, and affordability measures.

The NPL analysis creates a target based on loan status and compares performing versus non-performing loans. Stronger indicators include lender risk variables such as grade, sub-grade, and interest rate, along with affordability measures such as loan-to-income and installment-to-income percentage. Other variables, such as income, employment length, delinquencies, verification status, purpose, and term, provide additional but weaker signal.

The modeling notebook trains a Logistic Regression model with preprocessing for numeric and categorical variables. The target is highly imbalanced, so the model is evaluated using precision, recall, F1-score, ROC AUC, Average Precision, and the confusion matrix rather than accuracy alone.
