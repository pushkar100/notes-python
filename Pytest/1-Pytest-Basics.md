# 🧪 Pytest Notes

- [🌟 1. Introduction: What is Pytest?](#1-introduction-what-is-pytest)
- [🛠️ 2. Installation and IDE Setup](#2-installation-and-ide-setup)
- [🔍 3. Test Autodiscovery Rules](#3-test-autodiscovery-rules)
- [🚀 4. Writing Your First Test & Package Structure](#4-writing-your-first-test-package-structure)
- [⚠️ 5. Testing Exceptions: `pytest.raises` & Error Types](#5-testing-exceptions-pytestraises-error-types)
- [� 6. Testing Diverse Data Types & Collections](#6-testing-diverse-data-types-collections)
- [🏛️ 7. Testing Classes & Object-Oriented Code](#7-testing-classes-object-oriented-code)
- [🏗️ 8. Deep Dive: Fixtures (The Modern Setup & Teardown)](#8-deep-dive-fixtures-the-modern-setup-teardown)
- [🔄 9. Deep Dive: Parameterized Testing](#9-deep-dive-parameterized-testing)
- [🏷️ 10. Markers & Filtering Tests](#10-markers-filtering-tests)
- [🎭 11. Mocking: Testing Without Real Dependencies](#11-mocking-testing-without-real-dependencies)
- [🪄 12. Real-World Application: The Harry Potter Test Suite (AI Assisted)](#12-real-world-application-the-harry-potter-test-suite-ai-assisted)
- [⚡ 13. Pytest CLI Execution Cheat Sheet](#13-pytest-cli-execution-cheat-sheet)

---

## 🌟 1. Introduction: What is Pytest?

Pytest is a robust and flexible testing framework for Python. This course, taught by full-stack developer Farhan Ali, outlines how to leverage Pytest to write clean, effective tests.

### Core Reasons to Choose Pytest:

- **Simplified Syntax:** It uses standard Python `assert` statements rather than requiring special assertion methods like `assertEqual` or `assertTrue` found in other libraries.
- **Rich Assertion Introspection:** When a test fails, Pytest generates highly readable, clean reports that break down exactly why the failure occurred, making debugging straightforward.
- **Autodiscovery:** Pytest automatically identifies which functions and methods are tests without explicit manual registration.
- **Backward Compatibility:** Pytest can seamlessly run tests originally written for other frameworks like `unittest` or `nose`, making migration easy.
- **Extensibility:** It features a rich plug-in architecture, such as `pytest-django` for testing Django applications.
- **Powerful Fixtures:** Fixtures handle setup and teardown operations, can utilize auto-use settings, and manage scope (so an object can be created once and used across all tests).

---

## 🛠️ 2. Installation and IDE Setup

While you can use VS Code or even Notepad, the tutorial highly recommends using **PyCharm** (Community version works perfectly) due to its excellent, out-of-the-box test integration.

Setting up the project inside a virtual environment is standard practice:

```bash
# Install pytest using pip (version 7.4.2 was used in the tutorial)
pip install pytest
```

---

## 🔍 3. Test Autodiscovery Rules

Pytest automatically picks up tests based on specific naming conventions:

1. **Files:** Must be named `test_<name>.py` or `<name>_test.py`.
2. **Functions:** Inside those files, test functions must start with `test_` (e.g., `test_addition`).

Because of autodiscovery, you don't need to specify each test case manually in the CLI; running the command `pytest` will find and execute them all.

---

## 🚀 4. Writing Your First Test & Package Structure

### Project & Package Organization

To keep tests organized and avoid import collisions, structure your project by separating source code from test code:

```text
my_project/
├── source/
│   ├── __init__.py          # Marks 'source' as a Python package
│   └── my_functions.py      # Source code (e.g., add, divide)
├── tests/
│   ├── __init__.py          # Marks 'tests' as a package
│   └── test_my_functions.py # Test file
└── pytest.ini               # Project-level Pytest configuration
```

#### How Packages & Imports Work

- **`__init__.py`**: An `__init__.py` file inside a directory turns that directory into a Python package. This enables standard package imports such as `import source.my_functions as my_functions`.
- **Resolving `ModuleNotFoundError`**: When Pytest runs, it needs to locate the root package folder. The standard solutions are:
  1. **`pytest.ini` (Recommended)**: Create a `pytest.ini` at your project root with:
     ```ini
     [pytest]
     pythonpath = .
     testpaths = tests
     ```
     This automatically prepends the root directory to `sys.path`.
  2. **Run as a module**: Run `python -m pytest` from the root directory instead of plain `pytest`.
  3. **Set `PYTHONPATH`**: Prepend the current directory via `PYTHONPATH=. pytest`.

### Step 1: The Source File (`source/my_functions.py`)

Create the functions to test:

```python
def add(num1, num2):
    return num1 + num2

def divide(num1, num2):
    return num1 / num2
```

### Step 2: The Test File & Assertions (`tests/test_my_functions.py`)

Pytest leverages standard Python `assert` statements instead of cumbersome assertion methods like `self.assertEqual()`. When expecting an exception (such as `ZeroDivisionError`), use `pytest.raises()`.

```python
import pytest
import source.my_functions as my_functions

def test_add():
    result = my_functions.add(1, 4)
    assert result == 5

def test_add_strings():
    result = my_functions.add("i like ", "burgers")
    assert result == "i like burgers"

def test_divide():
    result = my_functions.divide(10, 2)
    assert result == 5

def test_divide_by_zero():
    # Verify that dividing by zero raises ZeroDivisionError
    with pytest.raises(ZeroDivisionError):
        my_functions.divide(10, 0)
```

### Step 3: Running the Tests

Run Pytest from your terminal in the project root:

```bash
# Standard run (captures and silences print statements on passing tests)
pytest

# Verbose run (displays each test name and pass/fail state)
pytest -v

# Display print statements live in the console (-s or --capture=no)
pytest -s

# Highly recommended: Combine verbose test names with live print statements
pytest -vs
```

#### 💡 Showing `print()` Statements with `-s` (`--capture=no`)

By default, Pytest **captures standard output (`stdout`) and standard error (`stderr`)** during execution:

- **Passing tests:** Pytest swallows and conceals all `print()` output so your terminal stays clean.
- **Failing tests:** Pytest only displays captured `print()` logs at the very end in the failure report under `--- Captured stdout call ---`.

To see `print()` output printed to the terminal in real time for **all** tests (passing and failing):

1. **Pass the `-s` flag via CLI:**

   ```bash
   pytest -s
   pytest -vs     # Both verbose test names and console output
   ```

   > [!TIP]
   > `-s` is a convenient shorthand for `--capture=no`.

2. **Enable it permanently via `pytest.ini` (Optional):**
   If you prefer to always see console outputs without having to type `-s` each time, add `addopts = -s` to your configuration file:
   ```ini
   [pytest]
   pythonpath = .
   addopts = -s
   ```

### Step 4: Verifying the Terminal Logs

#### ✅ The Passing Case

Running `pytest -v` when all assertions succeed:

```text
============================= test session starts ==============================
platform darwin -- Python 3.14.2, pytest-9.1.1, pluggy-1.6.0 -- ...
rootdir: /Users/pushkar/Desktop/pytest
configfile: pytest.ini
testpaths: tests
collected 4 items

tests/test_my_functions.py::test_add PASSED                              [ 25%]
tests/test_my_functions.py::test_add_strings PASSED                      [ 50%]
tests/test_my_functions.py::test_divide PASSED                           [ 75%]
tests/test_my_functions.py::test_divide_by_zero PASSED                   [100%]

============================== 4 passed in 0.01s ===============================
```

- **Dots (`.`) vs. `PASSED`**: In default mode, each passing test is represented by a single dot (`.`). In verbose mode (`-v`), each test displays `PASSED`.
- **Exit Status 0**: Pytest exits with status code `0`, signaling that all tests completed successfully.

#### ❌ The Failing Case

If an assertion fails (for example, if `test_add` expected `assert result == 6`):

```text
=================================== FAILURES ===================================
___________________________________ test_add ___________________________________

    def test_add():
        result = my_functions.add(1, 4)
>       assert result == 6
E       assert 5 == 6

tests/test_my_functions.py:7: AssertionError
=========================== short test summary info ============================
FAILED tests/test_my_functions.py::test_add - assert 5 == 6
========================= 1 failed, 3 passed in 0.02s ==========================
```

- **`FAILURES` Block**: Highlights the exact function and file that encountered the failure.
- **`>` Indicator**: Points directly to the line of code that triggered the failure.
- **`E` (Error) Introspection**: Pytest details the exact values evaluated during execution (`5 == 6`), making debugging immediate without adding print statements.
- **Short test summary**: Lists failed tests at the bottom of the log for quick reference in large suites.
- **Exit Status 1**: Pytest exits with status code `1`, which alerts CI/CD pipelines of test failures.

---

## ⚠️ 5. Testing Exceptions: `pytest.raises` & Error Types

Testing the "happy path" (successful outputs) is only half of testing. Robust test suites must also verify that your code **fails cleanly and predictably** when handed invalid arguments, missing data, or illegal operations.

Pytest provides the `pytest.raises()` context manager to test that a specific exception is raised.

### How `pytest.raises` Works

Wrap the code expected to raise an error inside `with pytest.raises(...)`:

```python
import pytest
import source.my_functions as my_functions

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        my_functions.divide(10, 0)
```

#### The Three Possible Outcomes:

1. **Expected exception is raised**: The test **PASSES**.
2. **No exception is raised**: The test **FAILS** with `Failed: DID NOT RAISE <class '...'>`.
3. **A different exception is raised**: The test **FAILS** with an unhandled exception error.

### Testing Different Python Error Types

You can pass any built-in or custom exception class to `pytest.raises()`:

| Exception Type      | When to Test For It                     | Example Scenario                            |
| :------------------ | :-------------------------------------- | :------------------------------------------ |
| `ZeroDivisionError` | Division or modulo by zero              | `divide(10, 0)`                             |
| `TypeError`         | Operation applied to incompatible types | `add(10, "five")`                           |
| `ValueError`        | Correct type but inappropriate value    | `int("not_a_number")` or `math.sqrt(-1)`    |
| `KeyError`          | Accessing a non-existent dictionary key | `user_dict["missing_id"]`                   |
| `IndexError`        | Sequence subscript out of range         | `empty_list[0]`                             |
| `CustomException`   | Application-specific domain errors      | `School.enroll(student)` exceeding capacity |

#### Code Examples:

```python
import pytest
import source.my_functions as my_functions

# 1. TypeError (Incompatible types)
def test_add_type_error():
    with pytest.raises(TypeError):
        my_functions.add(10, "five")

# 2. ValueError (Invalid value)
def test_invalid_value():
    with pytest.raises(ValueError):
        int("abc")

# 3. Custom Application Exception
class SchoolCapacityError(Exception):
    pass

def test_custom_exception():
    def enroll_student(current_count, max_capacity):
        if current_count >= max_capacity:
            raise SchoolCapacityError("Classroom is full!")
        return current_count + 1

    with pytest.raises(SchoolCapacityError):
        enroll_student(current_count=30, max_capacity=30)
```

### Checking Exception Messages

Sometimes catching the error type isn't enough; you also want to confirm the error message contains the right information.

#### Method 1: Using the `match` Parameter (Regex / Substring)

Pass a regex pattern or plain substring to `match`:

```python
def test_exception_match_message():
    # Passes only if ZeroDivisionError is raised AND message matches regex
    with pytest.raises(ZeroDivisionError, match="division by zero"):
        my_functions.divide(10, 0)
```

If the error message doesn't match the regex, Pytest fails the test:

```text
AssertionError: Pattern 'division by zero' not found in 'invalid division'
```

#### Method 2: Inspecting `exc_info` Directly

You can capture the exception object using `as exc_info` and perform standard assertions on its properties:

```python
def test_exception_inspection():
    with pytest.raises(ZeroDivisionError) as exc_info:
        my_functions.divide(10, 0)

    # 1. Check exact message string
    assert "division by zero" in str(exc_info.value)

    # 2. Check the exact exception type
    assert exc_info.type is ZeroDivisionError
```

### What Log Failures Look Like

#### 1. When Code DOES NOT Raise (Expected Failure Missed)

If you write a test expecting an exception, but the function succeeds:

```python
def test_divide_by_zero_fails():
    with pytest.raises(ZeroDivisionError):
        my_functions.divide(10, 2)  # This returns 5, does not raise!
```

Pytest terminal output:

```text
=================================== FAILURES ===================================
__________________________ test_divide_by_zero_fails ___________________________

    def test_divide_by_zero_fails():
>       with pytest.raises(ZeroDivisionError):
E       Failed: DID NOT RAISE <class 'ZeroDivisionError'>

tests/test_my_functions.py:18: Failed
=========================== short test summary info ============================
FAILED tests/test_my_functions.py::test_divide_by_zero_fails - Failed: DID NOT RAISE <class 'ZeroDivisionError'>
```

#### 2. When Code Raises the WRONG Exception

If your test expects `ValueError`, but the code raises `TypeError`:

```text
=================================== FAILURES ===================================
___________________________ test_wrong_exception _______________________________

    def test_wrong_exception():
>       with pytest.raises(ValueError):
>           my_functions.add(10, "five")
E       TypeError: unsupported operand type(s) for +: 'int' and 'str'

tests/test_my_functions.py:22: TypeError
```

---

## � 6. Testing Diverse Data Types & Collections

In real-world applications, functions return more than simple integers. Pytest makes asserting across Python's built-in data types (strings, floats, booleans, lists, dictionaries, sets) and specialized collections (`namedtuple`, `defaultdict`, `OrderedDict`, `deque`, `Counter`) clean and readable.

Here are simple, function-based examples demonstrating the best ways to test each type.

### 1. Numbers: Integers, Comparisons & Floating Point Precision

```python
import pytest

def calculate_discount(price, discount_percent):
    return price * (1 - discount_percent)

def test_integer_and_comparisons():
    result = calculate_discount(100, 0.20)
    assert result == 80          # Exact equality
    assert result > 0            # Greater than
    assert result <= 100         # Less than or equal to

def test_floating_point():
    # In Python: 0.1 + 0.2 equals 0.30000000000000004 due to binary floating-point representation.
    # A standard `assert 0.1 + 0.2 == 0.3` will FAIL.
    # Use `pytest.approx()` to safely compare floats within a sensible tolerance:
    assert (0.1 + 0.2) == pytest.approx(0.3)
```

> [!TIP]
> Always use `pytest.approx()` when asserting float results to prevent test failures caused by tiny floating-point rounding errors.

### 2. Booleans & `None`

Use Python's identity checks (`is`, `is not`) or direct boolean evaluation:

```python
def is_even(n):
    return n % 2 == 0

def find_user(username):
    users = {"alice": 1, "bob": 2}
    return users.get(username)  # returns None if user not found

def test_booleans():
    assert is_even(4) is True
    assert is_even(7) is False
    assert is_even(4)           # Truthy check
    assert not is_even(7)       # Falsy check

def test_none_value():
    assert find_user("alice") is not None
    assert find_user("charlie") is None
```

### 3. Strings: Exact Matches, Substrings & Case Sensitivity

```python
def format_welcome_message(name):
    return f"Welcome, {name.strip().capitalize()}!"

def test_string_formatting():
    msg = format_welcome_message("  sarah  ")

    # Exact match
    assert msg == "Welcome, Sarah!"

    # Substring check (membership)
    assert "Sarah" in msg
    assert "error" not in msg

    # Prefix and suffix checks
    assert msg.startswith("Welcome")
    assert msg.endswith("!")

    # Length check
    assert len(msg) == 15
```

### 4. Lists & Tuples: Ordered Sequences

Lists and tuples preserve order. Pytest provides itemized diffs if any element is out of place.

```python
def get_shopping_list():
    return ["apples", "bananas", "cherries"]

def test_list_contents():
    items = get_shopping_list()

    # 1. Exact equality (must have identical elements in identical order)
    assert items == ["apples", "bananas", "cherries"]

    # 2. Length check
    assert len(items) == 3

    # 3. Membership checks
    assert "bananas" in items
    assert "oranges" not in items

    # 4. Position checks (indexing)
    assert items[0] == "apples"
    assert items[-1] == "cherries"
```

### 5. Dictionaries: Key-Value Mappings

When asserting on dictionaries, Pytest excels at displaying precise differences (missing keys, extra keys, or mismatched values).

```python
def create_user_profile(user_id, username, email):
    return {
        "id": user_id,
        "username": username,
        "email": email,
        "is_active": True
    }

def test_user_profile_dictionary():
    profile = create_user_profile(101, "farhan", "farhan@example.com")

    # 1. Key existence checks
    assert "email" in profile
    assert "password" not in profile

    # 2. Value checks
    assert profile["username"] == "farhan"
    assert profile["is_active"] is True

    # 3. Full dictionary equality
    assert profile == {
        "id": 101,
        "username": "farhan",
        "email": "farhan@example.com",
        "is_active": True
    }
```

### 6. Sets: Unordered & Unique Collections

Sets ignore element ordering and duplicate entries, making them ideal when the order of results does not matter.

```python
def get_user_roles(user_id):
    # Returns a collection of assigned permissions/roles
    return {"viewer", "editor"}

def test_roles_set():
    roles = get_user_roles(1)

    # 1. Order-independent equality
    assert roles == {"editor", "viewer"}  # Order does not matter!

    # 2. Membership
    assert "editor" in roles
    assert "admin" not in roles

    # 3. Subset / Superset checks
    assert {"viewer"}.issubset(roles)
```

### 7. `namedtuple`: Structured & Immutable Records

`namedtuple` provides lightweight, immutable object representations with both named attribute and positional index access. When testing, you can assert field attributes, compare directly against tuples or other namedtuples, or verify the dictionary representation via `._asdict()`.

```python
from collections import namedtuple
import pytest

Coordinate = namedtuple("Coordinate", ["lat", "lon", "label"])

def get_headquarters_location():
    return Coordinate(lat=37.422, lon=-122.084, label="HQ")

def test_namedtuple():
    loc = get_headquarters_location()

    # 1. Attribute access
    assert loc.lat == pytest.approx(37.422)
    assert loc.label == "HQ"

    # 2. Positional indexing and unpacking
    assert loc[0] == pytest.approx(37.422)
    lat, lon, label = loc
    assert label == "HQ"

    # 3. Tuple and instance equality
    assert loc == Coordinate(pytest.approx(37.422), pytest.approx(-122.084), "HQ")
    assert loc == (pytest.approx(37.422), pytest.approx(-122.084), "HQ")

    # 4. Conversion to dictionary representation
    assert loc._asdict() == {
        "lat": pytest.approx(37.422),
        "lon": pytest.approx(-122.084),
        "label": "HQ",
    }
```

### 8. `defaultdict`: Mappings with Automatic Defaults

`defaultdict` calls a factory function whenever a missing key is accessed rather than raising a `KeyError`. In tests, verify both pre-populated keys, missing keys triggering default factory values, and conversion to standard dictionaries.

```python
from collections import defaultdict

def group_words_by_length(words):
    grouped = defaultdict(list)
    for word in words:
        grouped[len(word)].append(word)
    return grouped

def test_defaultdict():
    words = ["cat", "dog", "apple", "bird"]
    result = group_words_by_length(words)

    # 1. Access existing keys
    assert result[3] == ["cat", "dog"]
    assert result[5] == ["apple"]

    # 2. Accessing a missing key automatically initializes default value (empty list)
    assert result[10] == []
    assert 10 in result  # Accessing it inserted the key!

    # 3. Exact dictionary comparison
    assert dict(result) == {
        3: ["cat", "dog"],
        4: ["bird"],
        5: ["apple"],
        10: [],
    }
```

### 9. `OrderedDict`: Explicit Insertion Ordering

While standard Python dictionaries (since 3.7) retain insertion order, standard dictionary equality (`dict1 == dict2`) does **not** check key ordering. `OrderedDict` explicitly enforces key order during equality checks (`==`), making it critical when sequence matters.

```python
from collections import OrderedDict

def get_task_queue():
    queue = OrderedDict()
    queue["t1"] = "Download"
    queue["t2"] = "Process"
    queue["t3"] = "Notify"
    return queue

def test_ordered_dict():
    queue = get_task_queue()

    # 1. OrderedDict equality is order-sensitive
    reversed_queue = OrderedDict([
        ("t3", "Notify"),
        ("t2", "Process"),
        ("t1", "Download"),
    ])
    assert queue != reversed_queue  # Same keys and values, but different order!

    # 2. Standard dict comparison ignores ordering
    assert queue == {"t3": "Notify", "t1": "Download", "t2": "Process"}

    # 3. Explicit key order verification
    assert list(queue.keys()) == ["t1", "t2", "t3"]

    # 4. Mutations affecting order (move_to_end)
    queue.move_to_end("t1")
    assert list(queue.keys()) == ["t2", "t3", "t1"]
```

### 10. `deque`: Double-Ended Queues (Buffers & Pipelines)

`deque` (double-ended queue) is optimized for $O(1)$ appends and pops from both ends, and supports fixed-capacity circular buffers via `maxlen`. Testing deques typically focuses on boundary operations, eviction under capacity limits, and sequence validation.

```python
from collections import deque

def create_event_log(events, maxlen=3):
    log = deque(maxlen=maxlen)
    for event in events:
        log.append(event)
    return log

def test_deque():
    # Pass 4 events into a deque with maxlen=3 (oldest event 'e1' will be evicted)
    log = create_event_log(["e1", "e2", "e3", "e4"], maxlen=3)

    # 1. Capacity limit and FIFO auto-eviction
    assert len(log) == 3
    assert list(log) == ["e2", "e3", "e4"]
    assert "e1" not in log

    # 2. Left / Right operations
    log.appendleft("e_urgent")        # 'e4' gets pushed out from the right
    assert log[0] == "e_urgent"
    assert log.pop() == "e3"           # Remove from right end
    assert log.popleft() == "e_urgent" # Remove from left end
    assert list(log) == ["e2"]
```

### 11. `Counter`: Multiset & Frequency Counts

`Counter` is a dictionary subclass for counting hashable items. Testing involves checking counts, missing item behavior (returns 0 instead of `KeyError`), and frequency rankings (`most_common()`).

```python
from collections import Counter

def tally_votes(ballots):
    return Counter(ballots)

def test_counter():
    votes = tally_votes(["yes", "no", "yes", "yes", "abstain"])

    # 1. Exact counts
    assert votes["yes"] == 3
    assert votes["no"] == 1
    assert votes["abstain"] == 1

    # 2. Missing items return 0 count instead of raising KeyError
    assert votes["invalid"] == 0

    # 3. Frequency rankings
    assert votes.most_common(1) == [("yes", 3)]
    assert votes.most_common(2) == [("yes", 3), ("no", 1)]

    # 4. Total count
    assert votes.total() == 5
```

### 📋 Quick Reference: Common Assertion Patterns

| Data Type              | Common Assertion Pattern         | Example                                                    |
| :--------------------- | :------------------------------- | :--------------------------------------------------------- |
| **Integers / Numbers** | Equality and comparison          | `assert result == 42` / `assert count > 0`                 |
| **Floats**             | Approximate equality             | `assert result == pytest.approx(3.14, rel=1e-2)`           |
| **Booleans**           | Identity or truthiness           | `assert is_valid is True` / `assert not has_errors`        |
| **None**               | Identity check                   | `assert response is None`                                  |
| **Strings**            | Substring, case, or exact        | `assert "success" in msg.lower()`                          |
| **Lists / Tuples**     | Length, membership, order        | `assert len(items) == 3` / `assert item in items`          |
| **Dictionaries**       | Key existence and values         | `assert "id" in data` / `assert data["id"] == 1`           |
| **Sets**               | Unordered match and subsets      | `assert set_a == {"a", "b"}` / `assert subset <= full_set` |
| **`namedtuple`**       | Field access, indexing, equality | `assert loc.lat == 37.4` / `assert loc[0] == 37.4`         |
| **`defaultdict`**      | Missing key defaults & mappings  | `assert dd["missing"] == []` / `assert dict(dd) == {...}`  |
| **`OrderedDict`**      | Order-sensitive key matching     | `assert od != rev_od` / `assert list(od.keys()) == [...]`  |
| **`deque`**            | Maxlen eviction & end pop/append | `assert list(dq) == ["b", "c"]` / `assert dq.popleft()`    |
| **`Counter`**          | Frequency count & most common    | `assert counts["a"] == 3` / `assert counts["x"] == 0`      |

---

## 🏛️ 7. Testing Classes & Object-Oriented Code

Testing object-oriented code requires verifying instance initialization, attribute state, method calculations, mutations, inheritance, and magic/dunder methods (like `__eq__`).

Pytest gives you two complementary ways to test classes:

1. **Function-based tests:** Standalone functions testing class instances.
2. **Pytest Test Classes (`class Test...`):** Grouping related test methods inside a class for logical structure and shared lifecycle management.

### Step 1: The Source Classes (`source/shapes.py`)

Here is an object-oriented hierarchy featuring an abstract base class `Shape`, a `Circle`, and a `Rectangle`:

```python
import math

class Shape:
    """Base class for geometric shapes."""
    def area(self):
        raise NotImplementedError("Subclasses must implement area()")

    def perimeter(self):
        raise NotImplementedError("Subclasses must implement perimeter()")

class Circle(Shape):
    def __init__(self, radius):
        if radius <= 0:
            raise ValueError("Radius must be a positive number")
        self.radius = radius

    def area(self):
        return math.pi * (self.radius ** 2)

    def perimeter(self):
        return 2 * math.pi * self.radius

    def __eq__(self, other):
        if not isinstance(other, Circle):
            return False
        return self.radius == other.radius

class Rectangle(Shape):
    def __init__(self, length, width):
        if length <= 0 or width <= 0:
            raise ValueError("Dimensions must be positive numbers")
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)

    def __eq__(self, other):
        if not isinstance(other, Rectangle):
            return False
        return self.length == other.length and self.width == other.width
```

### Step 2: Pytest Test Class Rules & Conventions

When using classes to group tests in Pytest, adhere to these strict rules:

> [!IMPORTANT]
>
> 1. **Class Name:** Must begin with `Test` (in PascalCase, e.g., `TestCircle`, `TestRectangle`).
> 2. **NO `__init__` Constructor:** Pytest instantiates test classes internally. Defining an `__init__` method will trigger a `PytestWarning` or cause the tests to be ignored.
> 3. **Method Names:** Test methods inside the class must start with `test_` and accept `self` as their first parameter.

### Step 3: Writing Test Classes with Lifecycle Hooks (`setup_method` / `teardown_method`)

Pytest supports classic xUnit-style setup and teardown methods inside test classes:

- **`setup_method(self, method)`**: Executed automatically _before each_ test method runs in the class.
- **`teardown_method(self, method)`**: Executed automatically _after each_ test method finishes in the class.
- **`setup_class(cls)`**: Executed once _before all_ tests in the class run.
- **`teardown_class(cls)`**: Executed once _after all_ tests in the class finish.

```python
# tests/test_shapes.py
import math
import pytest
from source.shapes import Shape, Circle, Rectangle

class TestCircle:
    """Group all unit tests for the Circle class."""

    def setup_method(self, method):
        """Runs before every test method. Fresh instance per test prevents state leakage."""
        print(f"\nSetting up for: {method.__name__}")
        self.circle = Circle(radius=10)

    def teardown_method(self, method):
        """Runs after every test method."""
        print(f"\nTearing down after: {method.__name__}")
        del self.circle

    def test_area(self):
        expected_area = math.pi * (10 ** 2)
        assert self.circle.area() == pytest.approx(expected_area)

    def test_perimeter(self):
        expected_perimeter = 2 * math.pi * 10
        assert self.circle.perimeter() == pytest.approx(expected_perimeter)

    def test_equality(self):
        # Instances with identical state evaluate equal
        circle_same = Circle(radius=10)
        assert self.circle == circle_same

    def test_inequality(self):
        # Instances with different radii evaluate not equal
        circle_different = Circle(radius=5)
        assert self.circle != circle_different

    def test_type_inequality(self):
        # Comparing against a different class returns False safely
        rect = Rectangle(10, 10)
        assert self.circle != rect
        assert self.circle != "not a circle"

    def test_invalid_radius_raises_error(self):
        with pytest.raises(ValueError, match="Radius must be a positive number"):
            Circle(radius=-5)

        with pytest.raises(ValueError, match="Radius must be a positive number"):
            Circle(radius=0)

class TestRectangle:
    """Group all unit tests for the Rectangle class."""

    def setup_method(self, method):
        self.rect = Rectangle(length=10, width=5)

    def test_area(self):
        assert self.rect.area() == 50

    def test_perimeter(self):
        assert self.rect.perimeter() == 30

    def test_equality(self):
        assert self.rect == Rectangle(10, 5)
        assert self.rect != Rectangle(5, 10)

    def test_invalid_dimensions(self):
        with pytest.raises(ValueError, match="Dimensions must be positive"):
            Rectangle(length=-1, width=5)
```

### Step 4: Testing Base Classes & Abstract Interfaces

To ensure derived classes properly fulfill interface contracts and base methods behave as intended when invoked directly:

```python
def test_shape_base_class_cannot_calculate_area():
    base_shape = Shape()
    with pytest.raises(NotImplementedError, match="Subclasses must implement area"):
        base_shape.area()

def test_shape_base_class_cannot_calculate_perimeter():
    base_shape = Shape()
    with pytest.raises(NotImplementedError, match="Subclasses must implement perimeter"):
        base_shape.perimeter()

def test_circle_is_instance_of_shape():
    c = Circle(5)
    assert isinstance(c, Shape)
```

### Step 5: Executing Class-Based Tests from the CLI

Pytest provides path syntax (`::`) to target test classes or individual methods directly:

```bash
# 1. Run only tests inside the TestCircle class
pytest tests/test_shapes.py::TestCircle

# 2. Run a specific test method within a test class
pytest tests/test_shapes.py::TestCircle::test_area

# 3. Use -k keyword filtering matching class name
pytest -k "TestCircle"

# 4. Run all test classes with verbose method names
pytest tests/test_shapes.py -v
```

---

## 🏗️ 8. Deep Dive: Fixtures (The Modern Setup & Teardown)

In Section 7, we saw how test classes use `setup_method(self, method)` to prepare a fresh instance (like `self.circle = Circle(10)`) before each test method.

**However, what about standalone test functions?** Python functions do not belong to a class and have no `self` or instance state to attach setup logic to.

### ❓ The Problem: Duplication in Function-Based Tests

Without setup hooks, standalone test functions are forced to create their test objects over and over again inside every single test:

```python
# ❌ Boilerplate code repeated in every function:
def test_rectangle_area():
    rectangle = Rectangle(length=10, width=20)  # Repeated setup!
    assert rectangle.area() == 200

def test_rectangle_perimeter():
    rectangle = Rectangle(length=10, width=20)  # Repeated setup!
    assert rectangle.perimeter() == 60

def test_rectangle_equality():
    rectangle = Rectangle(length=10, width=20)  # Repeated setup!
    assert rectangle == Rectangle(10, 20)
```

**Why is this problematic?**

- **Violates DRY (Don't Repeat Yourself):** Every new test duplicates identical instantiation logic.
- **Maintenance Overhead:** If `Rectangle.__init__` changes (e.g., adding a new parameter or changing units), you must manually update dozens of test functions.
- **Accidental Coupling:** Attempting to solve this with module-level global variables creates shared state where one test mutating the object can cause other unrelated tests to fail.

### 💡 The Solution: Pytest Fixtures (`@pytest.fixture`)

A **fixture** is a function decorated with `@pytest.fixture` that prepares and provides data, models, connections, or state needed by tests.

Pytest connects fixtures to tests via **Dependency Injection**:

1. You define a fixture function: `@pytest.fixture def my_rectangle(): ...`
2. You pass the fixture's name as a parameter to any test function: `def test_area(my_rectangle):`
3. Pytest automatically discovers the parameter name, executes the fixture, and passes its returned value into the test!

### Step 1: Basic Fixture (Value / Object Injection)

Here is how simple and clean the previous test functions become using a fixture:

```python
# tests/test_rectangle.py
import pytest
from source.shapes import Rectangle

# 1. Define the fixture
@pytest.fixture
def my_rectangle():
    """Creates and supplies a fresh Rectangle instance for each test."""
    return Rectangle(length=10, width=20)

# 2. Inject it into standalone test functions by parameter name
def test_area(my_rectangle):
    assert my_rectangle.area() == 200

def test_perimeter(my_rectangle):
    assert my_rectangle.perimeter() == 60

def test_equality(my_rectangle):
    assert my_rectangle == Rectangle(10, 20)
```

> [!NOTE]
> By default, Pytest executes the fixture **once per test function** (`scope="function"`). Each test gets a completely fresh, isolated `Rectangle` instance. If `test_area` modifies `my_rectangle`, `test_perimeter` will still receive its own untouched instance!

### Step 2: Setup AND Teardown with `yield`

Often, a fixture needs to clean up after the test completes (e.g. closing database connections, deleting temporary files, or resetting system state).

Pytest uses Python's `yield` statement to cleanly separate setup from teardown within the same fixture function:

```python
@pytest.fixture
def custom_rectangle():
    # 1. SETUP: Code before yield runs BEFORE the test starts
    print("\n[Setup] Initializing custom rectangle...")
    rect = Rectangle(length=10, width=20)

    # 2. HANDOFF: Pauses fixture and injects 'rect' into the test
    yield rect

    # 3. TEARDOWN: Code after yield runs AFTER the test completes
    print("\n[Teardown] Cleaning up custom rectangle resources...")
```

#### Real-World Example: Managing a Database Connection Lifecycle

```python
import pytest

class Database:
    def connect(self):
        print("\nDatabase connected.")
        return "Connected"

    def disconnect(self):
        print("\nDatabase disconnected.")
        return "Disconnected"

@pytest.fixture
def db_connection():
    # SETUP
    db = Database()
    db.connect()

    # YIELD (Passes db to test and pauses)
    yield db

    # TEARDOWN (Guaranteed to execute even if the test fails)
    db.disconnect()

def test_database_query(db_connection):
    assert db_connection is not None
```

### Step 3: Global Fixtures & Setup via `conftest.py`

When multiple test files require the same setup, duplicating fixture functions across each test file violates DRY.

Pytest solves this with a special configuration file named **`conftest.py`**.

#### 1. How `conftest.py` Works: The "Zero-Import" Rule

Any fixture defined inside a `conftest.py` file is automatically registered in Pytest's fixture registry. All test files located in the same directory (or any child subdirectories) can use those fixtures **without importing them**.

```text
my_project/
├── source/
│   ├── __init__.py
│   └── shapes.py
├── tests/
│   ├── __init__.py
│   ├── conftest.py          # 👈 Global/shared fixtures go here
│   ├── test_circle.py       # Automatically sees fixtures in conftest.py
│   └── test_rectangle.py    # Automatically sees fixtures in conftest.py
└── pytest.ini
```

> [!WARNING]
> **Never `import conftest` into your test files!** Doing so causes circular imports and breaks Pytest's internal fixture resolution plugin. Pytest automatically reads `conftest.py` on startup.

#### 2. Defining Shared Fixtures in `conftest.py`

```python
# tests/conftest.py
import pytest
from source.shapes import Rectangle

@pytest.fixture
def shared_rectangle():
    """Available to ANY test file in tests/ without needing an import!"""
    return Rectangle(length=10, width=20)
```

Now, in any test file (such as `tests/test_rectangle.py`), simply pass `shared_rectangle` as an argument:

```python
# tests/test_rectangle.py
def test_area(shared_rectangle):
    assert shared_rectangle.area() == 200

def test_perimeter(shared_rectangle):
    assert shared_rectangle.perimeter() == 60
```

#### 3. Global Scopes: Running Setup Once Per Test Session (`scope="session"`)

By default, fixtures run on **`scope="function"`** (executed anew for each test). For heavy, expensive setups (e.g. connecting to a database, starting an in-memory server, or reading large files), you can set **`scope="session"`** so setup runs **once for the entire test suite**:

```python
# tests/conftest.py
import pytest

@pytest.fixture(scope="session")
def global_database():
    print("\n[GLOBAL SETUP] Connecting to test database once for the whole run...")
    db = {"status": "connected", "users": []}

    yield db  # Shared across all test files and functions

    print("\n[GLOBAL TEARDOWN] Disconnecting test database after all tests complete...")
```

#### Available Fixture Scopes:

- **`function`** _(default)_: Runs once per test function.
- **`class`**: Runs once per test class.
- **`module`**: Runs once per test file (`.py`).
- **`package`**: Runs once per test package directory.
- **`session`**: Runs once across the entire `pytest` execution run.

#### 4. Automatic Global Setup with `autouse=True`

If you have a global setup or teardown routine that **must run for every test** without requiring you to manually type the fixture name in every single test signature, set **`autouse=True`**:

```python
# tests/conftest.py
import pytest
import time

@pytest.fixture(scope="session", autouse=True)
def suite_timer():
    """Automatically records the duration of the entire test suite."""
    start_time = time.time()
    print("\n🚀 [Suite Started]")

    yield

    elapsed = time.time() - start_time
    print(f"\n🏁 [Suite Finished] Total execution time: {elapsed:.2f}s")

@pytest.fixture(scope="function", autouse=True)
def clean_state():
    """Automatically runs before and after EVERY single test without being declared."""
    # Setup runs before each test
    yield
    # Teardown runs after each test
```

### ⚖️ Why Fixtures Beat Class `setup_method`

| Capability                          | Class `setup_method`                  | Pytest Fixtures (`@pytest.fixture`)                                    |
| :---------------------------------- | :------------------------------------ | :--------------------------------------------------------------------- |
| **Works with Standalone Functions** | ❌ No (requires a `class`)            | ✅ Yes (works with functions AND classes)                              |
| **Data Passing**                    | Stored on `self.var` (can leak state) | Cleanly injected as explicit function arguments                        |
| **Composability**                   | Hard to combine multiple setups       | Fixtures can freely request other fixtures                             |
| **Configurable Scopes**             | Limited to class or method            | Supports `function`, `class`, `module`, `package`, `session`           |
| **Sharing Across Files**            | Requires class inheritance            | Define once in `conftest.py` — available project-wide without imports! |

---

## 🔄 9. Deep Dive: Parameterized Testing

Parameterization allows you to run a single test block multiple times with different inputs and expected outputs, eliminating boilerplate repetition and broadening test coverage.

> [!WARNING]
> **Common Gotcha:** Pytest spells the decorator `@pytest.mark.parametrize` (**no `e`** between the `t` and `r`). Accidental misspelling as `parameterize` (with an `e`) is quietly treated as an unrecognized custom mark, causing missing argument errors instead of parameterizing your test.

### Why Parameterization is Needed & How It Works

Before using parameterization, developers typically resort to two flawed approaches:

1. **Multiple Duplicate Test Functions:** Writing `test_is_even_two()`, `test_is_even_four()`, `test_is_even_five()`. This creates massive boilerplate and code duplication.
2. **A `for` Loop Inside a Single Test:**

   ```python
   # ❌ Anti-pattern: Using a for loop inside a test function
   def test_is_even_loop():
       cases = [(2, True), (3, True), (4, True)]
       for num, expected in cases:
           assert is_even(num) == expected
   ```

   - **Early Exit Problem:** If `3` fails, the test crashes immediately on the first failure — subsequent cases (like `4`) never get executed!
   - **Opaque Reporting:** Pytest counts this entire loop as only **1 single test**, hiding which specific inputs succeeded and which failed.

#### How `@pytest.mark.parametrize` Solves This:

- **Test Generation at Discovery:** Pytest unrolls your list of inputs into **separate, isolated test instances** during collection.
- **Independent Execution:** Each parameter set runs as its own test. If one input fails, all other cases continue running and report their individual pass/fail statuses.
- **Clear Failure Reporting:** Pytest labels each run with the input values in square brackets (e.g. `test_is_even[2-True]`, `test_is_even[4-True]`, `test_is_even[5-False]`).

### Code Sample:

```python
import pytest

def is_even(num):
    return num % 2 == 0

@pytest.mark.parametrize("number, expected", [
    (2, True),
    (4, True),
    (5, False)
])
def test_is_even(number, expected):
    assert is_even(number) == expected
```

#### Terminal Output Sample (`pytest -v`):

```text
tests/test_math.py::test_is_even[2-True] PASSED                          [ 33%]
tests/test_math.py::test_is_even[4-True] PASSED                          [ 66%]
tests/test_math.py::test_is_even[5-False] PASSED                         [100%]

============================== 3 passed in 0.01s ==============================
```

---

## 🏷️ 10. Markers & Filtering Tests

**Markers** are decorators (`@pytest.mark.<name>`) used to configure test behavior or categorize tests into logical groups (e.g., smoke tests, slow integration tests, database tests).

Pytest provides both **built-in markers** (for controlling test execution flow) and allows you to create **custom markers** (for tag-based filtering).

### 1. Built-in Markers

#### A. `@pytest.mark.skip`: Unconditional Skipping

Skips a test unconditionally. Always provide a `reason` explaining why:

```python
import pytest

@pytest.mark.skip(reason="External payment gateway is undergoing maintenance")
def test_payment_processing():
    assert process_payment(100) == "success"
```

**Terminal Output Sample (`pytest -v`):**

```text
tests/test_payment.py::test_payment_processing SKIPPED (External payment gateway is undergoing maintenance) [100%]

============================== 1 skipped in 0.01s ==============================
```

#### B. `@pytest.mark.skipif`: Conditional Skipping

Evaluates a boolean condition. If `True`, the test is skipped:

```python
import sys
import pytest

@pytest.mark.skipif(sys.platform != "darwin", reason="Runs only on macOS")
def test_macos_specific_shortcut():
    assert check_apple_menu() is True
```

#### C. `@pytest.mark.xfail`: Expected Failures

Marks a test that you know is currently broken (e.g., an unfixed bug or unimplemented feature).

- If it **fails**, Pytest reports it as `XFAIL` (expected failure) and the test suite **still passes with exit code 0** (CI does not break).
- If it **passes**, Pytest reports it as `XPASS` (unexpected pass).

```python
import pytest

@pytest.mark.xfail(reason="Ticket #402: Pending fix for negative radius validation")
def test_negative_radius_handling():
    # Currently broken code that returns 0 instead of raising ValueError
    assert Circle(-5) is None
```

**Terminal Output Sample (`pytest -v`):**

```text
tests/test_shapes.py::test_negative_radius_handling XFAIL (Ticket #402: Pending fix) [100%]

============================== 1 xfailed in 0.01s ==============================
```

> [!TIP]
> Use `strict=True` (`@pytest.mark.xfail(strict=True)`) if you want the test to actively **FAIL** your test run if it unexpectedly passes, alerting you that the issue was resolved.

### 2. Custom Markers: Tagging Tests by Category

Custom markers let you categorize tests so you can selectively run quick tests, slow tests, smoke tests, or database tests.

#### Step 1: Register Custom Markers in `pytest.ini`

To prevent Pytest from issuing `PytestUnknownMarkWarning`, always register your custom markers in `pytest.ini`:

```ini
# pytest.ini
[pytest]
pythonpath = .
markers =
    slow: marks tests as slow or computationally heavy
    smoke: fast sanity checks that must always pass
    database: tests that communicate with the database
```

#### Step 2: Tag Test Functions or Classes

You can apply markers to individual functions, entire test classes, or whole files:

```python
# tests/test_shapes.py
import pytest
from source.shapes import Rectangle

# 1. Single function tagged as 'smoke'
@pytest.mark.smoke
def test_rectangle_instantiation():
    rect = Rectangle(10, 20)
    assert rect.length == 10

# 2. Function tagged as 'slow'
@pytest.mark.slow
def test_complex_rendering_benchmark():
    import time
    time.sleep(1)
    assert True

# 3. An entire test class tagged with multiple markers
@pytest.mark.slow
@pytest.mark.database
class TestDatabaseShapeSync:
    def test_fetch_from_db(self):
        assert True
```

> [!NOTE]
> **Marking an entire module (file):** Add `pytestmark = pytest.mark.smoke` at the top of your test file to tag every test inside it automatically.

### 3. Running Marked Tests via the CLI (`-m` flag)

Pytest uses the **`-m`** option to filter and run only tests matching a marker expression.

#### A. Run Only a Specific Marker

Run only tests tagged with `@pytest.mark.slow`:

```bash
pytest -m slow -v
```

**Terminal Output Sample:**

```text
collected 4 items / 3 deselected / 1 selected

tests/test_shapes.py::test_complex_rendering_benchmark PASSED            [100%]

======================== 1 passed, 3 deselected in 0.02s ========================
```

_(Notice the `3 deselected` message — Pytest collected all tests but selectively skipped unmarked ones!)_

#### B. Invert / Exclude a Marker (`not`)

Run all fast tests by excluding the `@pytest.mark.slow` tag:

```bash
pytest -m "not slow" -v
```

**Terminal Output Sample:**

```text
collected 4 items / 1 deselected / 3 selected

tests/test_shapes.py::test_rectangle_instantiation PASSED                [ 33%]
tests/test_shapes.py::test_area PASSED                                   [ 66%]
tests/test_shapes.py::test_perimeter PASSED                              [100%]

======================== 3 passed, 1 deselected in 0.01s ========================
```

#### C. Combine Markers with Boolean Operators (`and`, `or`)

You can build compound filter expressions using `and`, `or`, and `not`:

```bash
# Run tests marked as BOTH 'smoke' AND 'database'
pytest -m "smoke and database"

# Run tests marked as EITHER 'smoke' OR 'database'
pytest -m "smoke or database"

# Run fast smoke tests (tagged 'smoke' but NOT 'slow')
pytest -m "smoke and not slow"
```

### 📋 Markers Quick Reference

| Command / Syntax                          | Description                                        |
| :---------------------------------------- | :------------------------------------------------- |
| `@pytest.mark.skip(reason="...")`         | Skips test unconditionally; logs reason            |
| `@pytest.mark.skipif(cond, reason="...")` | Skips test only if condition evaluates `True`      |
| `@pytest.mark.xfail(reason="...")`        | Expected failure; suite still succeeds if it fails |
| `@pytest.mark.<custom_name>`              | Tags test with a custom label                      |
| `pytest -m <marker>`                      | Runs **only** tests tagged with `<marker>`         |
| `pytest -m "not <marker>"`                | Runs all tests **except** those with `<marker>`    |
| `pytest -m "m1 and m2"`                   | Runs tests tagged with **both** markers            |
| `pytest -m "m1 or m2"`                    | Runs tests tagged with **either** marker           |
| `pytest --markers`                        | Lists all registered built-in and custom markers   |

---

## 🎭 11. Mocking: Testing Without Real Dependencies

### 💡 What is Mocking & Why Do We Need It?

In movies, an actor doesn’t jump off an actual exploding helicopter — a **stunt double** steps in to keep things safe, cheap, and predictable.

In software testing, **Mocking** means replacing a real dependency (like a database, an external payment API, an email service, or the system clock) with a fake stunt double called a **Mock**.

#### Why not just use the real services in tests?

1. **Speed:** A database query or network call takes 500ms; unit tests must execute in under 5ms.
2. **Reliability:** If the external service or internet goes down, your tests fail even when your code has no bugs.
3. **No Side Effects:** You don't want tests sending real emails to users or charging real credit cards.
4. **Simulating Errors:** It's difficult to force a real server to return an HTTP `500` error or a timeout. With a mock, you can trigger these errors on demand.

### Step 1: Simplest Mocking Example with `@mock.patch`

Let's start with the simplest possible example: mocking a single function using the `@mock.patch` decorator.

#### The Source Code (`source/users.py`)

Suppose `get_user()` calls another function `get_user_from_db()` that queries a real database:

```python
# source/users.py
def get_user_from_db(user_id):
    # Imagine this connects to an expensive, slow PostgreSQL database:
    users = {'1': 'Pushkar', '2': 'Sneha', '3': 'Trump'}
    return users[user_id]

def get_user(user_id):
    user = get_user_from_db(user_id)
    return user
```

#### The Test (`tests/test_users.py`)

We want to test `get_user()`, but **without hitting the real database**:

```python
# tests/test_users.py
import pytest
import unittest.mock as mock
import source.users as users

@mock.patch("source.users.get_user_from_db")
def test_get_user(mock_get_user_from_db):
    # 1. Program the mock to return a fake value
    mock_get_user_from_db.return_value = "Test user"

    # 2. Call the function under test
    username = users.get_user(2)

    # 3. Assert on the result
    assert username == "Test user"

    # 4. (Optional) Verify that the mock was called with the right argument
    mock_get_user_from_db.assert_called_once_with(2)
```

#### How this works:

1. `@mock.patch("source.users.get_user_from_db")` intercepts calls to `get_user_from_db`.
2. Pytest passes the created fake object as an argument into our test function (`mock_get_user_from_db`).
3. We set `mock_get_user_from_db.return_value = "Test user"`.
4. When `users.get_user(2)` runs, it calls our mock instead of the real database, instantly returning `"Test user"`.

### Step 2: Mocking Multiple Functions (Stacked `@mock.patch`)

What happens when your function depends on **more than one** external function? You simply stack multiple `@mock.patch` decorators.

#### The Code:

Suppose we add an email notification when retrieving or updating a user:

```python
# source/users.py
def get_user_from_db(user_id): ...
def send_login_notification(user_id): ...

def login_user(user_id):
    user = get_user_from_db(user_id)
    send_login_notification(user_id)
    return user
```

#### The Stack Order Gotcha:

Decorators in Python are applied **from the bottom up** (inside out).
Therefore, **the decorator closest to the `def` maps to the first argument**:

```python
# tests/test_users.py
@mock.patch("source.users.send_login_notification")  # 2nd parameter (top decorator)
@mock.patch("source.users.get_user_from_db")         # 1st parameter (bottom decorator)
def test_login_user(mock_get_user, mock_notify):
    mock_get_user.return_value = "Pushkar"
    mock_notify.return_value = True

    result = users.login_user("1")

    assert result == "Pushkar"
    mock_get_user.assert_called_once_with("1")
    mock_notify.assert_called_once_with("1")
```

> [!WARNING]
> **Order Rule:**
>
> - The decorator **closest** to `def test_...` matches the **first** parameter.
> - The decorator **above it** matches the **second** parameter, and so on.

### Step 3: Understanding `Mock()` vs. `patch`

A common question for beginners is: _What is the difference between `Mock()` and `patch`?_

| Tool          | What It Is             | Purpose                                                                                        | Analogy                                                      |
| :------------ | :--------------------- | :--------------------------------------------------------------------------------------------- | :----------------------------------------------------------- |
| **`Mock()`**  | A **Python object**    | Creates a blank fake object that you can give attributes and return values to.                 | The stunt double actor.                                      |
| **`patch()`** | A **tool / decorator** | Replaces a real function or class in your codebase with a `Mock()` for the duration of a test. | The casting director who puts the stunt double onto the set. |

#### Using `Mock()` Directly (Without `patch`)

You don't always need `patch`. If your function accepts an object or dependency as an argument (**Dependency Injection**), you can create a `Mock()` and pass it directly!

##### Example A: Passing a Mock Service into a Function

```python
from unittest.mock import Mock

def calculate_order_total(payment_gateway, amount):
    # Calls payment_gateway.charge(...)
    return payment_gateway.charge(amount)

def test_calculate_order_total():
    # Create a standalone mock object
    fake_gateway = Mock()
    fake_gateway.charge.return_value = True

    # Pass the fake object directly into the function
    success = calculate_order_total(fake_gateway, 99.99)

    assert success is True
    fake_gateway.charge.assert_called_once_with(99.99)
```

##### Example B: Building a Fake User Object on the Fly

```python
def test_mock_attributes():
    # Any attribute or method you call on Mock() works automatically!
    mock_user = Mock()
    mock_user.name = "Pushkar"
    mock_user.is_admin.return_value = True
    mock_user.get_roles.return_value = ["admin", "editor"]

    assert mock_user.name == "Pushkar"
    assert mock_user.is_admin() is True
    assert "admin" in mock_user.get_roles()
```

### Step 4: Real-World Example — Mocking an External API Request

In real-world applications, mocking third-party REST APIs (like weather APIs, GitHub, Stripe) is the most common use case.

Here, **`Mock()` and `patch()` work together**:

1. You use `Mock()` to construct a fake HTTP `response` object (`status_code`, `.json()`).
2. You use `@mock.patch` to replace `requests.get` so no real HTTP call ever leaves your computer.

#### The Source Code (`source/weather.py`):

```python
# source/weather.py
import requests

def get_current_temperature(city):
    """Fetches weather data from an external REST API."""
    try:
        response = requests.get(f"https://api.weather.com/v1/{city}", timeout=5)
        if response.status_code == 200:
            data = response.json()
            return data.get("temp")
        return None
    except requests.exceptions.Timeout:
        return "timeout"
```

#### Test 1: Successful API Response (Status 200)

```python
# tests/test_weather.py
from unittest.mock import patch, Mock
import source.weather as weather

@patch("source.weather.requests.get")
def test_get_current_temperature_success(mock_get):
    # 1. Build a fake HTTP response using Mock()
    mock_response = Mock()
    mock_response.status_code = 200
    mock_response.json.return_value = {"city": "Berlin", "temp": 22.5}

    # 2. Tell mock_get to return our fake response
    mock_get.return_value = mock_response

    # 3. Call the function
    temp = weather.get_current_temperature("Berlin")

    # 4. Verify outcome
    assert temp == 22.5
    mock_get.assert_called_once_with("https://api.weather.com/v1/Berlin", timeout=5)
```

#### Test 2: Handling Failures & Timeouts (`side_effect`)

Mocking makes testing network errors effortless using `side_effect`:

```python
import requests

@patch("source.weather.requests.get")
def test_get_current_temperature_timeout(mock_get):
    # Simulate a network timeout exception
    mock_get.side_effect = requests.exceptions.Timeout

    result = weather.get_current_temperature("Tokyo")

    assert result == "timeout"
```

### ⚠️ The Golden Rule: "Where to Patch?"

Always patch the object **where it is looked up/used**, NOT where it was originally defined:

- ❌ **Wrong:** `@mock.patch("requests.get")` — patches global `requests`, but `source/weather.py` may already have imported its own reference.
- ✅ **Right:** `@mock.patch("source.weather.requests.get")` — patches the exact reference that `source.weather` is calling.

### 📋 Mocking Cheat Sheet

| Syntax / Method                       | Purpose                                      | Example                                        |
| :------------------------------------ | :------------------------------------------- | :--------------------------------------------- |
| `@mock.patch("module.function")`      | Temporarily swaps out a function in a module | `@mock.patch("source.users.get_user_from_db")` |
| `Mock()`                              | Creates a blank fake object                  | `fake_response = Mock()`                       |
| `mock_obj.return_value = x`           | What the mock returns when called            | `mock_func.return_value = "Test"`              |
| `mock_obj.side_effect = Exception`    | Causes mock to raise an error when called    | `mock_get.side_effect = TimeoutError`          |
| `mock_obj.assert_called_once()`       | Verifies function was called exactly 1 time  | `mock_db.assert_called_once()`                 |
| `mock_obj.assert_called_once_with(x)` | Verifies exact arguments passed to call      | `mock_db.assert_called_once_with(2)`           |

---

## 🪄 12. Real-World Application: The Harry Potter Test Suite (AI Assisted)

The tutorial demonstrates using Large Language Models (ChatGPT 3.5 and ChatGPT 4) to rapidly generate boilerplate test code by combining everything covered so far: fixtures, parameterization, and markers.

### The AI Prompt

To generate the test suite, the exact prompt used was:

> _"Using pytest and the functions that come from it such as fixtures, parameterizers, and mark wherever necessary, test the following code and theme after Harry Potter."_

### The ChatGPT-4 Output & Implementation

ChatGPT-4 significantly outperformed 3.5 by natively utilizing parameterization and strict thematic rules. The generated suite included five total tests:

1. **Thematic Fixtures:**
   - It generated a `students` fixture returning a list of characters: Hermione, Harry, Ron, Draco Malfoy, Luna Lovegood, and Neville Longbottom.
   - It created a fixture for a `Transfiguration class`, setting Professor McGonagall as the teacher.

2. **The Tests:**
   - **`test_add_student`**: Added "Ginny Weasley" and asserted the new student was successfully in the list.
   - **`test_too_many_students`**: Attempted to add "Dean Thomas", verified it raised a "too many students" error, and then attempted to add "Parvati Patil".
   - **`test_remove_student`**: Used `@pytest.mark.parametrize` to run the removal logic iteratively for "Ron Weasley" and "Draco Malfoy".
   - **`test_change_teacher`**: Replaced McGonagall with "Alastor Moody".

### Debugging the AI Output

AI is not perfect. When running the generated tests, an import error occurred that had to be manually corrected to `source.School`. Additionally, an assertion failed because the initial prompt wasn't updated with the latest code state, which was fixed by manually removing "Seamus Finnigan" from the student list.

---

## ⚡ 13. Pytest CLI Execution Cheat Sheet

A comprehensive quick-reference table for running, targeting, filtering, and debugging tests from the command line.

### 📋 CLI Execution Cheat Sheet

| Goal / Execution Type | Command | Description |
| :--- | :--- | :--- |
| **Run All Tests** | `pytest` | Runs all discovered tests across the workspace |
| **Verbose Output** | `pytest -v` | Shows full test names and individual `PASSED` / `FAILED` statuses |
| **Quiet / Minimal Output** | `pytest -q` | Minimalist one-line output summary |
| **Live Print Output** | `pytest -s` | Disables stdout/stderr capture; displays all `print()` logs in real time |
| **Verbose + Live Prints** | `pytest -vs` | Most popular dev mode: full test names plus real-time console prints |
| **Single Directory** | `pytest tests/unit/` | Runs only tests residing inside a specific directory |
| **Single Test File** | `pytest tests/test_circle.py` | Runs all tests inside one specific file |
| **Single Standalone Function** | `pytest tests/test_my_functions.py::test_add` | Runs exactly one specific test function using node ID (`::`) |
| **Single Test Class** | `pytest tests/test_circle.py::TestCircle` | Runs all test methods contained inside a specific class |
| **Single Method in a Class** | `pytest tests/test_circle.py::TestCircle::test_area` | Runs exactly one test method inside a specific test class |
| **Filter by Keyword / Pattern** | `pytest -k "add"` | Runs any test whose name contains the substring `"add"` |
| **Compound Pattern Filtering** | `pytest -k "circle and not slow"` | Matches tests with `"circle"` in name, excluding those with `"slow"` |
| **Run by Marker** | `pytest -m smoke` | Runs only tests decorated with `@pytest.mark.smoke` |
| **Invert / Exclude Marker** | `pytest -m "not slow"` | Runs all tests **except** those decorated with `@pytest.mark.slow` |
| **Compound Marker Logic** | `pytest -m "smoke and not database"` | Combines markers using boolean operators (`and`, `or`, `not`) |
| **Stop on First Failure** | `pytest -x` | Halts the entire test session immediately upon the first failure |
| **Stop after N Failures** | `pytest --maxfail=2` | Halts test execution after reaching `N` failures |
| **Rerun Only Failures** | `pytest --lf` | (*Last Failed*) Reruns only tests that failed in the previous run |
| **Failed Tests First** | `pytest --ff` | (*Failed First*) Runs previous failures first, then runs the rest |
| **Debug on Failure (PDB)** | `pytest --pdb` | Automatically drops into Python's interactive debugger upon any failure |
| **Show Local Variables** | `pytest -l` (or `--showlocals`) | Prints local variables and their values inside failing tracebacks |
| **Short Tracebacks** | `pytest --tb=short` | Condenses error stack traces to only the most relevant lines |
| **Dry Run / List Tests** | `pytest --collect-only` | Discovers and prints all tests without actually executing them |
| **List Available Markers** | `pytest --markers` | Displays all registered built-in and custom markers |
| **List Available Fixtures** | `pytest --fixtures` | Displays all available fixtures and their locations |
