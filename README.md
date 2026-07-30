# Model Comparison Tool for CSV Data

A fast, automated way to evaluate **8 different regression models** on your structured dataset.  
Perfect for quickly identifying which linear-style model best learns your data's patterns.

---

# What This Script Does , just the surface part!

- Takes any CSV file (with numeric features and a numeric target column)
- Splits data into:
  - **80% Training**
  - **20% Testing**
- Trains **8 regression models** simultaneously:

1. Linear Regression
2. Ridge
3. Lasso
4. ElasticNet
5. Bayesian Ridge
6. Huber Regressor
7. SGD Regressor
8. Passive Aggressive Regressor

- Compares performance using:
  - MSE
  - MAE
  - R² Score
- Automatically highlights the best performing model

---

# Data Requirements

| Requirement | Description |
|---|---|
| File format | `.csv` |
| Data type | All numeric (`float` / `int`) |
| Target column | The **LAST** column must be the target variable |
| Feature columns | All other columns are features |
| Missing values | Must be cleaned first |

> ⚠️ Important:  
> This script only works for **numeric regression problems**.  
> It will NOT work with:
> - Text data
> - Categories
> - Classification tasks

---

# How To Use With Your Own Data

## Step 1 — Prepare Your CSV

Your CSV must contain:

- Only numeric values
- Last column = target value
- Other columns = features/descriptors

---

## Step 2 — Update The File Path

Find this line:

```python
df = pd.read_csv('https://raw.githubusercontent.com/dataprofessor/data/refs/heads/master/delaney_solubility_with_descriptors.csv')
```

Replace it with your own dataset path.

### Option A — Windows Local File

```python
df = pd.read_csv('C:/Users/YourName/Downloads/your_data.csv')
```

### Option B — Mac/Linux Local File

```python
df = pd.read_csv('/Users/yourname/Downloads/your_data.csv')
```

### Option C — GitHub Raw URL

```python
df = pd.read_csv('https://raw.githubusercontent.com/yourusername/yourrepo/main/yourdata.csv')
```


## Step 3 — Run The Script

Execute all cells or run the script.

The script will, like i mentoned above :

1. Split your data
2. Train all 8 models
3. Display a comparison table
4. Recommend the best model

---

# Understanding The Results

The output table contains these metrics(Used for evaluating the best model):

| Metric | Meaning |
|---|---|
| Train_R2 | Performance on training data |
| Test_R2 | Performance on unseen data (**most important**) |
| R2_Diff | Overfitting indicator (smaller is better) |
| Train/Test MSE | Mean Squared Error (lower is better) |
| Train/Test MAE | Mean Absolute Error (lower is better) |

---

# Ideal Values (General Reference)

| Metric | Good Value |
|---|---|
| R² Score | `> 0.85` |
| MSE | `< 0.40` |
| MAE | `< 0.50` |

---

# Installation

Install dependencies:

```bash
pip install pandas scikit-learn numpy tabulate
```

Or use:

- Google Colab
- Kaggle Notebooks
- Jupyter Notebook

(No installation required there.)

---

# Example Output

```text
🏆 BEST MODEL: Ridge

• Test R² Score: 0.8723
• Test MSE: 0.3412
• Test MAE: 0.4789
```

---

# Example Dataset

The demo dataset comes from DataProfessor's GitHub repository:
`https://raw.githubusercontent.com/dataprofessor/data/refs/heads/master/delaney_solubility_with_descriptors.csv`

---



# Quesions you might ask ..

## Q1 — How do i  Change The Train/Test Split Ratio?because you want to ..

Find:

```python
x_train, x_test, y_train, y_test = train_test_split(
    x,
    y,
    test_size=0.2,
    random_state=100
)
```

Change:

```python
test_size=0.3
```

For a 70/30 split.

---

## Q2 — My Target Column Is NOT The Last Column

Replace:

```python
y = df.iloc[:, -1]
x = df.iloc[:, :-1]
```

With:

```python
y = df['your_target_column_name']
x = df.drop('your_target_column_name', axis=1)
```

---

## Q4 — Can I Save The Best Model?

Yes.

```python
import joblib

joblib.dump(model, 'best_model.pkl')
```

Load later:

```python
model = joblib.load('best_model.pkl')
```

---

## Q5 — What About Huge Datasets?

Use sampling:

```python
df = df.sample(n=10000, random_state=42)
```

---


## Q6 — Does Data Type Matter?

Yes.Like i said above 

The script requires:
- Integers
- Floats

It will fail if your dataset contains:
- Text
- Dates
- Categories

Convert them first using(which you have to learn):
- One-hot encoding
- Label encoding

---

# Troubleshooting

## Error: could not convert string to float

Your CSV contains text columns.(you did not follow the rules.)

Solution:
- Remove text columns
- Encode categories

---

## Error: Input contains NaN(maybe you don't have times to debug your csv)

Your dataset contains missing values.

Fix:

```python
df = df.dropna()
```

---

## Error: File not found

Check:
- File path
- Spelling
- Slashes

Use:
- Forward slashes `/`
- Raw strings `r'path'`

---

## Error: NameError: name 'pd' is not defined

Make sure this exists:

```python
import pandas as pd
```

---

# Summary

This script provides a **fast and automated** way to compare multiple regression models on structured CSV datasets.

Perfect for:

- Quick ML prototyping
- Learning regression
- Comparing models
- Detecting overfitting
- Evaluating dataset quality

Best suited for:

✅ Numeric regression datasets  
✅ Structured CSV files  
✅ Quick experimentation  

Not suited for:

❌ Text datasets  
❌ Classification problems  
❌ Missing-value datasets (without cleaning)

---

# Made For Quick Prototyping

Find the best linear model for your data in seconds.
