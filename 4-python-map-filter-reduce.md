# Functional Programming in Python: Map, Filter, and Reduce

_A practical, beginner-friendly guide to functional programming and iterators in Python based on `db2.py`._

---

## Table of Contents

- [1. `map()`: Transforming Every Element](#1-map-transforming-every-element)
  - [1.1 Concept & Syntax](#11-concept--syntax)
  - [1.2 Code from `db2.py` (Celsius to Fahrenheit)](#12-code-from-db2py-celsius-to-fahrenheit)
  - [1.3 Other Ways to Invoke `map()` & Popular Real-World Usages](#13-other-ways-to-invoke-map--popular-real-world-usages)
- [2. The Iterator Trap: Why Did My Iterator Turn Empty?](#2-the-iterator-trap-why-did-my-iterator-turn-empty)
- [3. `filter()`: Selecting Elements That Pass a Test](#3-filter-selecting-elements-that-pass-a-test)
  - [3.1 Concept & Syntax](#31-concept--syntax)
  - [3.2 Code from `db2.py` and the `map` vs. `filter` Discovery](#32-code-from-db2py-and-the-map-vs-filter-discovery)
  - [3.3 Other Ways to Invoke `filter()` & Popular Real-World Usages](#33-other-ways-to-invoke-filter--popular-real-world-usages)
- [4. The Common Gotcha: `map()` vs. `filter()`](#4-the-common-gotcha-map-vs-filter)
- [5. `reduce()`: Aggregating to a Single Value](#5-reduce-aggregating-to-a-single-value)
  - [5.1 Concept & Syntax](#51-concept--syntax)
  - [5.2 Code from `db2.py` (Sum of Prices)](#52-code-from-db2py-sum-of-prices)
  - [5.3 How `reduce()` Works Internally: The Accumulator](#53-how-reduce-works-internally-the-accumulator)
  - [5.4 Using the `operator` Module (Cleaner & Faster)](#54-using-the-operator-module-cleaner--faster)
- [6. The Power of the `initial` Value in `reduce()`](#6-the-power-of-the-initial-value-in-reduce)
  - [6.1 Why `initial` is Critical: Preventing the Empty Sequence Crash](#61-why-initial-is-critical-preventing-the-empty-sequence-crash)
  - [6.2 Popular Advanced Patterns with `reduce()`](#62-popular-advanced-patterns-with-reduce)
- [7. `reduce()` vs. `itertools.accumulate()`](#7-reduce-vs-itertoolsaccumulate)
- [8. Building a Full Data Pipeline: Filter $\rightarrow$ Map $\rightarrow$ Reduce](#8-building-a-full-data-pipeline-filter--map--reduce)
- [9. Cheat Sheet & Decision Matrix: Functional Tools vs. Comprehensions](#9-cheat-sheet--decision-matrix-functional-tools-vs-comprehensions)

---

Python is a versatile multi-paradigm programming language. Alongside object-oriented and procedural styles, Python provides powerful tools inspired by **functional programming**:

- **`map()`**: Transforms every element in an iterable by applying a function.
- **`filter()`**: Selects only elements from an iterable that satisfy a boolean condition.
- **`reduce()`**: Cumulatively combines all items in an iterable down into a single summary value.

```text
Input Collection:  [ A,   B,   C,   D ]
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
    map(func)       filter(func)     reduce(func)
[ f(A), f(B), ... ]  [ Keeps B, D ]   Single Value: (((A + B) + C) + D)
```

---

## 1. `map()`: Transforming Every Element

### 1.1 Concept & Syntax

`map()` is a Python **built-in** function. It takes a function and applies it to each item in one or more iterables.

```python
map(function, iterable, ...)
```

- **Returns**: A **lazy iterator** (`<map object>`). It does **not** create a new list immediately in memory; instead, it generates items one by one on demand.
- **Memory Efficient**: Ideal for processing massive datasets or infinite streams.

---

### 1.2 Code from `db2.py` (Celsius to Fahrenheit)

```python
# Collection of temperatures in Celsius
celcius_temps = [0.0, 10.0, 40.5, 36.1, 29.5]

def c_to_f(temp):
    return (temp * 9 / 2) + 32

# map() produces a lazy iterator
farenheit_temps = map(c_to_f, celcius_temps)

print(farenheit_temps)
# Output: <map object at 0x1072b79c0>

# First consumption of the iterator using a for-loop
for ftemp in farenheit_temps:
    print(ftemp)

# Output:
# 32.0
# 77.0
# 214.25
# 194.45000000000002
# 164.75

# Converting the iterator back to a list (AFTER it was already consumed):
print(list(farenheit_temps))
# Output: []
```

#### Immediate Consumption with `list()`

If you need the entire transformed sequence stored and ready to use, convert it immediately:

```python
print(list(map(c_to_f, celcius_temps)))
# Output: [32.0, 77.0, 214.25, 194.45000000000002, 164.75]
```

#### Using an Anonymous `lambda`

If the transformation is a simple one-liner, you don't need to define a separate `def` function:

```python
print(list(map(lambda temp: (temp * 9 / 2) + 32, celcius_temps)))
# Output: [32.0, 77.0, 214.25, 194.45000000000002, 164.75]
```

---

### 1.1.3 Other Ways to Invoke `map()` & Popular Real-World Usages

#### Method 1: Using Built-in Functions & Methods as Callables

Functions in Python are first-class citizens. You can pass built-ins like `int`, `float`, `abs`, `str`, or method descriptors like `str.strip`, `str.upper` directly to `map()` without writing any wrapper or lambda.

```python
# 1. Parsing space-separated string inputs (Standard competitive programming pattern)
raw_input = "10 25 40 85 99"
numbers = list(map(int, raw_input.split()))
print(numbers)
# Output: [10, 25, 40, 85, 99]

# 2. Sanitizing and trimming strings in batch
raw_names = ["  alice ", " bob\n", "\t charlie  "]
clean_names = list(map(str.strip, raw_names))
print(clean_names)
# Output: ['alice', 'bob', 'charlie']

# 3. Converting to uppercase
words = ["python", "functional", "programming"]
upper_words = list(map(str.upper, words))
print(upper_words)
# Output: ['PYTHON', 'FUNCTIONAL', 'PROGRAMMING']
```

#### Method 2: Mapping Across Multiple Iterables in Parallel

`map()` accepts multiple iterables! The function will receive one argument from each iterable per step. Mapping stops as soon as the **shortest** iterable is exhausted (identical to `zip()`):

```python
# Math: pow(base, exponent)
bases = [10, 20, 30, 40]
powers = [1, 2, 3]  # Note: only 3 items

# Computes: pow(10, 1), pow(20, 2), pow(30, 3)
powers_result = list(map(pow, bases, powers))
print(powers_result)
# Output: [10, 400, 27000]

# Element-wise addition of two lists
list_a = [1, 2, 3]
list_b = [10, 20, 30]
sums = list(map(lambda x, y: x + y, list_a, list_b))
print(sums)
# Output: [11, 22, 33]
```

#### Method 3: `itertools.starmap()` for Pre-Grouped Tuples

When your arguments are already bundled together in tuples (e.g. `[(2, 5), (3, 2), (10, 3)]`), standard `map()` passes the whole tuple as a single argument. Use `itertools.starmap()` to unpack each tuple into separate arguments (equivalent to `func(*args)`):

```python
from itertools import starmap

pairs = [(2, 5), (3, 2), (10, 3)]
powers = list(starmap(pow, pairs))
print(powers)
# Output: [32, 9, 1000]
```

---

## 2. The Iterator Trap: Why Did My Iterator Turn Empty?

In `db2.py`, you noticed this behavior:

```python
farenheit_temps = map(c_to_f, celcius_temps)

for ftemp in farenheit_temps:
    print(ftemp)

print(list(farenheit_temps))
# Output: []
```

### Why does `list(farenheit_temps)` return `[]`?

1. **Iterators are Single-Pass Data Streams**: Unlike a list, an iterator does **not** store all elements in memory. It holds a cursor and produces items on the fly using Python's `__next__()` protocol.
2. **Consumption**: When the `for` loop ran, it called `next()` on `farenheit_temps` repeatedly until all elements were yielded. The iterator then raised `StopIteration` internally, marking it as **exhausted**.
3. **No Automatic Rewind**: Iterators cannot be rewound or restarted. Once exhausted, calling `list(farenheit_temps)` asks for any remaining items. Since there are none left, it yields `[]`.

```text
Iterables vs Iterators:

List (Container in RAM):
[ 32.0, 77.0, 214.25, 194.45, 164.75 ] ◄── Can be read unlimited times

Map Object (One-way lazy pipeline):
[0.0, 10.0, ...] ──► c_to_f() ──► Yield 32.0 ──► Yield 77.0 ──► ... ──► [Exhausted!]
                                                                             │
                                                                   list(...) == []
```

### Practical Solutions

- **If you need multiple passes**: Convert to a list immediately: `farenheit_temps = list(map(c_to_f, celcius_temps))`.
- **If the dataset is too big for memory**: Keep it as an iterator, or use `itertools.tee(iterator, 2)` to split the stream into two independent, lazy iterators without loading everything into memory.

---

## 3. `filter()`: Selecting Elements That Pass a Test

### 3.1 Concept & Syntax

`filter()` is a Python **built-in** function that selects elements from an iterable based on whether a function evaluates to `True` or `False`.

```python
filter(function, iterable)
```

- **Predicate Function**: The function passed to `filter()` must return a boolean value (`True` or `False`, or a truthy/falsy value).
- **Behavior**: If `function(item)` is `True`, `item` is kept; if `False`, it is discarded.
- **Returns**: A lazy iterator (`<filter object>`).

---

### 3.2 Code from `db2.py` and the `map` vs. `filter` Discovery

In Section 2 of `db2.py`:

```python
grades = [65, 90, 77, 78, 69]

def is_fcd(grade):
    # First Class with Distinction criteria (> 75)
    return grade > 75
```

If we run `map(is_fcd, grades)`:

```python
fcd_grades = map(is_fcd, grades)
print(list(fcd_grades))
# Output: [False, True, True, True, False]
```

Notice what happened: `map` transformed each number into a boolean (`True` or `False`), returning all 5 answers!

To **extract only the student scores that scored distinction**, we use `filter(is_fcd, grades)`:

```python
# filter() checks each element and retains only those where is_fcd is True:
fcd_grades = filter(is_fcd, grades)

print(fcd_grades)
# Output: <filter object at 0x1072bbb00>

# First consumption
for grade in fcd_grades:
    print(grade)
# Output:
# 90
# 77
# 78

# Exhausted check:
print(list(fcd_grades))
# Output: [] (Like map, filter iterators can only be consumed once!)

# Immediate conversion:
print(list(filter(is_fcd, grades)))
# Output: [90, 77, 78]

# Using lambda:
print(list(filter(lambda grade: grade > 75, grades)))
# Output: [90, 77, 78]
```

---

### 3.3 Other Ways to Invoke `filter()` & Popular Real-World Usages

#### Method 1: The "Truthiness" Filter with `None` (Extremely Popular!)

If you pass `None` as the first argument to `filter()`, Python uses the identity truth-test. It strips out all "falsy" values (`0`, `""`, `None`, `False`, `[]`, `{}`):

```python
raw_entries = ["user123", "", None, "admin", 0, False, "moderator", []]

# Passing None automatically cleans out all empty/falsy values!
valid_users = list(filter(None, raw_entries))
print(valid_users)
# Output: ['user123', 'admin', 'moderator']
```

#### Method 2: Filtering Dictionaries and Complex Data Records

`filter()` is widely used when querying collections of dictionaries, records, or dataclasses:

```python
employees = [
    {"name": "Alice", "dept": "Engineering", "active": True},
    {"name": "Bob", "dept": "HR", "active": False},
    {"name": "Charlie", "dept": "Engineering", "active": False},
    {"name": "Diana", "dept": "Engineering", "active": True},
]

# Keep only active employees in Engineering
active_engineers = list(filter(
    lambda emp: emp["dept"] == "Engineering" and emp["active"],
    employees
))

print(active_engineers)
# Output: [{'name': 'Alice', 'dept': 'Engineering', 'active': True}, {'name': 'Diana', 'dept': 'Engineering', 'active': True}]
```

#### Method 3: Inverting the Condition with `itertools.filterfalse()`

If you want to keep elements where the condition is `False`, instead of writing `lambda x: not func(x)`, Python provides `itertools.filterfalse()`:

```python
from itertools import filterfalse

grades = [65, 90, 77, 78, 69]

# Keep students who did NOT get distinction (grade <= 75)
non_fcd = list(filterfalse(lambda g: g > 75, grades))
print(non_fcd)
# Output: [65, 69]
```

---

## 4. The Common Gotcha: `map()` vs. `filter()`

A classic beginner mistake is mixing up `map()` and `filter()` when using a boolean check:

```python
numbers = [10, 15, 20, 25, 30]

# map() TRANSFORMS every element into the function's return value:
print(list(map(lambda x: x > 20, numbers)))
# Output: [False, False, False, True, True]  <-- Length is still 5!

# filter() KEEPS the original elements that evaluate to True:
print(list(filter(lambda x: x > 20, numbers)))
# Output: [25, 30]                           <-- Length is 2!
```

### Side-by-Side Comparison

| Feature                           | `map(func, iterable)`                        | `filter(func, iterable)`                        |
| :-------------------------------- | :------------------------------------------- | :---------------------------------------------- |
| **Primary Goal**                  | **Transform** elements                       | **Select** a subset of elements                 |
| **Output Length**                 | Always **identical** to input length         | **Less than or equal** to input length          |
| **What Result Contains**          | The return values: `func(item)`              | The original items where `func(item)` is `True` |
| **When given `lambda x: x > 75`** | Returns booleans: `[False, True, True, ...]` | Returns matching items: `[90, 77, 78]`          |

---

## 5. `reduce()`: Aggregating to a Single Value

### 5.1 Concept & Syntax

`reduce()` repeatedly applies a two-argument function to elements of a sequence from left to right, **reducing (or folding)** the entire collection into a single summary result.

```python
from functools import reduce

reduce(function, iterable[, initial])
```

> [!IMPORTANT]
> **Why is `reduce()` in `functools` instead of a built-in?**  
> In Python 2, `reduce()` was a built-in function. In Python 3, Guido van Rossum moved it to `functools` because most everyday reductions are clearer, faster, and more readable using dedicated built-in functions like `sum()`, `min()`, `max()`, `any()`, and `all()`.

---

### 5.2 Code from `db2.py` (Sum of Prices)

```python
from functools import reduce

prices = [44.6, 32.5, 50.0, 22.2]

# Note: Defining a function named 'sum' shadows Python's built-in sum()!
# In production, name it 'add' or 'my_sum'.
def add(x, y):
    return x + y

sum_of_prices = reduce(add, prices)

print(sum_of_prices)
# Output: 149.29999999999998

# Using an anonymous lambda:
print(reduce(lambda x, y: x + y, prices))
# Output: 149.29999999999998
```

---

### 5.3 How `reduce()` Works Internally: The Accumulator

`reduce()` maintains an internal running state called the **accumulator**:

```text
Sequence: [44.6, 32.5, 50.0, 22.2]

Iteration 1:
  Takes first 2 items: 44.6 and 32.5
  add(44.6, 32.5) ──────────────► 77.1   (Accumulator)

Iteration 2:
  Takes accumulator (77.1) and next item (50.0)
  add(77.1, 50.0) ──────────────► 127.1  (Accumulator)

Iteration 3:
  Takes accumulator (127.1) and next item (22.2)
  add(127.1, 22.2) ─────────────► 149.3  (Final Return Value!)
```

---

### 5.4 Using the `operator` Module (Cleaner & Faster)

Writing `lambda x, y: x + y` creates a Python function object. Python's built-in `operator` module provides C-level performance functions:

```python
from functools import reduce
import operator

prices = [44.6, 32.5, 50.0, 22.2]

# operator.add is faster and more Pythonic than a lambda:
total = reduce(operator.add, prices)
print(total)
# Output: 149.29999999999998
```

---

## 6. The Power of the `initial` Value in `reduce()`

The optional 3rd argument, `initial`, fundamentally enhances `reduce()`.

```python
reduce(function, iterable, initial)
```

When `initial` is supplied:

1. The accumulator starts with `initial` instead of the first list item.
2. The loop runs for **all** items (starting from index 0).

```python
from functools import reduce

prices = [44.6, 32.5, 50.0, 22.2]

# Add a flat $10 shipping fee at the start:
total_with_shipping = reduce(lambda acc, p: acc + p, prices, 10.0)
print(total_with_shipping)
# Output: 159.29999999999998
```

### 6.1 Why `initial` is Critical: Preventing the Empty Sequence Crash

Calling `reduce()` without `initial` on an empty collection raises a runtime `TypeError`:

```python
from functools import reduce

empty_data = []

# CRASH:
# reduce(lambda x, y: x + y, empty_data)
# TypeError: reduce() of empty sequence with no initial value

# SAFE:
safe_sum = reduce(lambda x, y: x + y, empty_data, 0)
print(safe_sum)
# Output: 0
```

---

### 6.2 Popular Advanced Patterns with `reduce()`

#### Pattern 1: Finding Maximum or Minimum

```python
from functools import reduce

nums = [19, 82, 34, 99, 56, 12]
max_val = reduce(lambda a, b: a if a > b else b, nums)
print(max_val)
# Output: 99
```

#### Pattern 2: Calculating Factorial / Cumulative Product

```python
from functools import reduce
import operator

# 5! = 1 * 2 * 3 * 4 * 5
fact_5 = reduce(operator.mul, range(1, 6))
print(fact_5)
# Output: 120
```

#### Pattern 3: Flattening a List of Lists

```python
from functools import reduce

nested = [[1, 2, 3], [4, 5], [6, 7, 8]]
flat = reduce(lambda acc, sublist: acc + sublist, nested, [])
print(flat)
# Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

#### Pattern 4: Deep Dictionary / JSON Key Traversal

Safe, elegant traversal of nested dictionaries using `reduce`:

```python
from functools import reduce

payload = {
    "user": {
        "profile": {
            "contact": {
                "email": "user@example.com"
            }
        }
    }
}

path = ["user", "profile", "contact", "email"]

# Navigates step by step: payload['user'] -> ['profile'] -> ['contact'] -> ['email']
email = reduce(lambda current_dict, key: current_dict[key], path, payload)
print(email)
# Output: user@example.com
```

---

## 7. `reduce()` vs. `itertools.accumulate()`

A common question: _"What if I want to see the intermediate running totals, not just the final total?"_

- `reduce()` returns only the **final aggregated scalar**.
- `itertools.accumulate()` returns a **running iterator** containing every intermediate step:

```python
from functools import reduce
from itertools import accumulate

prices = [44.6, 32.5, 50.0, 22.2]

# Final total:
print(reduce(lambda x, y: x + y, prices))
# Output: 149.29999999999998

# Running totals at each step:
print(list(accumulate(prices, lambda x, y: x + y)))
# Output: [44.6, 77.1, 127.1, 149.29999999999998]
```

---

## 8. Building a Full Data Pipeline: Filter $\rightarrow$ Map $\rightarrow$ Reduce

In data processing pipelines (ETL jobs, stream analytics, Big Data with MapReduce / Spark), these three operations are chained together:

```text
Raw Records ──► [ filter() ] ──► [ map() ] ──► [ reduce() ] ──► Final Summary Metric
```

### End-to-End Example: E-Commerce Transaction Report

```python
from functools import reduce

transactions = [
    {"id": 1, "item": "Laptop",   "amount": 1200.0, "status": "completed"},
    {"id": 2, "item": "Mouse",    "amount": 25.0,   "status": "refunded"},
    {"id": 3, "item": "Monitor",  "amount": 300.0,  "status": "completed"},
    {"id": 4, "item": "Keyboard", "amount": 80.0,   "status": "completed"},
    {"id": 5, "item": "Desk",     "amount": 450.0,  "status": "pending"},
]

# Step 1: FILTER completed transactions only
completed = filter(lambda t: t["status"] == "completed", transactions)

# Step 2: MAP each transaction to apply an 8% state sales tax
taxed_totals = map(lambda t: t["amount"] * 1.08, completed)

# Step 3: REDUCE to calculate the total company earnings
grand_total = reduce(lambda acc, amt: acc + amt, taxed_totals, 0.0)

print(f"Total Revenue (incl. tax): ${grand_total:.2f}")
# Output: Total Revenue (incl. tax): $1706.40
```

---

## 9. Cheat Sheet & Decision Matrix: Functional Tools vs. Comprehensions

In modern idiomatic Python, you can write many `map` and `filter` tasks using **List Comprehensions** or **Generator Expressions**.

### Syntax Translation Table

| Operation              | Functional Tool                                | Python Comprehension / Built-in             |
| :--------------------- | :--------------------------------------------- | :------------------------------------------ |
| **Transform**          | `list(map(lambda x: x * 2, nums))`             | `[x * 2 for x in nums]`                     |
| **Filter**             | `list(filter(lambda x: x > 0, nums))`          | `[x for x in nums if x > 0]`                |
| **Transform & Filter** | `list(map(f, filter(p, nums)))`                | `[f(x) for x in nums if p(x)]`              |
| **Sum**                | `reduce(operator.add, nums, 0)`                | `sum(nums)` _(Recommended)_                 |
| **Max / Min**          | `reduce(lambda a, b: a if a > b else b, nums)` | `max(nums)` / `min(nums)` _(Recommended)_   |
| **Truth Check**        | `reduce(lambda a, b: a or b, flags)`           | `any(flags)` / `all(flags)` _(Recommended)_ |

### Decision Guide: When Should You Use Which?

1. **Use `map()` when:**
   - Applying a pre-existing function or type-caster without a lambda: `map(int, inputs)`, `map(str.lower, words)`. This is concise and faster in CPython.
   - Processing multiple iterables simultaneously: `map(pow, bases, exps)`.
2. **Use Comprehensions when:**
   - Doing arithmetic or logic involving lambda: `[x**2 + 5 for x in data]` is far more readable than `map(lambda x: x**2 + 5, data)`.
   - Combining filter and map: `[x.upper() for x in words if len(x) > 3]`.
3. **Use Built-ins instead of `reduce()` when:**
   - Performing standard numeric calculations: `sum()`, `math.prod()`, `min()`, `max()`.
   - Performing logical aggregations: `any()`, `all()`.
