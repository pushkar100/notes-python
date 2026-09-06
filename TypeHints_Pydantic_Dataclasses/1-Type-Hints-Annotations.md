# Python Typing - Type Hints & Annotations

**Based on the Tech With Tim Tutorial**

- [Introduction](#introduction)
  - [Common Issues Without Type Hints (and How Annotations Help)](#common-issues-without-type-hints-and-how-annotations-help)
- [Basic Type Annotations](#basic-type-annotations)
  - [Why Doesn't `x: str = 1` Crash at Runtime? (Under the Hood)](#why-doesnt-x-str-1-crash-at-runtime-under-the-hood)
- [Where Do Types Come From in Python? (The Complete Set)](#where-do-types-come-from-in-python-the-complete-set)
  - [1. Built-in Core Types (No Imports Required)](#1-built-in-core-types-no-imports-required)
  - [2. Python's `typing` Standard Library Module](#2-pythons-typing-standard-library-module)
  - [3. Custom & User-Defined Types](#3-custom-user-defined-types)
- [Function Type Annotations](#function-type-annotations)
  - [Basic Syntax](#basic-syntax)
  - [Detailed Breakdown & Examples of Function Annotations](#detailed-breakdown-examples-of-function-annotations)
- [Static Code Analysis with MyPy](#static-code-analysis-with-mypy)
  - [Practical MyPy Execution Examples & Errors Caught](#practical-mypy-execution-examples-errors-caught)
- [The `typing` Module](#the-typing-module)
  - [1. Collections (Lists, Dicts, Sets, Tuples)](#1-collections-lists-dicts-sets-tuples)
  - [2. Custom Types (Aliases)](#2-custom-types-aliases)
  - [3. Special Typing Types](#3-special-typing-types)
- [Union Type Annotations (`Union` & `|`)](#union-type-annotations-union)
  - [Syntax](#syntax)
  - [Examples of `Union`](#examples-of-union)
- [Literal Type Annotations (`Literal`)](#literal-type-annotations-literal)
  - [Why Use `Literal`?](#why-use-literal)
  - [Examples of `Literal`](#examples-of-literal)
- [Final Type Annotations (`Final` & `@final`)](#final-type-annotations-final-final)
  - [Why Use `Final`?](#why-use-final)
  - [Examples of `Final`](#examples-of-final)
- [Generics with `TypeVar`](#generics-with-typevar)
  - [Why Use `TypeVar` Instead of `Any`?](#why-use-typevar-instead-of-any)
  - [Function Definition](#function-definition)
  - [Example Invocations & Output](#example-invocations-output)
  - [Error Cases (Caught by MyPy & Runtime)](#error-cases-caught-by-mypy-runtime)
  - [Advanced: Constrained `TypeVar` (Restricting Allowed Types)](#advanced-constrained-typevar-restricting-allowed-types)

## Introduction

Python is a dynamically typed programming language. By design, you aren't required to declare variable types when writing code—Python inspects and determines types at runtime. While this design offers tremendous speed and flexibility during early development, it can become a double-edged sword as projects grow. Without explicit types, developers often find themselves asking: _What data structure does this function parameter expect? Could this function return `None`? Why is this line crashing in production with a `TypeError`?_

To solve these problems without compromising Python's dynamic runtime, Python 3.5 introduced **Type Hints** and **Type Annotations** (PEP 484).

Type annotations allow you to explicitly declare the expected data types for variables, function arguments, and return values directly in your source code. Crucially, **type hints do not alter Python's runtime execution behavior**. Python will not throw a runtime crash simply because a variable receives an unexpected type. Instead, type annotations serve two major purposes:

1. **Machine-Readable Documentation**: They communicate intent clearly to other developers and to static analysis tools.
2. **Developer Tooling Powerhouse**: They enable IDEs (like PyCharm and VS Code) to offer accurate autocomplete, refactoring support, and instant code linting, while static analysis tools (like `mypy`) can detect type mismatches _before_ you ever run your code.

### Common Issues Without Type Hints (and How Annotations Help)

#### 1. Silent Logic Bugs & Operations on Unexpected Types

Without type hints, passing the wrong type into a function might not crash immediately, but can lead to silent, hard-to-debug logical errors.

**Without Type Hints:**

```python
def calculate_total(price, quantity):
    return price * quantity

# Intended usage: calculate_total(10.0, 3) -> 30.0
# Buggy usage: string passed instead of int or float
print(calculate_total("10.0", 3))
# Output: "10.010.010.0" (String repetition instead of math multiplication!)
```

**With Type Annotations:**

```python
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity

# Static checkers (mypy) or IDEs will instantly highlight this error before execution:
# Argument 1 to "calculate_total" has incompatible type "str"; expected "float"
print(calculate_total("10.0", 3))
```

#### 2. Unhandled `None` Edge Cases (`NoneType` Errors)

Functions often return `None` when a requested item isn't found. Without annotations, developers frequently forget to handle this scenario, causing runtime crashes deep in production.

**Without Type Hints:**

```python
def get_user_email(user_id):
    users = {1: "alice@example.com"}
    return users.get(user_id)  # Returns None if user_id is not found

# Crashes at runtime if user_id 2 does not exist:
# AttributeError: 'NoneType' object has no attribute 'lower'
email = get_user_email(2)
print(email.lower())
```

**With Type Annotations:**

```python
from typing import Optional

def get_user_email(user_id: int) -> Optional[str]:
    users = {1: "alice@example.com"}
    return users.get(user_id)

email = get_user_email(2)
# IDEs and static analyzers warn that `email` could be `None`,
# forcing you to safely handle the None case before calling `.lower()`:
if email is not None:
    print(email.lower())
```

#### 3. Loss of IDE Autocomplete & Productivity

When a function accepts an object without type annotations, the IDE has no insight into the object's attributes or methods, leaving developers to guess attribute names or consult external documentation constantly.

**Without Type Hints:**

```python
def greet_user(user):
    # IDE cannot offer autocomplete after `user.` because it doesn't know what `user` is
    return f"Hello, {user.first_name} {user.last_name}"
```

**With Type Annotations:**

```python
class User:
    def __init__(self, first_name: str, last_name: str):
        self.first_name = first_name
        self.last_name = last_name

def greet_user(user: User) -> str:
    # Typing `user.` immediately triggers accurate autocomplete for `first_name` and `last_name`
    return f"Hello, {user.first_name} {user.last_name}"
```

## Basic Type Annotations

```python
# Standard assignment
x = 1

# Type hinted assignment (Syntax: variable: type = value)
x: str = "tim"
```

### Why Doesn't `x: str = 1` Crash at Runtime? (Under the Hood)

When Python executes `x: str = 1`, it **does not crash** or throw a `TypeError`. Here is why:

1. **Separation of Execution and Annotations**: When the Python interpreter reads `x: str = 1`, it splits the statement into two distinct actions:
   - **Assignment**: It evaluates `1` and assigns it to variable `x`.
   - **Metadata Storage**: It ignores `str` during execution and simply stores the type hint in a hidden dictionary called `__annotations__` (e.g., `__annotations__['x'] = str`).
2. **Zero Built-In Runtime Validation**: Python's execution engine does **not** perform any type checking while your program is running. It ignores whether the stored value (`1`) matches the label (`str`).
3. **The "Sticky Note" Analogy**: Think of a type hint like writing a sticky note on a physical box. If you write `"Shoes"` on the sticky note but put a `"Book"` inside the box, Python will happily carry the box around without complaining. Python doesn't check what's inside. Only external tools—like your **IDE** or **static type checkers (like MyPy)**—read the sticky note, inspect the contents, and alert you if there is a mismatch.

---

## Where Do Types Come From in Python? (The Complete Set)

In Python, type hints come from **three main sources**:

### 1. Built-in Core Types (No Imports Required)

These are standard Python data types built directly into the language:

- **Primitives**: `int`, `float`, `str`, `bool`, `bytes`, `complex`
- **Built-in Collections** (Python 3.9+ allows using these directly as type hints): `list`, `dict`, `set`, `tuple`, `frozenset`
- **Special Core Types**: `None` (represents empty/null values), `object` (base of all types), `range`, `slice`

```python
# --- Primitive Type Annotations ---
age: int = 25
price: float = 19.99
name: str = "Alice"
is_active: bool = True
raw_data: bytes = b"hello world"
complex_num: complex = 3 + 4j

# --- Built-in Collections (Python 3.9+) ---
scores: list[int] = [95, 88, 92]
user_roles: dict[str, str] = {"admin": "Alice", "editor": "Bob"}
unique_ids: set[int] = {101, 102, 103}
coordinates: tuple[int, int] = (10, 20)
tags: frozenset[str] = frozenset(["python", "typing"])

# --- Special Core Types ---
middle_name: None = None
anything: object = "Can hold any Python object"
pages: range = range(1, 10)
```

### 2. Python's `typing` Standard Library Module

For advanced type hinting, Python includes a built-in module named `typing` (`from typing import ...`).

> [!NOTE]
> **Do you still need to import `typing` in Python 3.9+?**
>
> 1. **No imports needed for collections (Python 3.9+)**: In Python 3.9+ (PEP 585), standard built-in collections can be parameterized directly (e.g., `list[int]`, `dict[str, int]`, `tuple[str, int]`). You no longer need to import `List`, `Dict`, `Tuple`, or `Set` from `typing`.
> 2. **No imports needed for `Union` & `Optional` (Python 3.10+)**: In Python 3.10+ (PEP 604), you can use the `|` pipe operator (e.g., `str | int` instead of `Union[str, int]`, and `str | None` instead of `Optional[str]`).
> 3. **Imports still required for special constructs**: Specialized features such as `Any`, `Callable`, `Literal`, `TypeVar`, `Generic`, `Sequence`, and `Iterable` are **not** built-in keywords and must still be imported from `typing` (`from typing import Any, Callable`).
> 4. **Why your script executes without imports at runtime**: Python's execution engine ignores type annotations during runtime execution. Python won't raise a runtime crash simply because a type annotation is present. Built-in types like `list[int]` are natively recognized by the Python 3.9+ parser, so no import is needed for them to work cleanly in both execution and static analysis!

- **Special Type Wrappers**:
  - `Union[T1, T2]` (or `T1 | T2` in Python 3.10+): Variable can be _either_ type `T1` or `T2`.
  - `Optional[T]`: Short for `Union[T, None]` (variable can be type `T` or `None`).
  - `Any`: Bypasses type checking entirely for a variable.
  - `Literal["val1", "val2"]`: Restricts a variable to specific exact values.
  - `Final`: Declares a constant that cannot be re-assigned or overridden.
- **Functions & Behavior**:
  - `Callable[[Arg1Type, Arg2Type], ReturnType]`: Describes functions, lambdas, or methods.
- **Abstract Data Types & Interfaces**:
  - `Sequence`: Any ordered indexable collection (e.g., `list`, `tuple`, `str`).
  - `Iterable`: Anything that can be looped over with a `for` loop.
  - `Mapping`: Any key-value mapping (e.g., `dict`).
- **Generics**:
  - `TypeVar`, `Generic`: Used to build reusable, type-safe generic functions and classes.

### 3. Custom & User-Defined Types

You can use any custom structure as a valid type hint:

- **Classes**: Any class you define (e.g., `class User: ...` can be used as `user: User`).
- **Type Aliases**: Renaming complex types for readability (e.g., `UserId = int`).
- **Dataclasses & Pydantic Models**: Data models defined using `@dataclass` or Pydantic `BaseModel`.
- **Enums**: Standard Python `enum.Enum` classes.

---

## Function Type Annotations

In Python, function type annotations specify two key pieces of information:

1. **Parameter Types**: What data types the function expects for each argument.
2. **Return Type**: What data type the function promises to return using the `->` (arrow) syntax.

### Basic Syntax

```python
def function_name(parameter1: Type1, parameter2: Type2) -> ReturnType:
    # function body
    return value
```

### Detailed Breakdown & Examples of Function Annotations

#### 1. Standard Function Annotations

Annotating simple input parameters and return types:

```python
def add_numbers(a: int, b: int) -> int:
    return a + b

def format_greeting(name: str, age: int) -> str:
    return f"Hello {name}, you are {age} years old."
```

#### 2. Functions with Default Parameter Values

When combining default parameter values with type annotations, place the default value **after** the type annotation (`parameter: Type = default_value`):

```python
def calculate_discount(price: float, discount: float = 0.10) -> float:
    return price * (1.0 - discount)

# Called with default discount (0.10)
final_price = calculate_discount(100.0)  # Returns 90.0
```

#### 3. Functions Returning No Value (`None`)

If a function performs an action (like printing to console or writing to a database) without returning a value, annotate its return type as `None`:

```python
def log_event(event_name: str) -> None:
    print(f"[EVENT LOGGED]: {event_name}")
    # No return statement (implicitly returns None)
```

#### 4. Multiple or Optional Return Types

When a function can return different types, or might return `None` when a lookup fails:

```python
from typing import Optional, Union

# Returns a str if found, or None if user_id does not exist
def find_user_name(user_id: int) -> Optional[str]:
    users = {1: "Alice", 2: "Bob"}
    return users.get(user_id)  # Returns None for missing keys

# Returns either an int or a float depending on input format
def parse_numeric(val: str) -> Union[int, float]:
    if "." in val:
        return float(val)
    return int(val)
```

#### 5. Higher-Order Functions (`Callable`)

When passing a function as a parameter to another function, use `Callable[[ArgTypes...], ReturnType]` from the `typing` module:

```python
from typing import Callable

def apply_transform(numbers: list[int], transform: Callable[[int], int]) -> list[int]:
    return [transform(n) for n in numbers]

def square(x: int) -> int:
    return x * x

# Usage: square is passed as an argument
result = apply_transform([1, 2, 3, 4], square)  # Output: [1, 4, 9, 16]
```

---

## Static Code Analysis with MyPy

To enforce your type hints and check for mismatches, you can use a static code analysis tool called **mypy**.

- **Installation**: Open your terminal/command prompt and run:
  ```bash
  pip install mypy
  ```
- **Execution**: Run `mypy` against your python file by passing the filename:
  ```bash
  mypy filename.py
  ```

### Practical MyPy Execution Examples & Errors Caught

#### Example 1: Incompatible Assignment & Argument Type Mismatch

**Source Code (`example1.py`):**

```python
def multiply(a: int, b: int) -> int:
    return a * b

# Error 1: Assigning an integer to a variable hinted as string
user_name: str = 42

# Error 2: Passing a string argument where an int parameter is expected
total = multiply(10, "5")
```

**Terminal Execution:**

```bash
$ mypy example1.py
```

**MyPy Output (Errors Caught):**

```text
example1.py:5: error: Incompatible types in assignment (expression has type "int", variable has type "str")  [assignment]
example1.py:8: error: Argument 2 to "multiply" has incompatible type "str"; expected "int"  [arg-type]
Found 2 errors in 1 file (checked 1 source file)
```

#### Example 2: Invalid Return Type & Missing Return Statement

**Source Code (`example2.py`):**

```python
def get_user_id(username: str) -> int:
    if username == "admin":
        return 101
    # Error 1: Missing return statement when username != "admin" (returns None implicitly)

def calculate_score(points: float) -> str:
    # Error 2: Returning float/int when function promises to return str
    return points * 1.5
```

**Terminal Execution:**

```bash
$ mypy example2.py
```

**MyPy Output (Errors Caught):**

```text
example2.py:1: error: Missing return statement  [return]
example2.py:8: error: Incompatible return value type (got "float", expected "str")  [return-value]
Found 2 errors in 1 file (checked 1 source file)
```

#### Example 3: Unhandled `Optional` (`None`) Access

**Source Code (`example3.py`):**

```python
from typing import Optional

def find_email(user_id: int) -> Optional[str]:
    if user_id == 1:
        return "alice@example.com"
    return None  # User not found

email = find_email(99)

# Error: Calling .lower() on Optional[str] without checking if email is None
print(email.lower())
```

**Terminal Execution:**

```bash
$ mypy example3.py
```

**MyPy Output (Errors Caught):**

```text
example3.py:12: error: Item "None" of "Optional[str]" has no attribute "lower"  [union-attr]
Found 1 error in 1 file (checked 1 source file)
```

**How to fix the error in `example3.py`:**

```python
# Safe handling required by MyPy:
if email is not None:
    print(email.lower())
else:
    print("No email found")
```

## The `typing` Module

For more complex data structures and types, you must import them from Python's built-in `typing` module.

```python
from typing import List, Dict, Set, Tuple, Optional, Any, Sequence, Callable
```

### 1. Collections (Lists, Dicts, Sets, Tuples)

You can define exactly what types of elements are contained within your data structures.

```python
# Lists (e.g., A list of lists of integers)
x: List[List[int]] = [[1, 2, 3], [4, 5, 6]]

# Dictionaries (Specify the Key type, then Value type)
y: Dict[str, str] = {"key": "value"}

# Sets
z: Set[str] = {"a", "b", "c"}

# Tuples (Specify the exact type for each element in the tuple)
t: Tuple[int, int, str] = (1, 2, "hello")
```

### 2. Custom Types (Aliases)

You can create custom type aliases by assigning a complex typing configuration to a simple variable. This makes your code more readable.

```python
Vector = List[float] # Convention to use capitalized identifiers for types

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]
```

### 3. Special Typing Types

#### 1. Understanding Tuples (`tuple`) in Detail

Unlike lists (where every element usually shares the same type, like `list[int]`), tuples in Python are often used to store **fixed-length, ordered data** where each position can hold a _different_ data type.

##### A. Fixed-Length Heterogeneous Tuples

When annotating a fixed-length tuple, you must specify the exact type for **every item position**:

```python
# Fixed 2-element tuple of integers (e.g. (x, y) coordinates)
point: tuple[int, int] = (10, 20)

# Fixed 3-element tuple with different types (name: str, age: int, gpa: float)
student: tuple[str, int, float] = ("Alice", 20, 3.8)

# MyPy Error: Wrong element count or type mismatch!
# student: tuple[str, int, float] = ("Bob", 22)  # Missing float!
```

##### B. Variable-Length Homogeneous Tuples (`tuple[T, ...]`)

If a tuple can contain an arbitrary (unknown) number of elements of the _same_ type, use the ellipsis (`...`) syntax:

```python
# A tuple containing any number of integers:
scores: tuple[int, ...] = (90, 85, 95, 100)
empty_scores: tuple[int, ...] = ()
```

##### C. How Tuples Pass to `Sequence`

Any tuple whose elements share a uniform type (like `tuple[int, int, int]` or `tuple[int, ...]`) can be passed to a function expecting `Sequence[int]`:

```python
from typing import Sequence

def compute_total(numbers: Sequence[int]) -> int:
    return sum(numbers)

# 1. Passing a fixed 3-element int tuple -> Compatible with Sequence[int]
print(compute_total((10, 20, 30)))  # Output: 60

# 2. Passing a variable-length int tuple -> Compatible with Sequence[int]
print(compute_total((1, 2, 3, 4, 5)))  # Output: 15

# Note: A heterogeneous tuple like tuple[str, int] CANNOT be passed to Sequence[int]
# because not all elements are integers!
```

#### 2. `Sequence`

**What is a `Sequence`?**
In Python, a `Sequence` is a broad, read-only interface representing any ordered collection where elements can be accessed by index (like `data[0]`) and measured with `len(data)`. Built-in Python types like `list`, `tuple`, `str`, `bytes`, and `range` are all sequences under the hood.

**When to use `Sequence` over `list` or `tuple`?**

1. **Flexibility (Accepting Multiple Inputs)**:
   - If you annotate a function parameter as `items: list[int]`, static type checkers (`mypy`) will **reject** passing a tuple `(1, 2, 3)` or a `range(1, 10)`, even if your function only reads from the collection!
   - By annotating it as `items: Sequence[int]`, your function welcomes `list`, `tuple`, `range`, or any custom ordered container.
2. **Read-Only Safety Intent**:
   - `list[T]` implies that the function might modify the collection (using `.append()`, `.pop()`, `.extend()`).
   - `Sequence[T]` explicitly promises callers: _"This function will only read elements by index or iterate over them—it will never mutate your data."_

| Type Hint         | Best Used When...                                                      | Accepts...                      | Can Mutate Data?                  |
| ----------------- | ---------------------------------------------------------------------- | ------------------------------- | --------------------------------- |
| **`list[T]`**     | Your function specifically needs to modify the collection in place.    | Only `list`                     | Yes (`.append()`, `.pop()`, etc.) |
| **`tuple[...]`**  | You have a fixed-length container with specific element types.         | Only `tuple`                    | No (immutable)                    |
| **`Sequence[T]`** | Your function only **reads** an ordered collection by index or length. | `list`, `tuple`, `str`, `range` | No (read-only interface)          |

**Example 1: Flexibility — Accepting lists, tuples, and ranges**

```python
from typing import Sequence

def get_middle_item(items: Sequence[int]) -> int:
    # Function only reads by index and len()
    mid_index = len(items) // 2
    return items[mid_index]

print(get_middle_item([10, 20, 30]))     # Works with a list -> 20
print(get_middle_item((100, 200, 300)))  # Works with a tuple -> 200
print(get_middle_item(range(1, 6)))      # Works with a range -> 3
```

**Example 2: Read-Only Intent vs List Mutation**

```python
# Specific & Mutating: Requires a list, allows modifying original data
def append_zero(items: list[int]) -> None:
    items.append(0)  # Modifies list in place

# Generic & Read-Only: Accepts any sequence, guarantees no mutation
def calculate_sum(numbers: Sequence[float]) -> float:
    # numbers.append(1.0)  # MyPy Error! Sequence object has no attribute 'append'
    return sum(numbers)
```

**Example 3: Strings as Sequences**
In Python, strings are sequences of characters. A `Sequence[str]` can accept both a `str` or a list/tuple of strings:

```python
def print_indexed_chars(data: Sequence[str]) -> None:
    for idx, char in enumerate(data):
        print(f"Index {idx}: {char}")

# 1. Passing a string directly (Sequence of 1-character strings)
print_indexed_chars("CAT")
# Output:
# Index 0: C
# Index 1: A
# Index 2: T

# 2. Passing a list of strings
print_indexed_chars(["C", "A", "T"])
```

#### 3. `Callable`

Used when passing a function as a parameter or returning a function (`Callable[[Arg1Type, Arg2Type], ReturnType]`).

**Example 1: Passing a transformation function as an argument**

```python
from typing import Callable

def apply_op(a: int, b: int, func: Callable[[int, int], int]) -> int:
    return func(a, b)

def add(x: int, y: int) -> int:
    return x + y

print(apply_op(5, 3, add))  # Output: 8
```

**Example 2: Returning a factory function / multiplier lambda**

```python
def make_multiplier(factor: int) -> Callable[[int], int]:
    return lambda x: x * factor

double = make_multiplier(2)
print(double(5))  # Output: 10
```

**Using `Callable` with Lambda Functions:**
Since a `lambda` in Python is simply an anonymous function, it shares the exact same `Callable` type signature as a standard function defined with `def`. You can assign a `lambda` directly to a variable annotated with `Callable[[ArgTypes...], ReturnType]`, or pass an inline `lambda` directly into any function expecting a `Callable`:

```python
from typing import Callable

# 1. Assigning a lambda to a type-hinted variable
is_even: Callable[[int], bool] = lambda x: x % 2 == 0

print(is_even(4))  # Output: True

# 2. Passing an inline lambda into a function parameter expecting Callable[[int, int], int]
result = apply_op(10, 4, lambda x, y: x - y)  # Output: 6
```

#### 4. `Any`

Explicitly disables type checking for a variable. Useful when handling unpredictable third-party dynamic data or migrating legacy code.

**Example 1: Handling arbitrary JSON payload**

```python
from typing import Any

def log_raw_payload(payload: Any) -> None:
    # Any data structure allowed: dict, list, str, int, etc.
    print("Received payload:", payload)
```

**Example 2: Heterogeneous collections**

```python
# Mixed list where elements can be any type
mixed_data: list[Any] = [1, "hello", True, {"key": "value"}]
```

#### 5. `Optional`

Used when a variable, function parameter, or return value can be a specific type OR `None`. (Equivalent to `Union[T, None]` or `T | None` in Python 3.10+).

**Example 1: Optional Function Parameters with Default `None` (Most Common Use Case)**

```python
from typing import Optional

# `middle_name` is optional; defaults to None if omitted by caller
def greet(name: str, middle_name: Optional[str] = None) -> str:
    if middle_name:
        return f"Hello {name} {middle_name}"
    return f"Hello {name}"

print(greet("John"))                 # Output: Hello John
print(greet("John", "Robert"))       # Output: Hello John Robert
```

**Example 2: Optional Configuration Parameter**

```python
def connect_db(host: str, port: int = 5432, password: Optional[str] = None) -> None:
    if password is None:
        print(f"Connecting to {host}:{port} without password...")
    else:
        print(f"Connecting to {host}:{port} with password.")

connect_db("localhost")
connect_db("localhost", password="secret_pass")
```

**Example 3: Optional Return Type (Lookup results)**

---

## Union Type Annotations (`Union` & `|`)

A **Union** type annotation is used when a variable, function parameter, or return value can legitimately hold one of several different data types.

### Syntax

- **Python 3.10+ (Modern Pipe Syntax)**: `Type1 | Type2 | Type3` (No imports required!)
- **Python 3.5+ (Standard Library `typing` Syntax)**: `Union[Type1, Type2, Type3]` (`from typing import Union`)

### Examples of `Union`

#### 1. Parameters Accepting Multiple Numeric or Primitive Types

```python
from typing import Union

# Accepts either an integer OR a float (Python 3.5+ syntax)
def double_value(val: Union[int, float]) -> Union[int, float]:
    return val * 2

# Python 3.10+ equivalent using pipe operator (|):
def double_value_modern(val: int | float) -> int | float:
    return val * 2

print(double_value(5))     # Output: 10
print(double_value(3.5))   # Output: 7.0
```

#### 2. Parsing Functions Returning Different Data Types

```python
# Parses a string input into either an int or float
def parse_number(text: str) -> int | float:
    if "." in text:
        return float(text)
    return int(text)
```

#### 3. Relation to `Optional`

Note that `Optional[str]` is simply a shorthand helper for `Union[str, None]` (or `str | None` in Python 3.10+).

---

## Literal Type Annotations (`Literal`)

While types like `str` or `int` allow _any_ string or integer, **`Literal`** restricts a variable or parameter to specific **exact values**.

### Why Use `Literal`?

- To enforce exact string options (e.g. file modes `"r"`, `"w"`, `"rb"`).
- To prevent bugs caused by typos in string flags or magic numbers.
- To give your IDE accurate autocomplete for string choices.

### Examples of `Literal`

#### 1. Restricting File Modes

```python
from typing import Literal

# Mode parameter MUST be one of these exact three strings: "r", "w", or "a"
def open_file(filename: str, mode: Literal["r", "w", "a"]) -> None:
    print(f"Opening {filename} in '{mode}' mode.")

open_file("data.txt", "r")  # Valid!

# MyPy / IDE Error! "rb" is not allowed in Literal["r", "w", "a"]
# open_file("data.txt", "rb")
```

#### 2. Enforcing User Statuses & Config Flags

```python
Status = Literal["pending", "approved", "rejected"]

def update_status(user_id: int, new_status: Status) -> None:
    print(f"User {user_id} status updated to {new_status}")

update_status(101, "approved")  # Valid!
# update_status(101, "completed")  # MyPy Error: Invalid Literal choice!
```

---

## Final Type Annotations (`Final` & `@final`)

The **`Final`** type qualifier is used to declare **constants** and prevent variables from being re-assigned, or to prevent classes/methods from being overridden by subclasses.

> [!NOTE]
> **Why does `Final[int]` use square brackets `[...]` like `list[int]`?**
>
> In Python's typing system, square brackets `[...]` are used for **type parameterization** (passing one type into a modifier), not just for lists or dictionaries:
>
> - For collections (`list[int]`), `[int]` specifies the type of elements contained _inside_ the list.
> - For type qualifiers (`Final[int]`), `Final` is a **wrapper/modifier**. The brackets `[int]` specify the single underlying data type that is being locked as constant. It reads as: _"treat this single `int` as Final (read-only)."_
> - **Type Inference Shorthand**: Because `Final` wraps the assigned value, Python can automatically infer the inner type! Writing `MAX_CONNECTIONS: Final = 100` is valid shorthand for `MAX_CONNECTIONS: Final[int] = 100`.

### Why Use `Final`?

- **Immutability Intention**: Signals to developers and type checkers that a value should never change once set.
- **Protection**: MyPy will raise an error if any code attempts to overwrite a `Final` variable.

### Examples of `Final`

#### 1. Defining Immutable Constants

```python
from typing import Final

# Declare a constant variable
MAX_CONNECTIONS: Final[int] = 100
DATABASE_URL: Final[str] = "postgres://user:pass@localhost:5432/db"

# MyPy Error: Cannot assign to final name "MAX_CONNECTIONS"
# MAX_CONNECTIONS = 200
```

#### 2. Final Class Attributes

```python
class AppConfig:
    # Class constant that subclasses cannot override
    VERSION: Final[str] = "1.0.0"
```

#### 3. Preventing Subclass Overriding (`@final` Decorator)

```python
from typing import final

class BaseDatabase:
    @final
    def connect(self) -> None:
        print("Connecting securely...")

class CustomDatabase(BaseDatabase):
    # MyPy Error: Cannot override final method "connect" in BaseDatabase
    # def connect(self) -> None:
    #     print("Custom connection")
    pass
```

---

## Generics with `TypeVar`

Generics allow you to write reusable functions and classes that work across multiple data types while preserving **strict type consistency**.

### Why Use `TypeVar` Instead of `Any`?

If you annotate a function with `Any`:

```python
def get_item(lst: list[Any], index: int) -> Any:
    return lst[index]
```

The static type checker loses track of the relationship between the input list items and the returned item. If you pass a `list[str]`, the returned value is typed as `Any` instead of `str`, so your IDE cannot offer `str` autocompletions (like `.upper()`) or catch type mismatches!

By using `TypeVar('T')`, you create a **type variable binding**:

- When passed a `list[int]`, `T` binds to `int`, so the return type is guaranteed to be `int`.
- When passed a `list[str]`, `T` binds to `str`, so the return type is guaranteed to be `str`.

### Function Definition

```python
from typing import TypeVar, List

# Create a generic type placeholder 'T'
T = TypeVar('T')

def get_item(lst: List[T], index: int) -> T:
    return lst[index]
```

### Example Invocations & Output

#### Example 1: Passing a List of Integers (`T` binds to `int`)

```python
numbers = [10, 20, 30]

# T is inferred as `int`, so `first_num` is automatically typed as `int`
first_num = get_item(numbers, 0)

print(first_num)        # Output: 10
print(type(first_num))  # Output: <class 'int'>
```

#### Example 2: Passing a List of Strings (`T` binds to `str`)

```python
words = ["apple", "banana", "cherry"]

# T is inferred as `str`, so `fruit` is automatically typed as `str`
fruit = get_item(words, 1)

print(fruit.upper())    # Output: BANANA
```

### Error Cases (Caught by MyPy & Runtime)

#### Error Case 1: Incompatible Assignment (MyPy Error)

```python
names: list[str] = ["Alice", "Bob"]

# MyPy Error: Incompatible types in assignment (expression has type "str", variable has type "int")
user_id: int = get_item(names, 0)
```

#### Error Case 2: Calling Undefined Methods on Inferred Type (MyPy Error)

```python
scores: list[int] = [95, 88, 100]

score = get_item(scores, 0)

# MyPy Error: "int" has no attribute "lower"  [attr-defined]
print(score.lower())
```

#### Error Case 3: Out of Bounds Index (Runtime Error)

```python
items = [1, 2, 3]

# Runtime Error: IndexError: list index out of range
get_item(items, 10)
```

### Advanced: Constrained `TypeVar` (Restricting Allowed Types)

You can restrict a `TypeVar` to only permit specific allowed types:

```python
from typing import TypeVar

# T can ONLY be an int or a float
NumberT = TypeVar('NumberT', int, float)

def add_values(a: NumberT, b: NumberT) -> NumberT:
    return a + b

add_values(10, 20)      # Valid! NumberT = int -> Returns int
add_values(1.5, 2.5)    # Valid! NumberT = float -> Returns float

# MyPy Error: Value of type "str" is not a valid choice for NumberT  [type-var]
# add_values("hello", "world")
```
