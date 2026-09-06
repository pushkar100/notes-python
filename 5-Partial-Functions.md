# Notes: Partial Functions in Python

_Based on the NeuralNine tutorial on YouTube._

- [1. What is a Partial Function?](#1-what-is-a-partial-function)
- [2. Creating Partial Functions Manually (Not Recommended)](#2-creating-partial-functions-manually-not-recommended)
  - [Example 1: Direct `lambda` Wrapper](#example-1-direct-lambda-wrapper)
  - [Example 2: Higher-Order Factory Function](#example-2-higher-order-factory-function)
  - [Why this is not recommended:](#why-this-is-not-recommended)
- [3. The Recommended Way: `functools.partial`](#3-the-recommended-way-functoolspartial)
  - [Basic Example: Comparisons](#basic-example-comparisons)
  - [Realistic Example: Fetching Stock Data](#realistic-example-fetching-stock-data)
- [4. Key Takeaways](#4-key-takeaways)

## 1. What is a Partial Function?

A partial function is a new function created from an existing function by taking one or more of its parameters and setting them to fixed, constant values [cite: 1]. By doing this, you don't have to pass those specific arguments to the function anymore [cite: 1]. This is incredibly helpful when working with complex functions where certain arguments repeat frequently [cite: 1].

## 2. Creating Partial Functions Manually (Not Recommended)

You can create partial functions manually by using a `lambda` expression or a wrapper function (closure) that fixes one of the arguments.

### Example 1: Direct `lambda` Wrapper

If you have a base function `greater_than(a, b)`:

```python
def greater_than(a, b):
    return a > b

# Manually fixing 'b' to 20 using a lambda:
greater_than_20 = lambda a: greater_than(a, 20)

print(greater_than_20(30))  # True
print(greater_than_20(10))  # False
```

### Example 2: Higher-Order Factory Function

```python
def make_greater_than(b):
    # Returns a new function with 'b' enclosed
    return lambda a: greater_than(a, b)

greater_than_50 = make_greater_than(50)
print(greater_than_50(65))  # True
print(greater_than_50(25))  # False
```

### Why this is not recommended:

1. **Lacks Metadata & Introspection:** Lambdas do not preserve original docstrings, function names (`greater_than_20.__name__` is just `"<lambda>"`), or annotations.
2. **Boilerplate:** You have to manually write and maintain wrappers for every combination of arguments you want to pre-fill.
3. **No Introspection of Frozen Arguments:** Unlike `functools.partial` (which provides `.func`, `.args`, and `.keywords`), manual lambdas don't expose what arguments were frozen.

## 3. The Recommended Way: `functools.partial`

The built-in and recommended way to create partial functions in Python is by using the `partial` method from the core `functools` module [cite: 1].

**Importing:**

```python
from functools import partial
```

### Basic Example: Comparisons

If you have a base function `greater_than(a, b)`:

```python
def greater_than(a, b):
    return a > b
```

You can create a new function `greater_than_20` by setting the `b` parameter to 20:

```python
greater_than_20 = partial(greater_than, b=20)

# Now it only requires the 'a' parameter
print(greater_than_20(30)) # Returns True
print(greater_than_20(10)) # Returns False
```

_Note: You can pass positional or keyword arguments to `partial`. If you skip positional keywords, Python applies them in the original function's order [cite: 1]._

### Realistic Example: Fetching Stock Data

Imagine a function `get_stock_data(ticker, start, end)` that fetches financial data [cite: 1]:

**Fixing the Ticker:**
If you want to pull data only for Apple, you can fix the `ticker` argument [cite: 1]:

```python
get_apple_data = partial(get_stock_data, 'AAPL')

# Now you only need to pass the dates
data = get_apple_data(start='1-1-2018', end='1-1-2019')
```

**Fixing the Time Frame:**
Alternatively, if you want to pull data for many companies but always starting from 2018 [cite: 1]:

```python
get_stock_data_from_2018 = partial(get_stock_data, start='1-1-2018')

# When calling this, you must specify subsequent parameters (like 'end') as keyword arguments
# so you don't accidentally overwrite the 'start' argument.
data = get_stock_data_from_2018('FB', end='1-1-2020')
```

**Fixing Multiple Parameters:**
You can fix multiple arguments at once [cite: 1]:

```python
get_stock_2018_to_2020 = partial(get_stock_data, start='1-1-2018', end='1-1-2020')

# Now you only need to supply the ticker symbol
data = get_stock_2018_to_2020('GS')
```

## 4. Key Takeaways

- Partial functions prevent you from repeating the same arguments over and over [cite: 1].
- They save you from having to rewrite entirely new functions that do the exact same thing with fewer parameters [cite: 1].
- Always import `partial` from `functools` rather than building lambda wrappers yourself [cite: 1].
- Pay attention to argument positioning. If you fix an earlier parameter (like `start`), ensure you use explicit keyword arguments for the remaining parameters (like `end=...`) when calling the new function so things don't get overwritten incorrectly [cite: 1].
