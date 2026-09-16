# 🐼 Pandas Quick-Reference Cheatsheet

A concise reference for the key Pandas operations used in our weekly data science workshops.

---

## 1. Data Inspection & Auditing

```python
import pandas as pd

# Load dataset
df = pd.read_csv("data.csv")

# View first 5 rows
df.head(5)

# Check schema, column data types, and non-null counts
df.info()

# Calculate total missing values per column
df.isnull().sum()

# Summary statistics for numerical columns
df.describe()
