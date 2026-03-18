# SQL-Exercises-ROUND-1
sql advanced · causes of death · vol 1 &amp; 2
[SQL_EXERCISES_README.md](https://github.com/user-attachments/files/26075534/SQL_EXERCISES_README.md)
# 🌍 SQL Practice — Causes of Death Dataset

> *"Real data. Real stories. Real SQL."*

---

## 📌 Overview

A progressive SQL exercise series built on real global health data from Our World in Data. Covers everything from basic filtering to advanced window functions — the exact skills tested in data analyst interviews.

All exercises use a single SQLite database built from the **Causes of Death Worldwide** dataset — the same dataset used in my first portfolio project.

---

## 🗂️ Exercise Sets

### 🔥 Warm-Up Sheet (9 exercises)
Focused review of the three most commonly misunderstood SQL concepts.

| Section | Exercises | Concepts |
|---|---|---|
| HAVING | EX 01–03 | WHERE vs HAVING, multiple conditions |
| JOINs | EX 04–06 | INNER JOIN, LEFT JOIN, CTEs + JOIN |
| Subqueries | EX 07–09 | WHERE, HAVING, nested subqueries |

---

### 📊 Main Exercise Sheet (12 exercises)
Full SQL skill progression from SELECT to window functions.

| Section | Exercises | Concepts |
|---|---|---|
| SELECT & Filter | EX 01–02 | WHERE, BETWEEN, LIKE |
| GROUP BY + HAVING | EX 03–04 | SUM, COUNT, HAVING |
| CTEs | EX 05–06 | Single CTE, double CTE + JOIN |
| Subqueries | EX 07–08 | In WHERE and HAVING |
| Window Functions ⭐ | EX 09–11 | PARTITION BY, RANK, LAG |
| Boss Level | EX 12 | Full pipeline |

---

### 🚀 Advanced Sheet (22 exercises)
The hard stuff — patterns that appear in every real analyst interview.

| Section | Exercises | Concepts |
|---|---|---|
| Subqueries | EX 01–06 | Correlated, nested, self-JOIN, NULLIF |
| CTEs | EX 07–12 | 3 CTEs, UNION ALL, percentages, success analysis |
| Window Functions ⭐ | EX 13–19 | Running totals, DENSE_RANK, LEAD, moving averages, ROW_NUMBER, PERCENT_RANK |
| Boss Levels | EX 20–22 | Full pipelines combining everything |

---

## 🗃️ Dataset

**Source:** Our World in Data — Annual Number of Deaths by Cause
**Format:** SQLite database (`causes_of_death.db`)
**Size:** 8,254 rows × 34 columns
**Coverage:** 200+ countries and regions, 1990–2019

**Key columns:**
- `Entity` — country or region name
- `Code` — country code (use `Code NOT LIKE 'OWID%'` to filter real countries only)
- `Year` — year of data
- 31 cause-of-death columns including Cardiovascular diseases, Malaria, HIV/AIDS, Tuberculosis, Neoplasms, and more

---

## ⚙️ Setup

```python
import sqlite3
import pandas as pd

# Load and clean the dataset
df = pd.read_csv('annual-number-of-deaths-by-cause.csv')

# Clean column names
df.columns = df.columns.str.replace('Deaths - ', '', regex=False)
df.columns = df.columns.str.replace(' - Sex: Both - Age: All Ages (Number)', '', regex=False)
df.columns = df.columns.str.strip()

# Drop columns with too many missing values
df = df.drop(columns=['Number of executions (Amnesty International)', 'Terrorism (deaths)'])

# Fill missing death counts with 0
death_columns = df.columns[3:]
df[death_columns] = df[death_columns].fillna(0)

# Load to SQLite
conn = sqlite3.connect('causes_of_death.db')
df.to_sql('causes_of_death', conn, if_exists='replace', index=False)

print(f"Ready! {pd.read_sql('SELECT COUNT(*) as total FROM causes_of_death', conn)['total'][0]} rows loaded.")
```

---

## ⚠️ Important Notes

**Column names with spaces need double quotes:**
```sql
✅ "Cardiovascular diseases"
❌  Cardiovascular diseases
```

**Always filter out regional aggregates:**
```sql
WHERE Code NOT LIKE 'OWID%'
```
Without this, results include World, Africa, Sub-Saharan Africa etc. which inflate numbers.

---

## 💡 Key Concepts Covered

`SELECT` `WHERE` `BETWEEN` `LIKE` `GROUP BY` `HAVING` `ORDER BY` `LIMIT`
`JOIN` `LEFT JOIN` `Self-JOIN` `UNION ALL`
`WITH (CTE)` `Multiple CTEs` `Nested CTEs`
`Subquery in WHERE` `Subquery in SELECT` `Subquery in HAVING` `Correlated Subquery`
`AVG() OVER` `SUM() OVER` `RANK()` `DENSE_RANK()` `ROW_NUMBER()` `PERCENT_RANK()`
`LAG()` `LEAD()` `ROWS BETWEEN` `PARTITION BY` `NULLIF()`

---

## 🧠 The SQL Thinking Framework

Before writing any query, ask:

1. **What do I want to see?** → SELECT
2. **From which table?** → FROM
3. **Any filters?** → WHERE
4. **Group or aggregate?** → GROUP BY + HAVING
5. **Sort?** → ORDER BY + LIMIT

> *"Think first, query second."*

---

## 👩‍💻 About

Built by **Fatima Zahra** — a self-taught data analyst from Morocco 🇲🇦

These exercises are part of a structured self-learning path combining real datasets, deliberate practice, and deep understanding over syntax memorization.

[![GitHub](https://img.shields.io/badge/GitHub-fatima--zahra20-black?logo=github)](https://github.com/fatima-zahra20)
