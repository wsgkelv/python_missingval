# Handling Missing Values in Python

### Using Forward Fill • Backward Fill • Interpolation • Mean Fill

## Overview

This work demonstrates how to handle missing values in a small sensor dataset (`sensor_log.csv`) using Python and pandas.  
The dataset contains readings of **temperature**, **humidity**, and **voltage**, but some values were not recorded. Missing values can affect analysis and model performance, so it is important to detect and handle them properly.

This tutorial explains **four (4) different methods** of handling missing data and compares their advantages.

---

## Learning Objectives

By the end of this work, I am able to:

- Identify missing values in a dataset.
- Summarize the number of missing values per column.
- Understand why missing values are a challenge in data analysis.
- Use pandas to **detect**, **handle**, and **fill** missing values.
- Apply **four imputation methods**:
  - Forward Fill (`ffill`)
  - Backward Fill (`bfill`)
  - Interpolation (time-series)
  - Mean Fill
- Compare results and observe how summary statistics change after cleaning.

---

## Files in This Project

| File                           | Description                                   |
| ------------------------------ | --------------------------------------------- |
| `sensor_log.csv`               | Original dataset with missing values          |
| `missing_value_cleaning.ipynb` | Main Jupyter notebook (all code and analysis) |
| `forward_fill.csv`             | Result after forward fill                     |
| `backward_fill.csv`            | Result after backward fill                    |
| `interpolated.csv`             | Result after interpolation                    |
| `mean_fill.csv`                | Result after mean imputation                  |
| `README.md`                    | This report and explanation                   |

---

## 🧪 Step-by-Step Process

### ✔ Step 1 — Load the Dataset

```python
import pandas as pd
df = pd.read_csv("sensor_log.csv")
df.head()
```

### ✔ Step 2 — Check for Missing Values

```python
df.isnull().sum()
```

---

## 🛠 Methods Used to Handle Missing Values

| Method            | Code                        | Best For                      |
| ----------------- | --------------------------- | ----------------------------- |
| **Forward Fill**  | `df.fillna(method='ffill')` | Slow changes over time        |
| **Backward Fill** | `df.fillna(method='bfill')` | Future value is reliable      |
| **Interpolation** | `df.interpolate()`          | Time-series or gradual change |
| **Mean Fill**     | `df.fillna(df.mean())`      | Stable numeric datasets       |

---

### 🔹 Forward Fill (uses previous value)

```python
df_forward_fill = df.fillna(method='ffill')
```

### 🔹 Backward Fill (uses next value)

```python
df_back_fill = df.fillna(method='bfill')
```

### 🔹 Interpolation (best method for this dataset)

```python
df_interpolate = df.interpolate()
```

### 🔹 Mean Fill (uses average of column)

```python
df_mean_fill = df.fillna(df.mean(numeric_only=True))
```

---

## Summary Statistics (After Cleaning)

To compute min, max, mean, std, etc.:

```python
df_interpolate.describe()
```

---

## Conclusion

| Method                   | Recommended When             |
| ------------------------ | ---------------------------- |
| Forward Fill             | Sensor values are stable     |
| Backward Fill            | Future readings are correct  |
| **Interpolation (Best)** | Time-series / gradual change |
| Mean Fill                | Simple numeric filling       |

**I concluded that Interpolation is the most suitable method** for this sensor dataset because it maintains data consistency and follows the natural trend of real-time readings.

---

## Student Details

**Name:** Quist Kelvin Kobla Selorm  
**Student ID:** PUIT/22210092
