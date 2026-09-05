# 📚 Python Pandas Masterclass: Comprehensive Study Notes
**Instructor:** Tech With Tim  
**Source Video:** https://www.youtube.com/watch?v=EXIgjIBu4EU  

- [1. Introduction & Environment Setup](#1-introduction-environment-setup)
  - [Recommended IDEs](#recommended-ides)
  - [Installation & Virtual Environments](#installation-virtual-environments)
- [2. Core Data Structures: Series vs. DataFrame](#2-core-data-structures-series-vs-dataframe)
  - [1D Structure: The Series](#1d-structure-the-series)
  - [2D Structure: The DataFrame](#2d-structure-the-dataframe)
- [3. Loading Data](#3-loading-data)
  - [Visualizing `orders.csv`](#visualizing-orderscsv)
  - [The Code: Ingestion](#the-code-ingestion)
- [4. Inspecting & Understanding Data](#4-inspecting-understanding-data)
  - [Exploring the Extremes](#exploring-the-extremes)
  - [Extracting a Single Column](#extracting-a-single-column)
- [5. Filtering Data (Conditional Selection)](#5-filtering-data-conditional-selection)
  - [Single Condition Filters](#single-condition-filters)
  - [Multiple Condition Filters](#multiple-condition-filters)
- [6. Data Cleaning & Manipulation](#6-data-cleaning-manipulation)
  - [The `inplace=True` Concept](#the-inplacetrue-concept)
  - [Renaming Columns](#renaming-columns)
  - [Handling Missing/Corrupted Data](#handling-missingcorrupted-data)
- [7. Data Analysis & Aggregation](#7-data-analysis-aggregation)
  - [1. Frequency Distribution: `.valuecounts()`](#1-frequency-distribution-value_counts)
  - [2. Grouping Metrics: `.groupby()`](#2-grouping-metrics-groupby)
  - [3. Sorting Data: `.sortvalues()`](#3-sorting-data-sort_values)
- [8. Exporting Data](#8-exporting-data)

---

## 1. Introduction & Environment Setup

Pandas is the foundational open-source Python library used for data manipulation, cleaning, and analysis. It serves as a prerequisite for virtually all Data Science, Machine Learning (ML), Artificial Intelligence (AI), and Data Visualization workflows.

### Recommended IDEs
*   **VS Code / Cursor:** Excellent for general scripting and building pipelines.
*   **Jupyter Notebooks:** Highly recommended for data analysis because it allows you to run code cell-by-cell and visualize tables instantly.
*   **PyCharm:** A strong choice for large-scale enterprise projects.

### Installation & Virtual Environments
While you can install Pandas globally, best practice dictates using an isolated virtual environment to manage project dependencies. The tutorial utilizes `uv`, an extremely fast package manager.

**Terminal Commands:**
```bash
# Global Installation
pip install pandas       # Windows
pip3 install pandas      # Mac/Linux

# Virtual Environment Setup (Using 'uv')
uv init .                # Initialize a virtual environment in the current directory
uv add pandas            # Add the pandas library to this environment
uv run main.py           # Execute your script using the environment's python interpreter
```

---

## 2. Core Data Structures: Series vs. DataFrame

Before writing complex operations, you must understand how Pandas structures its data in memory.

### 1D Structure: The Series
A Series is a one-dimensional labeled array. You can think of a Series as a single, isolated column extracted from a larger table.

```text
Index | Values (Product Series)
-------------------------------
  0   | Laptop
  1   | Mouse
  2   | Keyboard
```

### 2D Structure: The DataFrame
A DataFrame is a two-dimensional labeled data structure. It is a collection of Series aligned side-by-side to form a grid of rows and columns, functioning exactly like an Excel spreadsheet or a SQL table.

```text
       | Order ID | Product  | Price | Country     |
-------|----------|----------|-------|-------------|
Row 0  | 1001     | Laptop   | 1200  | USA         |
Row 1  | 1002     | Mouse    | 25    | South Korea |
Row 2  | 1003     | Keyboard | 45    | USA         |
```

---

## 3. Loading Data

The first operational step in Pandas is ingesting external data. CSV (Comma-Separated Values) files are the industry standard for lightweight datasets.

### Visualizing `orders.csv`
Imagine your CSV file looks like this in raw text form:
```text
orderID,Customer Name,Product Category,Quantity,Price,Country
101,Alice,Laptop,1,1200,USA
102,Bob,Monitor,2,300,South Korea
103,Charlie,Mouse,1,22,Argentina
104,Diana,Keyboard,1,45,Colombia
```

### The Code: Ingestion
```python
import pandas as pd

# Load the CSV file into a DataFrame object named 'df'
df = pd.read_csv('orders.csv')

# Print the table to the console
print(df)
```

**Automatic Indexing:** Notice that you did not provide row numbers in the CSV. When `.read_csv()` executes, Pandas automatically generates a numeric **Index** (starting at 0) for every single row.

---

## 4. Inspecting & Understanding Data

When working with hundreds of thousands of rows, printing the entire DataFrame will crash your terminal or become unreadable. You must rely on exploration methods to inspect small chunks of the data.

### Exploring the Extremes
```python
# Returns the first 5 rows (useful for checking column headers and data formatting)
print(df.head())

# Returns a specific number of rows from the top (e.g., first 10)
print(df.head(10))

# Returns the last 5 rows (useful for checking if the file parsed correctly to the end)
print(df.tail())
```

### Extracting a Single Column
Extracting a column from a DataFrame returns a Series object. You select columns using bracket notation and the exact string name of the column.
```python
prices = df['Price']
print(prices.head(3))
```

*Sample Output:*
```text
0    1200
1     300
2      22
Name: Price, dtype: int64
```

---

## 5. Filtering Data (Conditional Selection)

Filtering creates subsets of your DataFrame based on specific logical conditions.

### Single Condition Filters
To find all orders placed in the USA, you must pass a boolean statement into the DataFrame brackets.
```python
# Step 1: Create a boolean mask (True/False evaluation for every row)
usa_mask = df['Country'] == 'USA'

# Step 2: Apply the mask to only keep rows evaluating to True
usa_orders = df[usa_mask]

# Standard Developer Practice (Combined into a single line):
usa_orders = df[df['Country'] == 'USA']
print(usa_orders)
```

### Multiple Condition Filters
You can chain multiple criteria using `&` (AND) or `|` (OR). **Crucial Syntax Note:** Every individual condition must be wrapped in its own set of parentheses.
```python
# Extract all rows where the Country is USA AND the transaction Price exceeds 100
expensive_usa_orders = df[(df['Country'] == 'USA') & (df['Price'] > 100)]
```

---

## 6. Data Cleaning & Manipulation

Data requires extensive formatting before analysis can begin. This involves altering column names, fixing structural issues, and addressing null values.

### The `inplace=True` Concept
By default, data manipulation methods in Pandas return a **brand new** DataFrame, leaving the original `df` variable completely unchanged. To force Pandas to modify the existing DataFrame directly in memory, you must use the `inplace=True` argument.

```python
# Returns a new object (Original 'df' is unmodified)
new_df = df.dropna()

# Modifies the original object directly
df.dropna(inplace=True)
```

### Renaming Columns
Use a dictionary to map the old, messy column names to new, structured names.
```python
# Example: Adding a space to "orderID" for better readability
df.rename(columns={'orderID': 'Order ID'}, inplace=True)
```

### Handling Missing/Corrupted Data
```python
# Drops any row that contains at least one NaN (Not a Number) value
df.dropna(inplace=True)

# Alternatively, fill blank cells with a default placeholder value (e.g., 0)
df.fillna(0, inplace=True)
```

---

## 7. Data Analysis & Aggregation

Pandas replaces complex loops and scripts with highly optimized, single-line aggregation functions.

### 1. Frequency Distribution: `.value_counts()`
To calculate how many times unique values appear within a specific column (e.g., analyzing order volume by region), use `.value_counts()`.

```python
order_volume = df['Country'].value_counts()
print(order_volume)
```
*Sample Output:*
```text
USA            25
South Korea    10
Colombia        3
Argentina       2
Name: count, dtype: int64
```

### 2. Grouping Metrics: `.groupby()`
The `.groupby()` method functions identically to a SQL `GROUP BY` clause. It allows you to cluster rows by a shared category and apply a mathematical calculation (like sum, mean, or max) to another column.

```python
# 1. Group the table by the 'Country' column
# 2. Isolate the numerical 'Price' column
# 3. Apply the .sum() calculation to those clustered prices
revenue_by_country = df.groupby('Country')['Price'].sum()
print(revenue_by_country)
```
*Sample Output:*
```text
Country
Argentina      22
Colombia      280
South Korea   550
USA          1265
Name: Price, dtype: int64
```

### 3. Sorting Data: `.sort_values()`
To rank your dataset, you must pass the target column to `.sort_values()`. Set `ascending=False` to order the dataset from highest to lowest.

```python
# Sort the entire DataFrame by the most expensive orders
highest_prices = df.sort_values(by='Price', ascending=False)
print(highest_prices.head())
```

---

## 8. Exporting Data

After cleaning and aggregating, you will typically save your final analytical output back to your machine.

```python
# Save the current state of 'df' to a new CSV file.
# Setting index=False prevents Pandas from exporting the 0, 1, 2, 3 numerical index as a physical column in the file.
df.to_csv('cleaned_orders.csv', index=False)
```
