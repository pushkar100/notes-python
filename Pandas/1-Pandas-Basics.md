# 📚 Python Pandas Masterclass: Comprehensive Study Notes

**Instructor:** Tech With Tim  
**Source Video:** https://www.youtube.com/watch?v=EXIgjIBu4EU

- [1. Introduction & Environment Setup](#1-introduction-environment-setup)
- [2. Core Data Structures: Series vs. DataFrame](#2-core-data-structures-series-vs-dataframe)
- [3. Loading & Creating DataFrames](#3-loading-creating-dataframes)
- [4. Inspecting & Understanding Data](#4-inspecting-understanding-data)
- [5. Filtering Data (Conditional Selection)](#5-filtering-data-conditional-selection)
- [6. Data Cleaning & Manipulation](#6-data-cleaning-manipulation)
- [7. Data Analysis & Aggregation](#7-data-analysis-aggregation)
- [8. Exporting Data](#8-exporting-data)
- [9. Converting DataFrames to Python Data Structures](#9-converting-dataframes-to-python-data-structures)
- [10. Using Pandas in Python APIs](#10-using-pandas-in-python-apis)

---

## 1. Introduction & Environment Setup

Pandas is the foundational open-source Python library used for data manipulation, cleaning, and analysis. It serves as a prerequisite for virtually all Data Science, Machine Learning (ML), Artificial Intelligence (AI), and Data Visualization workflows.

### Recommended IDEs

- **VS Code / Cursor:** Excellent for general scripting and building pipelines.
- **Jupyter Notebooks:** Highly recommended for data analysis because it allows you to run code cell-by-cell and visualize tables instantly.
- **PyCharm:** A strong choice for large-scale enterprise projects.

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

### Working with Jupyter Notebooks (The Preferred Environment)

While you can write Pandas code in standard `.py` files, the video heavily emphasizes using Jupyter Notebooks (`.ipynb`) for data-related tasks. Notebooks allow you to execute code in isolated "cells" and display DataFrames as beautifully formatted HTML tables rather than raw text in a terminal.

**Installing Jupyter:**

```bash
# Standard pip installation
pip install notebook

# If using your 'uv' virtual environment
uv add notebook
```

**How to Use and Load Jupyter:**

1.  **Browser Interface:** Run `jupyter notebook` in your terminal. This spins up a local server and opens a web interface where you can create and run `.ipynb` files.
2.  **VS Code / Cursor Integration:** The easiest modern workflow is to simply create a file named `analysis.ipynb` directly inside VS Code or Cursor. The editor will prompt you to install the Jupyter extension.
3.  **Cell Execution:** You write code in blocks (cells). For example, place `df = pd.read_csv('orders.csv')` in Cell 1. Press `Shift + Enter` to run it. Then, place `df.head()` in Cell 2 and run it. The DataFrame variables stay loaded in memory, and the output table renders beautifully right below the cell!

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

## 3. Loading & Creating DataFrames

The first operational step in Pandas is ingesting data. While the tutorial heavily focuses on CSVs, Pandas is highly versatile and can create or read DataFrames from multiple data sources to represent two-dimensional data.

### Data Sources & Ingestion Methods

- **CSV Files:** The industry standard for lightweight datasets (Comma-Separated Values).
  - Command: `pd.read_csv('file.csv')`
- **Excel Spreadsheets:** Pandas can natively read `.xlsx` files, which is common for business data.
  - Command: `pd.read_excel('file.xlsx')`
- **SQL Tables:** You can read structured data directly from relational databases using SQL queries.
  - Command: `pd.read_sql('SELECT * FROM table', connection)`
- **Machine Learning Pipelines & Native Python:** As noted in the video, many large machine learning libraries automatically set up Pandas DataFrames for you, or you can construct them manually (e.g., from standard Python dictionaries or lists) before passing them to an ML algorithm.

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

_Sample Output:_

```text
   orderID Customer Name Product Category  Quantity  Price      Country
0      101         Alice           Laptop         1   1200          USA
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
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

_Sample Output:_

```text
0    1200
1     300
2      22
Name: Price, dtype: int64
```

### Extracting Multiple Columns

To extract multiple columns, pass a list of column names inside the DataFrame brackets. The result is another DataFrame, not a Series.

```python
# Select two columns
order_summary = df[['Product Category', 'Price']]
print(order_summary.head())

# Select several columns in the order you want them displayed
order_details = df[['orderID', 'Customer Name', 'Quantity', 'Price']]
```

_Sample Output:_

```text
  Product Category  Price
0           Laptop   1200
1          Monitor    300
2            Mouse     22
3         Keyboard     45
```

### Counting Rows and Columns

Use `len()` to count rows, and use `.shape` to get both the row and column counts. For a Series, `len()` returns the number of values in that column.

```python
# Number of rows in the entire DataFrame
row_count = len(df)

# Number of rows in one column
price_count = len(df['Price'])

# Tuple in the format (number_of_rows, number_of_columns)
row_count, column_count = df.shape

# Count only non-empty values in each selected column
non_empty_values = df[['Price', 'Country']].count()

print(f'DataFrame rows: {row_count}')
print(f'DataFrame columns: {column_count}')
print(non_empty_values)
```

_Sample Output:_

```text
DataFrame rows: 4
```

_Sample Output:_

```text
DataFrame columns: 6
```

_Sample Output:_

```text
Price      4
Country    4
dtype: int64
```

Use `.size` when you need the total number of cells in a DataFrame. For a single column, `.size` is the number of rows, including missing values.

```python
total_cells = df.size
price_values_including_missing = df['Price'].size
```

_Sample Output:_

```text
total_cells: 24
```

_Sample Output:_

```text
price_values_including_missing: 4
```

### Converting Column Values to Python Collections

Use `.tolist()` to convert a Series into a regular Python list. Use `set()` when you only need the distinct values and do not need duplicates. A set is unordered, so it should not be used when the original order matters.

```python
# Python list: preserves duplicates and the Series order
countries_list = df['Country'].tolist()

# Python set: removes duplicate country names
unique_countries = set(df['Country'].dropna())

print(countries_list)
print(unique_countries)
print(len(unique_countries))  # Number of distinct countries
```

_Sample Output:_

```text
['USA', 'South Korea', 'Argentina', 'Colombia']
```

_Sample Output:_

```text
{'USA', 'South Korea', 'Argentina', 'Colombia'}
```

_Sample Output:_

```text
4
```

Pandas also provides `.unique()` and `.nunique()` for common distinct-value tasks. `.unique()` returns the distinct values, while `.nunique()` returns their count.

```python
unique_products = df['Product Category'].unique()
product_count = df['Product Category'].nunique()

# Include missing values in the distinct-value count when needed
product_count_with_missing = df['Product Category'].nunique(dropna=False)
```

_Sample Output:_

```text
unique_products: ['Laptop' 'Monitor' 'Mouse' 'Keyboard']
```

_Sample Output:_

```text
product_count: 4
```

_Sample Output:_

```text
product_count_with_missing: 4
```

### Checking Values in a Column

Use `.isin()` to check whether each row's value belongs to a list of values. It returns a Boolean Series that can also be used to filter the DataFrame.

```python
target_countries = ['USA', 'Colombia']

# True/False result for every row
is_target_country = df['Country'].isin(target_countries)

# Keep only orders from the selected countries
target_orders = df[is_target_country]
```

_Sample Output:_

```text
is_target_country: [True, False, False, True]
```

_Sample Output:_

```text
target_orders:
  orderID Customer Name Product Category  Quantity  Price   Country
0      101         Alice           Laptop         1   1200       USA
3      104         Diana         Keyboard         1     45  Colombia
```

### Reading Individual Rows and Values

Use `.iloc` for position-based access and `.loc` for label-based access. Use `.at` when retrieving one specific value.

```python
# First row by position
first_order = df.iloc[0]

# First three rows and selected columns
sample = df.iloc[0:3][['orderID', 'Price']]

# Value from the row with index label 0
first_price = df.loc[0, 'Price']

# Equivalent single-value lookup
first_country = df.at[0, 'Country']
```

_Sample Output:_

```text
first_order:
orderID                 101
Customer Name         Alice
Product Category     Laptop
Quantity                  1
Price                  1200
Country                 USA
Name: 0, dtype: object
```

_Sample Output:_

```text

sample:
  orderID  Price
0      101   1200
1      102    300
2      103     22
```

_Sample Output:_

```text

first_price: 1200
```

_Sample Output:_

```text

first_country: USA
```

### Creating Python Lists from DataFrames and `iloc` Subsets

Use `.tolist()` on a Series when you need one column as a Python list. To create a list for each row, use `.values.tolist()` or `.to_numpy().tolist()` on a DataFrame. A two-dimensional DataFrame therefore becomes a list of lists.

#### Selecting Rows and Columns with `iloc`

`iloc` uses the format `df.iloc[row_selection, column_selection]` and selects data by numeric position. In `df.iloc[0:3, [0, 4]]`, `0:3` selects rows at positions 0, 1, and 2 because the stop position 3 is exclusive. The list `[0, 4]` selects columns at positions 0 and 4, which are `orderID` and `Price` in this DataFrame. The result is a three-row, two-column DataFrame.

```python
# One column becomes a one-dimensional list
price_list = df['Price'].tolist()

# A DataFrame becomes a list containing one list per row
order_list = df[['orderID', 'Price']].values.tolist()

# Select rows and columns by position, then convert them to nested lists
subset_list = df.iloc[0:3, [0, 4]].to_numpy().tolist()

print(price_list)
print(order_list)
print(subset_list)
```

_Sample Output:_

```text
[1200, 300, 22, 45]
```

_Sample Output:_

```text
[[101, 1200], [102, 300], [103, 22], [104, 45]]
```

_Sample Output:_

```text
[[101, 1200], [102, 300], [103, 22]]
```

If you want a flat list from a rectangular `iloc` subset, flatten the values first. This is useful when you do not need to preserve row boundaries.

```python
# Select the first three rows and the Price column
price_subset = df.iloc[0:3, 4].tolist()

# Select a rectangular subset and flatten it into one list
flat_subset = df.iloc[0:2, [0, 4]].to_numpy().flatten().tolist()
```

_Sample Output:_

```text
price_subset: [1200, 300, 22]
```

_Sample Output:_

```text
flat_subset: [101, 1200, 102, 300]
```

### Selecting Data with `loc`

`loc` selects data by row and column labels, while `iloc` selects data by numeric position. The general format is `df.loc[row_labels, column_labels]`. With the default index in this example, the row labels happen to be `0`, `1`, `2`, and `3`, but labels do not have to be numbers.

| Accessor | Selects by            | Slice endpoint | Example                |
| -------- | --------------------- | -------------- | ---------------------- |
| `loc`    | Row and column labels | Included       | `df.loc[0:2, 'Price']` |
| `iloc`   | Numeric positions     | Excluded       | `df.iloc[0:3, 4]`      |

#### Common `loc` Access Patterns

```python
# One cell: row label 0, column label 'Price'
price = df.loc[0, 'Price']

# One row by its label
first_order = df.loc[0]

# Several rows by their labels
selected_orders = df.loc[[0, 2]]

# One entire column
prices = df.loc[:, 'Price']

# Several columns for every row
order_summary = df.loc[:, ['orderID', 'Price']]

# A row-label slice: 0, 1, and 2 are all included
first_three_orders = df.loc[0:2]

# Row-label slice and selected columns
sample = df.loc[0:2, ['orderID', 'Price']]

# Filter rows with a Boolean condition, then choose columns
expensive_orders = df.loc[df['Price'] > 100, ['orderID', 'Price', 'Country']]
```

_Sample Output:_

```text
price: 1200
```

_Sample Output:_

```text

first_order:
orderID                 101
Customer Name         Alice
Product Category     Laptop
Quantity                  1
Price                  1200
Country                 USA
Name: 0, dtype: object
```

_Sample Output:_

```text

selected_orders:
  orderID Customer Name Product Category  Quantity  Price    Country
0      101         Alice           Laptop         1   1200        USA
2      103       Charlie            Mouse         1     22  Argentina
```

_Sample Output:_

```text

prices:
0    1200
1     300
2      22
3      45
Name: Price, dtype: int64
```

_Sample Output:_

```text

order_summary:
  orderID  Price
0      101   1200
1      102    300
2      103     22
3      104     45
```

_Sample Output:_

```text

sample:
  orderID  Price
0      101   1200
1      102    300
2      103     22
```

_Sample Output:_

```text

expensive_orders:
  orderID  Price      Country
0      101   1200          USA
1      102    300  South Korea
```

#### Updating Values with `loc`

Because `loc` identifies data by labels, it is also useful for assigning values to a single cell, a complete column, or rows that match a condition.

```python
# Update one cell
df.loc[0, 'Price'] = 1250

# Create a new column for every row
df.loc[:, 'Tax'] = df['Price'] * 0.10

# Update a column only for matching rows
df.loc[df['Country'] == 'USA', 'Country'] = 'United States'
```

_Sample Output:_

```text
After updating row 0 Price:
0    1250
1     300
2      22
3      45
Name: Price, dtype: int64
```

_Sample Output:_

```text

Tax:
0    125.0
1     30.0
2      2.2
3      4.5
Name: Tax, dtype: float64
```

_Sample Output:_

```text

Country at row 0: United States
```

Use `loc` when the meaning of the row or column label matters, especially after setting a custom index. Use `iloc` when you specifically need the item at a numeric position.

### Counting Values and Inspecting Column Types

These operations are useful for quickly understanding a column before cleaning or analysis.

```python
# Count every value, including duplicate values
country_counts = df['Country'].value_counts()

# Display the data type of each column
print(df.dtypes)

# Get a compact overview of row counts, types, and non-empty values
df.info()
```

_Sample Output:_

```text
country_counts:
USA            1
South Korea    1
Argentina      1
Colombia       1
Name: count, dtype: int64
```

_Sample Output:_

```text

df.dtypes:
orderID                int64
Customer Name         object
Product Category      object
Quantity               int64
Price                  int64
Country               object
dtype: object
```

_Sample Output:_

```text

df.info():
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4 entries, 0 to 3
Data columns (total 6 columns):
 #   Column            Non-Null Count  Dtype
---  ------            --------------  -----
 0   orderID           4 non-null      int64
 1   Customer Name     4 non-null      object
 2   Product Category  4 non-null      object
 3   Quantity          4 non-null      int64
 4   Price             4 non-null      int64
 5   Country           4 non-null      object
```

---

### Data Access: Normal Python vs. Pandas DataFrame

Normal Python collections and pandas DataFrames use different access patterns. Lists are accessed by numeric position, dictionaries are accessed by keys, and DataFrames support both numeric positions and row/column labels.

The examples below represent the same orders in different structures:

```python
# Normal Python: a list of lists has no column labels
orders_list = [
  [101, 'Alice', 'Laptop', 1, 1200, 'USA'],
  [102, 'Bob', 'Monitor', 2, 300, 'South Korea'],
]

# Normal Python: dictionaries make field names explicit
order_dict = {
  'orderID': 101,
  'Customer Name': 'Alice',
  'Product Category': 'Laptop',
  'Quantity': 1,
  'Price': 1200,
  'Country': 'USA',
}

# Pandas: rows and columns have labels
orders_df = pd.DataFrame(orders_list, columns=[
  'orderID', 'Customer Name', 'Product Category',
  'Quantity', 'Price', 'Country'
])
```

#### Comparing Common Access Operations

| Operation            | Normal Python list                                | Normal Python dictionary            | Pandas DataFrame                           |
| -------------------- | ------------------------------------------------- | ----------------------------------- | ------------------------------------------ |
| First row            | `orders_list[0]`                                  | Not directly applicable             | `orders_df.iloc[0]`                        |
| One field            | `orders_list[0][4]`                               | `order_dict['Price']`               | `orders_df.loc[0, 'Price']`                |
| One cell by position | `orders_list[0][4]`                               | Not directly applicable             | `orders_df.iloc[0, 4]`                     |
| One column           | `[row[4] for row in orders_list]`                 | `[order_dict['Price']]`             | `orders_df['Price']`                       |
| Several columns      | `[row[0:2] for row in orders_list]`               | `[order_dict[key] for key in keys]` | `orders_df[['orderID', 'Customer Name']]`  |
| First two rows       | `orders_list[0:2]`                                | Not directly applicable             | `orders_df.iloc[0:2]`                      |
| Filter by a value    | `[row for row in orders_list if row[5] == 'USA']` | `order_dict['Country'] == 'USA'`    | `orders_df[orders_df['Country'] == 'USA']` |

#### Fetching Rows, Columns, and Cells

```python
# Normal Python list: position-based access only
first_order = orders_list[0]
first_price = orders_list[0][4]
all_prices = [order[4] for order in orders_list]

# Normal Python dictionary: key-based access
customer_name = order_dict['Customer Name']
country = order_dict.get('Country')

# Pandas DataFrame: position-based access with iloc
first_order_df = orders_df.iloc[0]
first_price_by_position = orders_df.iloc[0, 4]
first_two_orders = orders_df.iloc[0:2]

# Pandas DataFrame: label-based access with loc
price_column = orders_df['Price']
first_price_by_label = orders_df.loc[0, 'Price']
selected_columns = orders_df.loc[:, ['orderID', 'Price']]

# at and iat are optimized for fetching one cell
price_by_label = orders_df.at[0, 'Price']
price_by_position = orders_df.iat[0, 4]
```

_Sample Output:_

```text
first_order: [101, 'Alice', 'Laptop', 1, 1200, 'USA']
```

_Sample Output:_

```text
first_price: 1200
```

_Sample Output:_

```text
all_prices: [1200, 300]
```

_Sample Output:_

```text
customer_name: Alice
```

_Sample Output:_

```text
country: USA
```

_Sample Output:_

```text
first_price_by_position: 1200
```

_Sample Output:_

```text
first_price_by_label: 1200
```

_Sample Output:_

```text
price_by_label: 1200
```

_Sample Output:_

```text
price_by_position: 1200
```

#### The Main Difference

- **Normal Python lists:** Fast and simple for small, position-based collections, but you must remember which position represents each field.
- **Normal Python dictionaries:** Clear for accessing fields by key, but handling many rows requires loops or a list of dictionaries.
- **Pandas DataFrames:** Designed for tabular data. They provide labeled columns, row and column selection, vectorized operations, filtering, missing-value handling, and aggregation without writing a loop for every row.

Use `iloc` when you know the numeric row or column position. Use `loc` when you want to access data by its row or column label. For a single cell, use `at` with labels or `iat` with numeric positions.

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

_Sample Output:_

```text
  orderID Customer Name Product Category  Quantity  Price Country
0      101         Alice           Laptop         1   1200     USA
```

### Other Common Filter Operations

Pandas comparison operators create a Boolean mask for every row. Apply that mask inside `df[...]` to keep only matching rows.

#### Comparison Operators

```python
# Equal to
price_is_300 = df[df['Price'] == 300]

# Not equal to
not_usa_orders = df[df['Country'] != 'USA']

# Greater than and greater than or equal to
prices_over_100 = df[df['Price'] > 100]
prices_at_least_300 = df[df['Price'] >= 300]

# Less than and less than or equal to
prices_under_300 = df[df['Price'] < 300]
prices_at_most_300 = df[df['Price'] <= 300]
```

_Sample Output:_

```text
price_is_300:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
```

_Sample Output:_

```text

not_usa_orders:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie             Mouse         1     22    Argentina
3      104         Diana          Keyboard         1     45     Colombia
```

_Sample Output:_

```text

prices_over_100:
  orderID Customer Name Product Category  Quantity  Price      Country
0      101         Alice           Laptop         1   1200          USA
1      102           Bob          Monitor         2    300  South Korea
```

_Sample Output:_

```text

prices_at_least_300:
  orderID Customer Name Product Category  Quantity  Price      Country
0      101         Alice           Laptop         1   1200          USA
1      102           Bob          Monitor         2    300  South Korea
```

_Sample Output:_

```text

prices_under_300:
  orderID Customer Name Product Category  Quantity  Price   Country
2      103       Charlie            Mouse         1     22 Argentina
3      104         Diana          Keyboard         1     45  Colombia
```

_Sample Output:_

```text

prices_at_most_300:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana          Keyboard         1     45     Colombia
```

#### AND, OR, and NOT Filters

Use `&` for AND, `|` for OR, and `~` to invert a Boolean condition. Put each condition in parentheses because pandas evaluates these operators differently from Python's `and`, `or`, and `not`.

```python
# AND: both conditions must be true
usa_or_expensive = df[(df['Country'] == 'USA') & (df['Price'] > 100)]

# OR: at least one condition must be true
usa_or_argentina = df[(df['Country'] == 'USA') | (df['Country'] == 'Argentina')]

# NOT: invert a condition
not_expensive = df[~(df['Price'] > 100)]
```

_Sample Output:_

```text
usa_or_expensive:
  orderID Customer Name Product Category  Quantity  Price Country
0      101         Alice           Laptop         1   1200     USA
```

_Sample Output:_

```text

usa_or_argentina:
  orderID Customer Name Product Category  Quantity  Price   Country
0      101         Alice           Laptop         1   1200       USA
2      103       Charlie            Mouse         1     22  Argentina
```

_Sample Output:_

```text

not_expensive:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
```

#### Membership Filters with `.isin()`

Use `.isin()` to match a column against multiple possible values. It is usually clearer than writing several equality comparisons joined with `|`.

```python
selected_countries = ['USA', 'Colombia']
selected_orders = df[df['Country'].isin(selected_countries)]

# Use ~ to select values that are not in the list
other_orders = df[~df['Country'].isin(selected_countries)]
```

_Sample Output:_

```text
selected_orders:
  orderID Customer Name Product Category  Quantity  Price   Country
0      101         Alice           Laptop         1   1200       USA
3      104         Diana         Keyboard         1     45  Colombia
```

_Sample Output:_

```text

other_orders:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
```

#### Range Filters with `.between()`

Use `.between(lower, upper)` when a value must fall within a range. The boundaries are included by default.

```python
# Includes both 20 and 300 if those values exist
mid_range_orders = df[df['Price'].between(20, 300)]

# Exclude the boundary values with inclusive='neither'
strict_mid_range_orders = df[df['Price'].between(20, 300, inclusive='neither')]
```

_Sample Output:_

```text
mid_range_orders:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
```

_Sample Output:_

```text

strict_mid_range_orders:
  orderID Customer Name Product Category  Quantity  Price      Country
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
```

#### Text Filters with `.str`

String methods allow you to filter text columns by prefixes, suffixes, or partial matches. Use `na=False` when missing text values should count as non-matches.

```python
# Product names containing the letters "top"
laptop_orders = df[df['Product Category'].str.contains('top', case=False, na=False)]

# Customer names beginning with "A"
customers_starting_with_a = df[df['Customer Name'].str.startswith('A', na=False)]

# Countries ending with "a"
countries_ending_with_a = df[df['Country'].str.endswith('a', na=False)]
```

_Sample Output:_

```text
laptop_orders:
  orderID Customer Name Product Category  Quantity  Price Country
0      101         Alice           Laptop         1   1200     USA
```

_Sample Output:_

```text

customers_starting_with_a:
  orderID Customer Name Product Category  Quantity  Price Country
0      101         Alice           Laptop         1   1200     USA
```

_Sample Output:_

```text

countries_ending_with_a:
  orderID Customer Name Product Category  Quantity  Price   Country
2      103       Charlie            Mouse         1     22  Argentina
3      104         Diana          Keyboard         1     45  Colombia
```

#### Missing-Value Filters

Use `.isna()` to find missing values and `.notna()` to find values that are present. Do not compare missing values with `== None` or `== float('nan')`.

```python
# Rows where Price is missing
missing_prices = df[df['Price'].isna()]

# Rows where Country is available
known_countries = df[df['Country'].notna()]
```

_Sample Output:_

```text
missing_prices:
Empty DataFrame
Columns: [orderID, Customer Name, Product Category, Quantity, Price, Country]
Index: []
```

_Sample Output:_

```text

known_countries:
  orderID Customer Name Product Category  Quantity  Price      Country
0      101         Alice           Laptop         1   1200          USA
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
```

#### Filtering by Index

Use `.loc` to filter by index labels. Use `.iloc` when selecting rows by their numeric positions rather than by a condition.

```python
# Select rows whose index labels are 1 and 3
selected_rows = df.loc[[1, 3]]

# Select rows in positions 1 through 2 (the stop position is exclusive)
middle_rows = df.iloc[1:3]
```

_Sample Output:_

```text
selected_rows:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
3      104         Diana         Keyboard         1     45     Colombia
```

_Sample Output:_

```text

middle_rows:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
```

For complex filters, assign the Boolean mask to a variable first. This makes the logic easier to inspect and reuse.

```python
price_filter = df['Price'] >= 300
country_filter = df['Country'].isin(['USA', 'South Korea'])
filtered_orders = df[price_filter & country_filter]
```

_Sample Output:_

```text
  orderID Customer Name Product Category  Quantity  Price      Country
0      101         Alice           Laptop         1   1200          USA
1      102           Bob          Monitor         2    300  South Korea
```

---

## 6. Data Cleaning & Manipulation

Data requires extensive formatting before analysis can begin. This involves altering column names, fixing structural issues, and addressing null values.

### Simple Assignments and Manipulations

The simplest way to manipulate a DataFrame is with assignment. Assignment changes the existing DataFrame directly, so the result does not need to be stored in a new variable.

```python
# Update one cell by row and column label
df.loc[0, 'Price'] = 1250

# Replace every value in an existing column
df['Country'] = df['Country'].str.upper()

# Create a new column from existing columns
df['Total'] = df['Quantity'] * df['Price']

# Create a column with the same value for every row
df['Reviewed'] = False
```

_Sample Output:_

```text
After df.loc[0, 'Price'] = 1250:
  orderID  Price
0      101   1250
1      102    300
2      103     22
3      104     45
```

_Sample Output:_

```text

After df['Country'] = df['Country'].str.upper():
0            USA
1    SOUTH KOREA
2      ARGENTINA
3       COLOMBIA
Name: Country, dtype: object
```

_Sample Output:_

```text

df['Total']:
0    1250
1     600
2      22
3      45
Name: Total, dtype: int64
```

_Sample Output:_

```text

df['Reviewed']:
0    False
1    False
2    False
3    False
Name: Reviewed, dtype: bool
```

To update only selected rows, combine assignment with a Boolean condition. Use `.loc` so pandas updates the original DataFrame without relying on an intermediate slice.

```python
# Add 10% to prices below 100
low_price_mask = df['Price'] < 100
df.loc[low_price_mask, 'Price'] = df.loc[low_price_mask, 'Price'] * 1.10
```

_Sample Output:_

```text
  orderID  Price
0      101   1250.0
1      102    300.0
2      103     24.2
3      104     49.5
```

### Removing Rows and Columns with `.drop()`

Use `.drop()` when you know which row labels or column names should be removed. Unlike `.dropna()`, which looks for missing values automatically, `.drop()` removes the labels you specify.

```python
# Remove one row by its index label
without_first_order = df.drop(index=0)

# Remove multiple rows by their index labels
without_some_orders = df.drop(index=[1, 3])

# Remove one column by name
without_country = df.drop(columns='Country')

# Remove multiple columns by name
summary = df.drop(columns=['Customer Name', 'Country'])
```

_Sample Output:_

```text
without_first_order:
  orderID Customer Name Product Category  Quantity  Price      Country
1      102           Bob          Monitor         2    300  South Korea
2      103       Charlie            Mouse         1     22    Argentina
3      104         Diana         Keyboard         1     45     Colombia
```

_Sample Output:_

```text

without_some_orders:
  orderID Customer Name Product Category  Quantity  Price Country
0      101         Alice           Laptop         1   1200     USA
2      103       Charlie            Mouse         1     22 Argentina
```

_Sample Output:_

```text

without_country:
  orderID Customer Name Product Category  Quantity  Price
0      101         Alice           Laptop         1   1200
1      102           Bob          Monitor         2    300
2      103       Charlie            Mouse         1     22
3      104         Diana         Keyboard         1     45
```

_Sample Output:_

```text

summary:
  orderID Product Category  Quantity  Price
0      101           Laptop         1   1200
1      102          Monitor         2    300
2      103            Mouse         1     22
3      104         Keyboard         1     45
```

You can use `axis=0` for rows and `axis=1` for columns, although the explicit `index=` and `columns=` arguments are usually easier to read.

```python
# Equivalent row and column operations using axis
without_first_order = df.drop(0, axis=0)
without_country = df.drop('Country', axis=1)

# Keep the original DataFrame unchanged and return a new one
new_df = df.drop(columns=['Country'])

# Modify the original DataFrame directly
df.drop(columns=['Country'], inplace=True)
```

`.drop()` removes explicitly named labels. `.dropna()` removes rows or columns based on whether they contain missing values. Both return a new DataFrame by default.

### Understanding `dropna()` and Method-Based Changes

`dropna()` removes rows or columns that contain missing values such as `NaN`, `None`, or `NaT`. By default, it returns a cleaned copy and leaves the original DataFrame unchanged. Use `axis=1` to remove columns instead of rows.

```python
# Remove rows containing at least one missing value
clean_orders = df.dropna()

# Remove columns containing at least one missing value
clean_columns = df.dropna(axis=1)
```

_Sample Output:_

```text
Original DataFrame:
  orderID  Price      Country
0      101  1200          USA
1      102   NaN   South Korea
2      103     22           NaN
```

_Sample Output:_

```text

clean_orders = df.dropna():
  orderID  Price Country
0      101  1200     USA
```

_Sample Output:_

```text

clean_columns = df.dropna(axis=1):
  orderID
0      101
1      102
2      103
```

### Filling Values with `.fillna()`

Use `.fillna()` to replace missing values with a default value. Pandas does not use a general `DataFrame.fill()` method for this operation.

```python
# Replace every missing value in Price with 0
filled_prices = df['Price'].fillna(0)

# Replace missing Country values with 'Unknown'
filled_countries = df['Country'].fillna('Unknown')

# Replace every missing value in the DataFrame with 0
updated_df = df.fillna(0)
```

_Sample Output:_

```text
filled_prices:
0    1200.0
1       0.0
2      22.0
Name: Price, dtype: float64
```

_Sample Output:_

```text

filled_countries:
0            USA
1    South Korea
2        Unknown
Name: Country, dtype: object
```

`fillna()` is the usual choice for missing-data cleanup. Like `dropna()`, it returns a new object by default; use `inplace=True` when the method supports it and you want to modify the original DataFrame.

### The `inplace=True` Concept

For pandas methods that support it, `inplace=True` tells the method to modify the existing DataFrame instead of returning a separate cleaned or transformed DataFrame. This rule applies to method calls such as `dropna()`, not to ordinary assignment statements.

```python
# Returns a new object; the original 'df' is unmodified
new_df = df.dropna()

# Modifies the original 'df' directly and returns None
df.dropna(inplace=True)
```

Direct assignment behaves differently because the assignment target is the existing DataFrame itself. The right-hand side is calculated, and the result is written into `df` immediately.

```python
# Direct assignment changes the existing DataFrame
df['Total'] = df['Quantity'] * df['Price']

# Method call without assignment does not replace df
df.dropna()

# Store the returned DataFrame when you want to keep the method result
df = df.dropna()
```

In short: assignment changes the target you assign to, while most pandas methods return a new object by default. Always check the method documentation because not every method supports `inplace=True`.

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

_Sample Output:_

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

_Sample Output:_

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

_Sample `cleaned_orders.csv` Output:_

```csv
orderID,Customer Name,Product Category,Quantity,Price,Country
101,Alice,Laptop,1,1200,USA
102,Bob,Monitor,2,300,South Korea
103,Charlie,Mouse,1,22,Argentina
104,Diana,Keyboard,1,45,Colombia
```

By default, `to_csv()` uses `index=True`, so the DataFrame index is included. Writing `index=True` explicitly produces the same result.

```python
# These two commands both include the DataFrame index
df.to_csv('orders_with_index.csv')
df.to_csv('orders_with_index_explicit.csv', index=True)
```

_Sample `orders_with_index.csv` Output:_

```csv
,orderID,Customer Name,Product Category,Quantity,Price,Country
0,101,Alice,Laptop,1,1200,USA
1,102,Bob,Monitor,2,300,South Korea
2,103,Charlie,Mouse,1,22,Argentina
3,104,Diana,Keyboard,1,45,Colombia
```

The first column contains the pandas index. When reading this file back, you can restore it as the index with `pd.read_csv('orders_with_index.csv', index_col=0)`.

---

## 9. Converting DataFrames to Python Data Structures

Use these simple conversions when passing pandas data to regular Python code, APIs, or loops.

### DataFrame Column to a List

```python
price_list = df['Price'].tolist()
```

_Sample Output:_

```text
[1200, 300, 22, 45]
```

### Column to a Set

```python
country_set = set(df['Country'].dropna())
```

_Sample Output:_

```text
{'USA', 'South Korea', 'Argentina', 'Colombia'}
```

### DataFrame Rows to Lists

```python
row_lists = df[['orderID', 'Price']].values.tolist()
```

_Sample Output:_

```text
[[101, 1200], [102, 300], [103, 22], [104, 45]]
```

### DataFrame Rows to Dictionaries

```python
records = df[['orderID', 'Price', 'Country']].to_dict(orient='records')
```

_Sample Output:_

```text
[
  {'orderID': 101, 'Price': 1200, 'Country': 'USA'},
  {'orderID': 102, 'Price': 300, 'Country': 'South Korea'},
  {'orderID': 103, 'Price': 22, 'Country': 'Argentina'},
  {'orderID': 104, 'Price': 45, 'Country': 'Colombia'}
]
```

### DataFrame to a Dictionary

```python
column_dictionary = df[['orderID', 'Price']].to_dict()
```

_Sample Output:_

```text
{
  'orderID': {0: 101, 1: 102, 2: 103, 3: 104},
  'Price': {0: 1200, 1: 300, 2: 22, 3: 45}
}
```

### DataFrame Rows to Tuples

```python
row_tuples = list(df[['orderID', 'Price']].itertuples(index=False, name=None))
```

_Sample Output:_

```text
[(101, 1200), (102, 300), (103, 22), (104, 45)]
```

For most practical tasks, use `.tolist()` for one column, `orient='records'` for a list of row dictionaries, and `.itertuples()` when looping over rows.

---

## 10. Using Pandas in Python APIs

APIs commonly receive and return lists of dictionaries. Pandas is useful in the middle of that process: convert the incoming Python data to a DataFrame, perform the calculation or filter, then convert the result back to Python dictionaries for the response.

### API Input: Python Records to a DataFrame

Imagine an API receives this JSON-like Python value from a request body:

```python
orders_data = [
  {'orderID': 101, 'Product': 'Laptop', 'Quantity': 1, 'Price': 1200},
  {'orderID': 102, 'Product': 'Monitor', 'Quantity': 2, 'Price': 300},
]

orders_df = pd.DataFrame(orders_data)
```

_Sample Output:_

```text
   orderID  Product  Quantity  Price
0      101   Laptop         1   1200
1      102  Monitor         2    300
```

### API Operation: Add a Calculated Field

Use vectorized column operations to calculate values for every record at once. This is simpler than writing a loop for each row.

```python
orders_df['Total'] = orders_df['Quantity'] * orders_df['Price']
```

_Sample Output:_

```text
   orderID  Product  Quantity  Price  Total
0      101   Laptop         1   1200   1200
1      102  Monitor         2    300    600
```

### API Operation: Filter Query Results

An API might receive a query parameter such as `min_total`. Use it to return only matching records.

```python
min_total = 700
filtered_df = orders_df[orders_df['Total'] >= min_total]
```

_Sample Output:_

```text
   orderID Product  Quantity  Price  Total
0      101  Laptop         1   1200   1200
```

### API Response: DataFrame to List of Dictionaries

Convert the filtered DataFrame to records before returning it from a typical Python API route.

```python
response_data = filtered_df.to_dict(orient='records')
```

_Sample Output:_

```text
[
  {'orderID': 101, 'Product': 'Laptop', 'Quantity': 1, 'Price': 1200, 'Total': 1200}
]
```

### API Operation: Return a Summary

An API can return summary values instead of full rows. Convert the pandas result to a normal Python value before building the response.

```python
total_revenue = orders_df['Total'].sum()
order_count = len(orders_df)

summary_response = {
  'order_count': order_count,
  'total_revenue': total_revenue,
}
```

_Sample Output:_

```text
{'order_count': 2, 'total_revenue': 1800}
```

### API Operation: Sort and Paginate Results

Sorting and pagination are common for list endpoints. `head()` is a simple way to limit the number of rows in a beginner example.

```python
page_size = 1
page_number = 1
start = (page_number - 1) * page_size

page_df = orders_df.sort_values('Total', ascending=False).iloc[start:start + page_size]
page_response = page_df.to_dict(orient='records')
```

_Sample Output:_

```text
[
  {'orderID': 101, 'Product': 'Laptop', 'Quantity': 1, 'Price': 1200, 'Total': 1200}
]
```

The common API pattern is: receive Python dictionaries, create a DataFrame, filter or calculate with pandas, and return `to_dict(orient='records')` or a normal Python dictionary.
