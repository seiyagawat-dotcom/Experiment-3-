# ECE2112---EXPERIMENT-3-PANDAS
# Seiya A. Gawat | 2ECE-A

---

## 📋 Table of Contents
- [Overview](#-overview)
- [Pandas Operations Summary](#-pandas-operations-summary)
- [Problem Specifications & Solutions](#-problem-specifications--solutions)
  - [A. Positional and Label-Based Slicing](#a-positional-and-label-based-slicing)
  - [B. Model Lookup](#b-model-lookup)
  - [C. Multi-Model Subsetting](#c-multi-model-subsetting)
- [Project File Structure](#-project-file-structure)
- [Prerequisites & Requirements](#-prerequisites--requirements)
- [How to Run](#-how-to-run)
  - [Using Jupyter Notebook](#using-jupyter-notebook)
  - [Using Terminal / Command Prompt](#using-terminal--command-prompt)
- [Edge Cases & Key Considerations](#-edge-cases--key-considerations)

---

## 📌 Overview

This project contains Python solutions for **Experiment 3: Python Data Analysis (Pandas)**. The task involves loading, exploring, indexing, and slicing vehicle performance data from `cars.csv`. Key concepts demonstrated include:
* Loading external CSV files into Pandas DataFrames
* Extracting structural metadata (`.shape`, `.columns`)
* Integer positional indexing (`.iloc[]`) vs. label-based indexing (`.loc[]`)
* Conditional row filtering using Boolean masking
* Vectorized membership operations using `.isin()`

---

## ⚙️ Pandas Operations Summary

| Operation / Method | Syntax Example | Return Type | Key Logic |
| :--- | :--- | :--- | :--- |
| `pd.read_csv()` | `pd.read_csv('cars.csv')` | `DataFrame` | Imports CSV data into a Pandas DataFrame structure |
| `.iloc[]` | `cars.iloc[5:10]` | `DataFrame` | Selects rows/columns by zero-based integer index locations |
| `.loc[]` / Boolean Filtering | `cars.loc[cars['Model'] == 'Toyota Corolla']` | `DataFrame` | Filters rows matching conditional logic and selects columns by label |
| `.isin()` | `cars['Model'].isin(list)` | `Series` (bool) | Checks whether column values match any element in a list for multi-row filtering |

---

## 💻 Problem Specifications & Solutions

### A. Positional and Label-Based Slicing
**Requirement:** Determine dataset dimensions and column names. Extract rows 6 through 10 using positional indexing, then display only the `Model`, `mpg`, `cyl`, `hp`, and `gear` columns.

```python
import pandas as pd

# Load dataset
cars = pd.read_csv('cars.csv')

# a. Metadata inspection
print("Dataset Shape:", cars.shape)
print("Column Names:", cars.columns.tolist())

# b. Extract rows 6 through 10 using iloc (zero-based index 5 to 9)
cars_6_to_10 = cars.iloc

# c. Subset specific columns using column labels
subset_a = cars_6_to_10[['Model', 'mpg', 'cyl', 'hp', 'gear']]
subset_a
```

---

### B. Model Lookup
**Requirement:** Retrieve the complete attribute record for `'Toyota Corolla'`. Extract specific performance attributes (`Model`, `mpg`, `hp`, `wt`) for `'Pontiac Firebird'`.

```python
# a. Full row output for 'Toyota Corolla'
toyota_df = cars[cars['Model'] == 'Toyota Corolla']
print("Toyota Corolla Full Record:")
display(toyota_df)

# b. Attribute subset for 'Pontiac Firebird'
pontiac_df = cars.loc[
    cars['Model'] == 'Pontiac Firebird', ['Model', 'mpg', 'hp', 'wt']
]
print("\nPontiac Firebird Subset:")
display(pontiac_df)
```

---

### C. Multi-Model Subsetting
**Requirement:** Select vehicle records for `'Datsun 710'`, `'Lotus Europa'`, and `'Ferrari Dino'` displaying columns `Model`, `mpg`, `cyl`, `hp`, and `gear`. Verify that the resulting DataFrame has dimensions `(3, 5)`.

```python
# Target vehicle list
target_models = ['Datsun 710', 'Lotus Europa', 'Ferrari Dino']

# Subsetting using .isin() and label indexing
selected_cars = cars.loc[
    cars['Model'].isin(target_models), ['Model', 'mpg', 'cyl', 'hp', 'gear']
]

# Display result and verify shape
display(selected_cars)
print("Resulting DataFrame Shape:", selected_cars.shape)  # Output: (3, 5)
```

---

## 📁 Project File Structure

```text
.
├── cars.csv                  # Dataset file containing vehicle performance data
├── Experiment3_Gawat.ipynb   # Main Jupyter Notebook containing executed solutions
└── README.md                 # Project documentation file
```

---

## 🛠️ Prerequisites & Requirements

* **Python 3.8+**
* **Pandas** (`pip install pandas`)
* **Jupyter Notebook / Anaconda**

---

## 🚀 How to Run

### Using Jupyter Notebook
1. Ensure `cars.csv` and `Experiment3_Gawat.ipynb` are in the **same directory**.
2. Open terminal/command prompt, navigate to the folder, and launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
3. Open `Experiment3_Gawat.ipynb`.
4. Run all cells sequentially (**Cell** -> **Run All**).

### Using Terminal / Command Prompt
1. Open a terminal in the project folder.
2. Execute the notebook via `nbconvert` or run your standalone Python script:
   ```bash
   python -m jupyter nbconvert --to notebook --execute Experiment3_Gawat.ipynb
   ```

---

## 🛡️ Edge Cases & Key Considerations Handled

* **Zero-based Index Alignment**: In Python, "Row 6 through 10" maps to indices `5` through `9`. Utilizing `iloc[5:10]` correctly includes index 9 while excluding index 10.
* **`FileNotFoundError` Handling**: Ensured relative path loading (`pd.read_csv('cars.csv')`) works seamlessly by keeping `cars.csv` in the notebook root working directory.
* **Data Immutability**: All indexing and subsetting operations generate new DataFrame views/copies, ensuring original raw data in `cars` remains unmodified throughout execution.
