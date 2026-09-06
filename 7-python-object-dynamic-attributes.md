# Dynamic Attributes in Python: A Beginner-Friendly Guide

_Learn how to read, write, check, and delete object attributes using strings with `getattr`, `setattr`, `hasattr`, and `delattr`._

---

## Table of Contents

- [1. The Problem: Dot Notation vs. Strings](#1-the-problem-dot-notation-vs-strings)
- [2. The 4 Core Functions](#2-the-4-core-functions)
  - [2.1 `getattr()`: Read an Attribute by String](#21-getattr-read-an-attribute-by-string)
  - [2.2 `setattr()`: Change or Add an Attribute by String](#22-setattr-change-or-add-an-attribute-by-string)
  - [2.3 `hasattr()`: Check if an Attribute Exists](#23-hasattr-check-if-an-attribute-exists)
  - [2.4 `delattr()`: Delete an Attribute by String](#24-delattr-delete-an-attribute-by-string)
- [3. Real-World Example: Loading Settings from a Dictionary](#3-real-world-example-loading-settings-from-a-dictionary)
- [4. Quick Cheat Sheet](#4-quick-cheat-sheet)

---

## 1. The Problem: Dot Notation vs. Strings

Normally in Python, you access an object's data using **dot notation**:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 25)

# Normal static access:
print(p.name)  # Alice
print(p.age)   # 25
```

### But what if the attribute name is inside a variable?

Imagine a user types `"name"` or `"age"` into an input prompt:

```python
choice = "age"  # A string!
```

- In a **dictionary**, you can look up keys with strings: `my_dict[choice]`.
- But with **objects**, `p[choice]` gives a `TypeError`!

Without dynamic tools, you would have to write messy `if-elif` chains:

```python
# The ugly way (hard to scale):
if choice == "name":
    print(p.name)
elif choice == "age":
    print(p.age)
else:
    print("Not found")
```

Python solves this with **4 built-in functions** that let you work with attributes using string names at runtime (**dynamic attribute handling**).

---

## 2. The 4 Core Functions

Here is our base object for all examples:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 25)
```

---

### 2.1 `getattr()`: Read an Attribute by String

Use `getattr()` to get the value of an attribute when you have its name as a string.

```python
getattr(object, "attribute_name", default_value)
```

#### Example:

```python
choice = "name"

# Replaces p.name:
print(getattr(p, choice))  # Output: Alice

# If the attribute doesn't exist, provide a fallback default:
print(getattr(p, "height", "Not found"))  # Output: Not found
```

> **Tip**: If you do not give a default value and the attribute doesn't exist, Python raises an `AttributeError`. Always provide a default value if you aren't sure!

---

### 2.2 `setattr()`: Change or Add an Attribute by String

Use `setattr()` to modify an existing attribute or create a brand new one.

```python
setattr(object, "attribute_name", new_value)
```

#### Example:

```python
# 1. Update an existing attribute:
setattr(p, "age", 26)
print(p.age)  # Output: 26

# 2. Add a brand new attribute on the fly:
setattr(p, "city", "New York")
print(p.city)  # Output: New York
```

---

### 2.3 `hasattr()`: Check if an Attribute Exists

Use `hasattr()` to safely check if an object has a certain attribute before doing something with it. It returns `True` or `False`.

```python
hasattr(object, "attribute_name")
```

#### Example:

```python
print(hasattr(p, "name"))    # Output: True
print(hasattr(p, "salary"))  # Output: False

# Safe check before accessing:
if hasattr(p, "city"):
    print(f"City is {p.city}")
```

---

### 2.4 `delattr()`: Delete an Attribute by String

Use `delattr()` to remove an attribute from an object at runtime.

```python
delattr(object, "attribute_name")
```

#### Example:

```python
# Delete the age attribute:
delattr(p, "age")

# Now checking if it exists:
print(hasattr(p, "age"))  # Output: False

# Trying to access it now will raise an error:
# print(p.age)  # AttributeError: 'Person' object has no attribute 'age'
```

---

## 3. Real-World Example: Loading Settings from a Dictionary

A classic real-world scenario is converting raw data (like JSON or database rows) into an object:

```python
class AppConfig:
    pass  # Starts empty

# Settings loaded from a config file or API:
user_settings = {
    "theme": "dark",
    "font_size": 16,
    "notifications": True
}

config = AppConfig()

# Dynamically attach every key/value pair as an attribute:
for key, value in user_settings.items():
    setattr(config, key, value)

# Now access them naturally:
print(config.theme)          # Output: dark
print(config.font_size)      # Output: 16
print(config.notifications)  # Output: True
```

---

## 4. Quick Cheat Sheet

| Function                          | What it Does                   | Example                 | Equivalent to    |
| :-------------------------------- | :----------------------------- | :---------------------- | :--------------- |
| **`getattr(obj, name, default)`** | **Reads** an attribute         | `getattr(p, "age", 0)`  | `p.age`          |
| **`setattr(obj, name, val)`**     | **Sets/Adds** an attribute     | `setattr(p, "age", 26)` | `p.age = 26`     |
| **`hasattr(obj, name)`**          | **Checks** if attribute exists | `hasattr(p, "age")`     | `True` / `False` |
| **`delattr(obj, name)`**          | **Deletes** an attribute       | `delattr(p, "age")`     | `del p.age`      |
