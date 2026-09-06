# Python Modules & Packages: A Beginner-Friendly Guide

_Learn how to organize Python code, create packages, use `__init__.py`, and understand `if __name__ == '__main__'`. Simple explanations, clear code, and real folder structures._

---

## Table of Contents

- [1. Module vs. Package: What's the Difference?](#1-module-vs-package-whats-the-difference)
- [2. The Purpose of `__init__.py`](#2-the-purpose-of-__init__py)
  - [2.1 Running Setup Code Automatically](#21-running-setup-code-automatically)
  - [2.2 Making Imports Shorter & Cleaner](#22-making-imports-shorter--cleaner)
  - [2.3 Controlling Wildcard Imports with `__all__`](#23-controlling-wildcard-imports-with-__all__)
- [3. Absolute vs. Relative Imports](#3-absolute-vs-relative-imports)
  - [3.1 Absolute Imports (From the Root)](#31-absolute-imports-from-the-root)
  - [3.2 Relative Imports (Using Dots)](#32-relative-imports-using-dots)
- [4. The Common Beginner Trap: Relative Import Error](#4-the-common-beginner-trap-relative-import-error)
- [5. Hands-On Mini Project: A Simple Helpers Package](#5-hands-on-mini-project-a-simple-helpers-package)
- [6. Cheat Sheet: Quick Rules to Remember](#6-cheat-sheet-quick-rules-to-remember)
- [7. What Does `if __name__ == '__main__'` Do in Python?](#7-what-does-if-__name__--__main__-do-in-python)
  - [7.1 The Problem: Code Runs Automatically on Import](#71-the-problem-code-runs-automatically-on-import)
  - [7.2 The Solution: The `__name__` Variable](#72-the-solution-the-__name__-variable)
  - [7.3 The Guard Block: `if __name__ == '__main__':`](#73-the-guard-block-if-__name__--__main__)
  - [7.4 Side-by-Side Example](#74-side-by-side-example)
  - [7.5 Best Practice: The `main()` Function](#75-best-practice-the-main-function)

---

## 1. Module vs. Package: What's the Difference?

- **Module**: A single `.py` file containing Python code.
  - Think of a module like a **single tool** (e.g., a screwdriver).
  - Example: `math_tools.py`
- **Package**: A folder that groups multiple modules together, usually containing an `__init__.py` file.
  - Think of a package like a **toolbox** containing many tools.
  - Example: A folder named `helpers/` containing `math_tools.py` and `text_tools.py`.

### Folder Structure Comparison

```text
Single Modules (Loose Files)        A Package (Organized Folder)
----------------------------        ----------------------------
my_project/                         my_project/
├── main.py                         ├── main.py
├── math_tools.py                   └── helpers/             <-- Package folder
└── text_tools.py                       ├── __init__.py      <-- Tells Python it's a package
                                        ├── math_tools.py    <-- Module
                                        └── text_tools.py    <-- Module
```

> **Do you still need `__init__.py`?**
> In modern Python (3.3+), a folder without `__init__.py` still works (called a _namespace package_). However, **always add `__init__.py`** to regular packages. It makes your code explicit, works with all tools, and lets you customize how the package is imported.

---

## 2. The Purpose of `__init__.py`

The `__init__.py` file sits inside your package folder. It does two big jobs:

```text
helpers/
├── __init__.py        <-- Runs whenever someone imports from "helpers"
├── math_tools.py
└── text_tools.py
```

### 2.1 Running Setup Code Automatically

Whenever you import a package, Python runs the code inside `__init__.py` **first**, and only **once**.

```python
# helpers/__init__.py
print("Helpers package is loaded!")
```

```python
# main.py
import helpers.math_tools
import helpers.text_tools

print("Main script running.")
```

**Output:**

```text
Helpers package is loaded!
Main script running.
```

Notice `"Helpers package is loaded!"` printed only once, even though we imported two different modules.

---

### 2.2 Making Imports Shorter & Cleaner

Without `__init__.py`, people using your package have to type long import paths:

```python
# Long and clunky:
from helpers.math_tools import add
from helpers.text_tools import greet
```

By re-exporting those functions inside `helpers/__init__.py`, you give your users a **shortcut**:

```python
# helpers/__init__.py
from .math_tools import add
from .text_tools import greet
```

Now, anyone using your package can import directly from the folder name:

```python
# main.py
# Clean and simple:
from helpers import add, greet

print(add(2, 3))         # 5
print(greet("Alice"))    # Hello, Alice!
```

---

### 2.3 Controlling Wildcard Imports with `__all__`

If someone writes `from helpers import *`, Python will import everything by default. You can use `__all__` to only share what you want:

```python
# helpers/__init__.py
from .math_tools import add

# Only 'add' will be imported with "import *"
__all__ = ["add"]
```

---

## 3. Absolute vs. Relative Imports

When you have multiple files inside a project, they often need to talk to each other. You have two ways to import them:

```text
my_project/
├── main.py
└── my_app/
    ├── __init__.py
    ├── math_tools.py
    └── greetings.py
```

### 3.1 Absolute Imports (From the Root)

An **absolute import** writes out the full path starting from the project root:

```python
# Inside greetings.py:
from my_app.math_tools import add
```

- **Pros**: Very clear. Anyone reading the code immediately knows where it comes from.
- **Cons**: If you rename the folder `my_app` to `app_v2`, you must update all your import paths.

---

### 3.2 Relative Imports (Using Dots)

A **relative import** looks for files based on the **current file's location** using dots (`.`):

- **`.` (one dot)**: Current folder (look for a neighbor file).
- **`..` (two dots)**: Parent folder (go up one level).

#### Simple Visual:

```text
my_app/
├── __init__.py
├── math_tools.py     <-- Target file (neighbor)
└── greetings.py      <-- You are here!
```

Inside `greetings.py`:

```python
# Look in the same folder (.) for math_tools:
from .math_tools import add
```

#### Going Up One Folder (`..`):

```text
my_project/
├── utils/
│   ├── __init__.py
│   └── helper.py     <-- Target file
└── features/
    ├── __init__.py
    └── welcome.py    <-- You are here!
```

Inside `welcome.py`:

```python
# Go up one folder (..), then into utils -> helper:
from ..utils.helper import shout
```

---

## 4. The Common Beginner Trap: Relative Import Error

If you try to run a file that contains relative imports directly:

```bash
$ python my_app/greetings.py
```

You will get this scary error:

```text
ImportError: attempted relative import with no known parent package
```

### Why does this happen?

When you run a file directly with `python filename.py`, Python sets that file's name to `"__main__"` and does not know what folder or package it belongs to. When it sees `from .math_tools`, it gets confused because it does not know where the "current package" is.

### The Easy Fix:

1. **Always run your main script from the root folder:**
   ```bash
   python main.py
   ```
2. **Or use the `-m` (module) flag:**
   ```bash
   python -m my_app.greetings
   ```

---

## 5. Hands-On Mini Project: A Simple Helpers Package

Let's build a tiny 4-file project to see it all work together.

### 5.1 The Folder Structure

```text
mini_project/
├── main.py
└── tools/
    ├── __init__.py
    ├── calculator.py
    └── formatter.py
```

### 5.2 The Code

#### 1. `tools/calculator.py`

```python
"""Simple math functions."""

def add(x, y):
    return x + y

def square(x):
    return x * x
```

#### 2. `tools/formatter.py`

Notice how this file imports `square` from its neighbor file `calculator.py` using `.`:

```python
"""Text formatting that uses calculator functions."""

from .calculator import square

def show_square(number):
    result = square(number)
    return f"The square of {number} is {result}."
```

#### 3. `tools/__init__.py`

Make our favorite functions easy to import:

```python
"""Package shortcut file."""

from .calculator import add
from .formatter import show_square
```

#### 4. `main.py`

Run our program from the root:

```python
# Import cleanly using the package shortcuts:
from tools import add, show_square

print(f"2 + 3 = {add(2, 3)}")
print(show_square(5))
```

### 5.3 Run It!

Run `main.py` from your terminal:

```bash
$ python main.py
```

**Output:**

```text
2 + 3 = 5
The square of 5 is 25.
```

---

## 6. Cheat Sheet: Quick Rules to Remember

| Concept                   | Rule                                                    | Example                            |
| :------------------------ | :------------------------------------------------------ | :--------------------------------- |
| **Module**                | One file.                                               | `calculator.py`                    |
| **Package**               | A folder with an `__init__.py`.                         | `tools/`                           |
| **`__init__.py`**         | Runs once on import; gives clean shortcuts.             | `from .calculator import add`      |
| **Absolute Import**       | Full path from root.                                    | `from tools.calculator import add` |
| **Relative Import**       | Uses dots (`.` = same folder, `..` = parent).           | `from .calculator import add`      |
| **Relative Import Error** | Don't run submodules directly; run `main.py` from root. | `python main.py`                   |

---

## 7. What Does `if __name__ == '__main__'` Do in Python?

_Based on the tutorial by Tech With Tim._

### 7.1 The Problem: Code Runs Automatically on Import

When you import a file in Python, Python reads and **runs every line of code in that file from top to bottom**.

If your file has test code or `print()` statements at the bottom, they will run immediately when someone imports your file.

#### Example of the Problem:

```python
# math_tools.py
def add(a, b):
    return a + b

# You added this to test your function:
print("Testing add function: 2 + 2 =", add(2, 2))
```

Now you try to use `add` in another file:

```python
# app.py
from math_tools import add

print("Welcome to my app!")
```

When you run `python app.py`, you get:

```text
Testing add function: 2 + 2 = 4
Welcome to my app!
```

The test code ran even though `app.py` only wanted to import the function!

### 7.2 The Solution: The `__name__` Variable

Python automatically creates a hidden variable named `__name__` for every file.

> **Note**: Variables with two underscores like `__name__` are called **"dunder"** variables (short for **D**ouble **UNDER**score).

Python sets `__name__` to different values depending on **how you ran the file**:

1. **If you run the file directly** (`python math_tools.py`):
   - Python sets `__name__ = "__main__"`
2. **If the file is imported** (`import math_tools`):
   - Python sets `__name__ = "math_tools"` (the module's actual name)

### 7.3 The Guard Block: `if __name__ == '__main__':`

By adding an `if` statement, you can make sure test or startup code **only runs when you run that file directly**:

```python
if __name__ == "__main__":
    # This code ONLY runs when you run this file directly!
    # It will NOT run when this file is imported elsewhere.
```

- **Run directly**: `__name__` is `"__main__"` -> Condition is **True** -> Code runs.
- **Imported**: `__name__` is `"math_tools"` -> Condition is **False** -> Code is skipped.

### 7.4 Side-by-Side Example

#### Updated `math_tools.py`:

```python
# math_tools.py
def add(a, b):
    return a + b

# Guard block:
if __name__ == "__main__":
    print("Running directly! Testing add: 2 + 2 =", add(2, 2))
```

#### Consumer File `app.py`:

```python
# app.py
from math_tools import add

print("Welcome to my app!")
print("10 + 5 =", add(10, 5))
```

#### What Happens in the Terminal:

1. **Run `math_tools.py` directly:**

   ```bash
   $ python math_tools.py
   Running directly! Testing add: 2 + 2 = 4
   ```

   _(The test code runs!)_

2. **Run `app.py`:**
   ```bash
   $ python app.py
   Welcome to my app!
   10 + 5 = 15
   ```
   _(The test code is ignored! Clean and perfect.)_

### 7.5 Best Practice: The `main()` Function

Instead of putting lots of code directly inside the `if` block, standard Python convention is to create a `main()` function:

```python
def add(a, b):
    return a + b

def main():
    # Put your startup/test code here
    print("Testing:", add(5, 5))

if __name__ == "__main__":
    main()
```

#### Why do this?

- **Keeps variables clean**: Variables created inside `main()` won't accidentally leak as global variables.
- **Easy to read**: Other developers can immediately see where your program starts.
