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

# Datetime Conversion (handles errors gracefully)
df["Date"] = pd.to_datetime(df["Date"], errors="coerce")

# Drop records missing critical identifiers
df = df.dropna(subset=["Customer_ID"])

# Global Mean / Median Imputation
df["Price"] = df["Price"].fillna(df["Price"].median())

# Category-Based Conditional Imputation
df["Price"] = df.groupby("Category")["Price"].transform(
    lambda x: x.fillna(x.median())
)
# Multi-condition Boolean Filtering using .loc[]
high_value = df.loc[
    (df["Spend"] > 150) & (df["Items"] > 3) & (df["Rating"] >= 4.0)
]

# Filtering using list matching (.isin)
top_categories = df[df["Category"].isin(["Electronics", "Fashion"])]

import numpy as np

# Binary Categorization with np.where
df["Spend_Category"] = np.where(df["Spend"] > 200, "High", "Standard")

# Rename ambiguous column headers
df = df.rename(columns={"Old_Name": "new_name", "Raw_Header": "clean_header"})
