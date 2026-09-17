# 📍 Week 1 Prep: Environment, Wrangling & Feature Engineering

**Session Date:** September 14  
**Difficulty Level:** Medium  
**Required Tools:** Google Colab, Python, Pandas, NumPy  

---

## 📖 Mandatory Pre-Readings (100% Free)

Please complete the following Kaggle Learn modules before attending the live session:

1. 🎓 **[Kaggle Learn: Python](https://www.kaggle.com/learn/python)**  
   *Focus Areas:* Variables, Functions, Booleans, Conditionals  

2. 🎓 **[Kaggle Learn: Pandas](https://www.kaggle.com/learn/pandas)**  
   *Focus Areas:* Indexing, Selecting & Assigning, Summary Functions & Maps  

---

## 💡 Key Functions & Operations to Review

During our live workshop, you will work in small teams to clean raw e-commerce data and build customer features. Make sure you understand how these core functions work before arriving:

* **Data Auditing:** `df.info()`, `df.isnull().sum()`
* **Date Parsing:** `pd.to_datetime()`
* **Conditional Imputation:** `df.groupby('Category')['Price'].transform(...)`
* **Logical Filtering:** `df.loc[(df['Spend'] > 150) & (df['Rating'] >= 4.0)]`
* **Feature Creation:** `np.where()` or `.apply()`
* **Header Renaming:** `df.rename(columns={...})`

---

## 📂 Session Structure & Deliverables

* **Preparation (Before Class):** Complete the readings above and familiarize yourself with the syntax.
* **Live Session (90 Mins):**
  * **15 Mins:** Briefing & live Q&A
  * **50 Mins:** Live Group Coding Challenge (*Tier 1: Standard* or *Tier 2: Advanced*)
  * **25 Mins:** Rapid presentations, code audit, and pushing your notebook to GitHub

---

## 🔒 Live Task Prompt

*The live problem statement, dataset challenges, and assignment tiers will be unlocked at the start of the workshop!*
