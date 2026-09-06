# Python Collections Module: Complete Guide & Reference

_A practical, beginner-friendly guide to Python's high-performance container datatypes._

- [Introduction: Why the `collections` Module?](#introduction-why-the-collections-module)
- [1. `Counter`: Counting and Frequency Maps](#1-counter-counting-and-frequency-maps)
  - [What is `Counter`?](#what-is-counter)
  - [Basic Usage and Dict Views](#basic-usage-and-dict-views)
  - [Different Ways to Initialize a `Counter`](#different-ways-to-initialize-a-counter)
  - [Finding the Most Common Elements (`mostcommon`)](#finding-the-most-common-elements-most_common)
  - [Reconstructing Elements (`elements()`)](#reconstructing-elements-elements)
  - [Missing Keys and Safe Lookups](#missing-keys-and-safe-lookups)
  - [Counter Arithmetic and Set Operations](#counter-arithmetic-and-set-operations)
  - [Updating Counts: `update()` vs `subtract()`](#updating-counts-update-vs-subtract)
- [2. `namedtuple`: Lightweight Object Structs](#2-namedtuple-lightweight-object-structs)
  - [What is `namedtuple`?](#what-is-namedtuple)
  - [Basic Definition and Instantiation](#basic-definition-and-instantiation)
  - [Different Ways to Define Field Names](#different-ways-to-define-field-names)
  - [Essential Helper Methods and Attributes](#essential-helper-methods-and-attributes)
  - [Setting Default Field Values](#setting-default-field-values)
  - [Modern Alternatives: `typing.NamedTuple` and `@dataclass`](#modern-alternatives-typingnamedtuple-and-dataclass)
- [3. `OrderedDict`: Order-Aware Dictionary](#3-ordereddict-order-aware-dictionary)
  - [What is `OrderedDict`?](#what-is-ordereddict)
  - [Is `OrderedDict` Still Needed in Modern Python?](#is-ordereddict-still-needed-in-modern-python)
- [4. `defaultdict`: Dictionaries Without `KeyError`](#4-defaultdict-dictionaries-without-keyerror)
  - [What is `defaultdict`?](#what-is-defaultdict)
  - [Basic Usage with Built-in Types](#basic-usage-with-built-in-types)
  - [How Can We Set a Custom Default Value?](#how-can-we-set-a-custom-default-value)
  - [Real-World Example: Grouping Data](#real-world-example-grouping-data)
  - [Critical Gotcha: Read Access Mutates the Dictionary!](#critical-gotcha-read-access-mutates-the-dictionary)
- [5. `deque`: High-Performance Double-Ended Queue](#5-deque-high-performance-double-ended-queue)
  - [What is `deque`?](#what-is-deque)
  - [Time Complexity Comparison](#time-complexity-comparison)
  - [Basic Operations: Appends and Pops](#basic-operations-appends-and-pops)
  - [Extending Left vs Right: The Direction Trap](#extending-left-vs-right-the-direction-trap)
  - [Rotating Elements (`rotate`)](#rotating-elements-rotate)
  - [Fixed-Size Sliding Windows (`maxlen`)](#fixed-size-sliding-windows-maxlen)
- [6. Bonus: `ChainMap`: Merging Contexts Without Copying](#6-bonus-chainmap-merging-contexts-without-copying)
  - [What is `ChainMap`?](#what-is-chainmap)
- [7. Quick Reference & Decision Matrix](#7-quick-reference-decision-matrix)

---

## Introduction: Why the `collections` Module?

Python comes with basic built-in collections: `list`, `dict`, `tuple`, and `set`. While versatile, handling specific tasks (like counting items, remembering insertion order, or building queues) using only built-ins often requires writing repetitive, inefficient code.

The built-in `collections` module provides specialized, high-performance container datatypes that solve common programming challenges cleanly and efficiently.

```text
+------------------------------------------------------------------------+
|                          collections Module                            |
+------------------------------------------------------------------------+
|  Counter      | Tracks frequencies of elements automatically           |
|  namedtuple   | Tuples with named fields (accessible via dot notation) |
|  OrderedDict  | Dictionary with order-specific manipulation methods    |
|  defaultdict  | Dictionary that provides defaults for missing keys     |
|  deque        | Double-ended queue with O(1) appends and pops on ends  |
|  ChainMap     | Combines multiple mappings into a single lookup view   |
+------------------------------------------------------------------------+
```

---

## 1. `Counter`: Counting and Frequency Maps

### What is `Counter`?

A `Counter` is a dictionary subclass designed specifically for counting hashable objects. It stores elements as dictionary keys and their counts as dictionary values.

### Basic Usage and Dict Views

```python
from collections import Counter

# 1. Initialize from a string
text = "aaaabbbbbbccccdd"
my_counter = Counter(text)

print(my_counter)
# Output: Counter({'b': 6, 'a': 4, 'c': 4, 'd': 2})

# Counter provides standard dictionary views:
print(my_counter.items())
# Output: dict_items([('a', 4), ('b', 6), ('c', 4), ('d', 2)])

print(my_counter.keys())
# Output: dict_keys(['a', 'b', 'c', 'd'])

print(my_counter.values())
# Output: dict_values([4, 6, 4, 2])
```

### Different Ways to Initialize a `Counter`

You can construct a `Counter` from any iterable, a mapping, or keyword arguments:

```python
from collections import Counter

# From a list of numbers
numbers = [10, 10, 10, 20, 30, 20, 30, 40]
c1 = Counter(numbers)
print(c1)
# Output: Counter({10: 3, 20: 2, 30: 2, 40: 1})

# From an existing dictionary
c2 = Counter({'apples': 5, 'oranges': 2})
print(c2)
# Output: Counter({'apples': 5, 'oranges': 2})

# Using keyword arguments
c3 = Counter(cats=4, dogs=7)
print(c3)
# Output: Counter({'dogs': 7, 'cats': 4})
```

### Finding the Most Common Elements (`most_common`)

The `most_common(k)` method returns the $k$ most frequent elements and their counts, sorted in descending order:

```python
from collections import Counter

my_counter = Counter("aaaabbbbbbccccdd")

# Get top 2 most common elements
print(my_counter.most_common(2))
# Output: [('b', 6), ('a', 4)]

# Get the #1 most common element and unpack its tuple
top_one = my_counter.most_common(1)[0]
print(top_one)
# Output: ('b', 6)

top_element, top_count = top_one
print(f"Top element is '{top_element}' with count {top_count}")
# Output: Top element is 'b' with count 6

# If no argument is passed, it returns ALL elements sorted by count:
print(my_counter.most_common())
# Output: [('b', 6), ('a', 4), ('c', 4), ('d', 2)]
```

### Reconstructing Elements (`elements()`)

The `elements()` method returns an iterator over elements, repeating each as many times as its count:

```python
from collections import Counter

my_counter = Counter({'a': 4, 'b': 2, 'c': 1})

# elements() returns an itertools chain iterator
print(my_counter.elements())
# Output: <itertools.chain object at 0x...>

# Convert to a list to view all items:
print(list(my_counter.elements()))
# Output: ['a', 'a', 'a', 'a', 'b', 'b', 'c']

# Iterate directly:
for item in my_counter.elements():
    print(item, end=" ")
# Output: a a a a b b c
print()
```

### Missing Keys and Safe Lookups

Unlike regular Python dictionaries which raise a `KeyError` when accessing a key that doesn't exist, a `Counter` returns `0`:

```python
from collections import Counter

counts = Counter({'apples': 3, 'bananas': 2})

print(counts['apples'])  # Output: 3
print(counts['pears'])   # Output: 0 (No KeyError!)
```

### Counter Arithmetic and Set Operations

`Counter` supports powerful mathematical operations:

```python
from collections import Counter

c1 = Counter(a=3, b=1, c=4)
c2 = Counter(a=1, b=2, c=1)

# Addition: adds counts together
print(c1 + c2)
# Output: Counter({'a': 4, 'c': 5, 'b': 3})

# Subtraction: keeps only positive results
print(c1 - c2)
# Output: Counter({'c': 3, 'a': 2})  (b is 1 - 2 = -1, so it is excluded)

# Intersection (min of each count):
print(c1 & c2)
# Output: Counter({'a': 1, 'b': 1, 'c': 1})

# Union (max of each count):
print(c1 | c2)
# Output: Counter({'c': 4, 'a': 3, 'b': 2})

# Total sum of all counts (Python 3.10+)
print(c1.total())
# Output: 8
```

### Updating Counts: `update()` vs `subtract()`

```python
from collections import Counter

inventory = Counter({'pens': 10, 'books': 5})

# Add incoming shipment
inventory.update({'pens': 5, 'erasers': 4})
print(inventory)
# Output: Counter({'pens': 15, 'books': 5, 'erasers': 4})

# Sell items
inventory.subtract({'pens': 3, 'books': 2})
print(inventory)
# Output: Counter({'pens': 12, 'books': 3, 'erasers': 4})
```

---

## 2. `namedtuple`: Lightweight Object Structs

### What is `namedtuple`?

Standard Python tuples are fast and immutable, but accessing elements by index (`p[0]`, `p[1]`) can make code hard to read and maintain.

`namedtuple` creates tuple subclasses where each position has an identifier. You can access values by name (`p.x`, `p.y`) or by index (`p[0]`, `p[1]`), with zero memory overhead compared to regular tuples.

### Basic Definition and Instantiation

```python
from collections import namedtuple

# Define the namedtuple blueprint: (TypeName, FieldNames)
Point = namedtuple('Point', 'x,y')

# Create an instance
p = Point(1, -4)

# Print representation
print(p)
# Output: Point(x=1, y=-4)

# Access by field name:
print(p.x, p.y)
# Output: 1 -4

# Access by index:
print(p[0], p[1])
# Output: 1 -4
```

### Different Ways to Define Field Names

You can specify fields as:

- A comma-separated string: `'x, y'` or `'x,y'`
- A space-separated string: `'x y'`
- A list or tuple of strings: `['x', 'y']`

```python
from collections import namedtuple

# All three definitions are equivalent:
PointA = namedtuple('Point', 'x, y')
PointB = namedtuple('Point', 'x y')
PointC = namedtuple('Point', ['x', 'y'])

p = PointC(10, 20)
print(p)
# Output: Point(x=10, y=20)
```

### Essential Helper Methods and Attributes

All built-in helper methods of `namedtuple` start with an underscore `_` to avoid conflicts with your field names.

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'city'])
person = Person(name='Alice', age=30, city='Seattle')

# 1. Convert to a dictionary (_asdict)
person_dict = person._asdict()
print(person_dict)
# Output: {'name': 'Alice', 'age': 30, 'city': 'Seattle'}

# 2. Create a modified copy (_replace)
# Remember: tuples are immutable, so _replace returns a NEW tuple!
older_person = person._replace(age=31)
print(older_person)
# Output: Person(name='Alice', age=31, city='Seattle')

# 3. Create an instance from an iterable or list (_make)
data = ['Bob', 25, 'Chicago']
bob = Person._make(data)
print(bob)
# Output: Person(name='Bob', age=25, city='Chicago')

# 4. View all field names (_fields)
print(Person._fields)
# Output: ('name', 'age', 'city')
```

### Setting Default Field Values

You can provide default values using the `defaults` argument (applied from right to left):

```python
from collections import namedtuple

# 'status' defaults to 'active'
User = namedtuple('User', ['username', 'role', 'status'], defaults=['active'])

u1 = User('john_doe', 'admin')
print(u1)
# Output: User(username='john_doe', role='admin', status='active')

u2 = User('jane_doe', 'editor', status='suspended')
print(u2)
# Output: User(username='jane_doe', role='editor', status='suspended')
```

### Modern Alternatives: `typing.NamedTuple` and `@dataclass`

While `collections.namedtuple` is standard, modern Python offers typed alternatives:

| Feature                  | `collections.namedtuple` | `typing.NamedTuple`     | `dataclasses.dataclass`                       |
| :----------------------- | :----------------------- | :---------------------- | :-------------------------------------------- |
| **Type hints**           | No                       | Yes                     | Yes                                           |
| **Mutability**           | Immutable                | Immutable               | Mutable (default) / Immutable (`frozen=True`) |
| **Methods & Properties** | Hard to add              | Easy (class definition) | Easy (class definition)                       |
| **Inheritance**          | Tuple subclass           | Tuple subclass          | Custom class                                  |

```python
from typing import NamedTuple

class Car(NamedTuple):
    brand: str
    year: int
    electric: bool = False

c = Car('Tesla', 2023, electric=True)
print(c)
# Output: Car(brand='Tesla', year=2023, electric=True)
```

---

## 3. `OrderedDict`: Order-Aware Dictionary

### What is `OrderedDict`?

An `OrderedDict` is a dictionary subclass that maintains keys in the exact order they were inserted.

```python
from collections import OrderedDict

ordered_dict = OrderedDict()
ordered_dict['a'] = 1
ordered_dict['c'] = 3
ordered_dict['b'] = 2
ordered_dict['d'] = 4

print(ordered_dict)
# Output: OrderedDict({'a': 1, 'c': 3, 'b': 2, 'd': 4})

for key, value in ordered_dict.items():
    print(key, value)
# Output:
# a 1
# c 3
# b 2
# d 4
```

### Is `OrderedDict` Still Needed in Modern Python?

Since Python 3.7, standard Python dictionaries (`dict`) are guaranteed to maintain insertion order. However, `OrderedDict` provides specialized capabilities that regular dictionaries do not:

#### 1. Order-Sensitive Equality

Regular dicts compare equal if their keys and values match, regardless of order. `OrderedDict` checks both content **and** order.

```python
from collections import OrderedDict

# Regular dictionaries:
d1 = {'a': 1, 'b': 2}
d2 = {'b': 2, 'a': 1}
print(d1 == d2)
# Output: True (Order is ignored!)

# OrderedDicts:
od1 = OrderedDict({'a': 1, 'b': 2})
od2 = OrderedDict({'b': 2, 'a': 1})
print(od1 == od2)
# Output: False (Order matters!)
```

#### 2. Reordering Elements (`move_to_end`)

Allows moving an existing key to the beginning or end of the dictionary:

```python
from collections import OrderedDict

od = OrderedDict({'a': 1, 'b': 2, 'c': 3})

# Move key 'a' to the very end
od.move_to_end('a')
print(od)
# Output: OrderedDict({'b': 2, 'c': 3, 'a': 1})

# Move key 'c' to the front (last=False)
od.move_to_end('c', last=False)
print(od)
# Output: OrderedDict({'c': 3, 'b': 2, 'a': 1})
```

#### 3. Popping from Front or Back (`popitem`)

While regular `dict.popitem()` only removes the last inserted item (LIFO), `OrderedDict.popitem(last=False)` removes from the front (FIFO):

```python
from collections import OrderedDict

od = OrderedDict({'first': 1, 'second': 2, 'third': 3})

# Pop the first item (FIFO queue behavior)
front = od.popitem(last=False)
print(front)
# Output: ('first', 1)

# Pop the last item (LIFO stack behavior)
back = od.popitem(last=True)
print(back)
# Output: ('third', 3)
```

Because of `move_to_end` and `popitem(last=False)`, `OrderedDict` is the classic tool for building **LRU (Least Recently Used) Caches**.

---

## 4. `defaultdict`: Dictionaries Without `KeyError`

### What is `defaultdict`?

When you query or assign to a missing key in a regular `dict`, Python raises a `KeyError`.

A `defaultdict` solves this by accepting a callable "factory" function as its first argument. When an accessed key does not exist, `defaultdict` automatically invokes this factory function to generate and insert a default value.

### Basic Usage with Built-in Types

```python
from collections import defaultdict

# 1. Using int as factory: default value is int() -> 0
d_int = defaultdict(int)
d_int['x'] = 5
d_int['y'] = 7
print(d_int['x'])    # Output: 5
print(d_int['foo'])  # Output: 0 (Automatically created!)

# 2. Using float as factory: default value is float() -> 0.0
d_float = defaultdict(float)
print(d_float['bar'])  # Output: 0.0

# 3. Using list as factory: default value is list() -> []
d_list = defaultdict(list)
d_list['fruits'].append('apple')
d_list['fruits'].append('banana')
print(d_list['fruits'])  # Output: ['apple', 'banana']
print(d_list['veggies']) # Output: [] (Created as empty list)
```

### How Can We Set a Custom Default Value?

In `db2.py`, the question was asked: _"How can we set a different default value?"_

The factory parameter must be a **callable** (a function that takes no arguments). You can pass a `lambda` or a custom function:

```python
from collections import defaultdict

# Using a lambda function:
d_custom = defaultdict(lambda: 100)
print(d_custom['missing_score'])
# Output: 100

d_msg = defaultdict(lambda: "Status: Pending")
print(d_msg['order_42'])
# Output: Status: Pending

# Using a standard function:
def generate_default_profile():
    return {"tier": "free", "credits": 10}

users = defaultdict(generate_default_profile)
print(users['guest_user'])
# Output: {'tier': 'free', 'credits': 10}
```

### Real-World Example: Grouping Data

Grouping items by a shared attribute is one of the most common applications of `defaultdict(list)`:

```python
from collections import defaultdict

students = [
    ("Alice", "Science"),
    ("Bob", "Math"),
    ("Charlie", "Science"),
    ("Diana", "Arts"),
    ("Ethan", "Math"),
]

# Group students by subject
grouped_by_subject = defaultdict(list)

for name, subject in students:
    grouped_by_subject[subject].append(name)

for subject, student_names in grouped_by_subject.items():
    print(f"{subject}: {', '.join(student_names)}")

# Output:
# Science: Alice, Charlie
# Math: Bob, Ethan
# Arts: Diana
```

### Critical Gotcha: Read Access Mutates the Dictionary!

When you simply read or check a missing key with bracket syntax `d[key]`, `defaultdict` **creates and stores** that key:

```python
from collections import defaultdict

d = defaultdict(int)
print(len(d))  # Output: 0

# Just reading a non-existent key:
val = d['ghost_key']

# The key now exists in the dictionary!
print(len(d))  # Output: 1
print(dict(d)) # Output: {'ghost_key': 0}
```

If you want to check whether a key exists without inadvertently creating it:

- Use `if key in d:` (does **not** insert the key).
- Use `d.get(key, default)` (returns default without inserting).

---

## 5. `deque`: High-Performance Double-Ended Queue

### What is `deque`?

`deque` (pronounced "deck") stands for **Double-Ended Queue**.

While a standard Python `list` is optimized for fast $O(1)$ operations at the end (`append` and `pop`), inserting or deleting from the beginning (`list.insert(0, val)` or `list.pop(0)`) requires shifting all remaining elements in memory, costing **$O(n)$ time**.

A `deque` is implemented as a doubly linked list of blocks, providing fast **$O(1)$** additions and removals from **both ends**.

### Time Complexity Comparison

| Operation                  | Python `list` | `collections.deque`       |
| :------------------------- | :------------ | :------------------------ |
| Append right (`append`)    | $O(1)$        | $O(1)$                    |
| Append left (`appendleft`) | $O(n)$        | $O(1)$                    |
| Pop right (`pop`)          | $O(1)$        | $O(1)$                    |
| Pop left (`popleft`)       | $O(n)$        | $O(1)$                    |
| Random Access (`d[i]`)     | $O(1)$        | $O(n)$ (slower in middle) |

### Basic Operations: Appends and Pops

```python
from collections import deque

g = deque()

# Adding elements to right and left
g.append(1)
g.append(2)
print(g)  # Output: deque([1, 2])

g.appendleft(3)
print(g)  # Output: deque([3, 1, 2])

# Removing elements from right and left
popped_right = g.pop()
print(popped_right)  # Output: 2
print(g)             # Output: deque([3, 1])

popped_left = g.popleft()
print(popped_left)   # Output: 3
print(g)             # Output: deque([1])
```

### Extending Left vs Right: The Direction Trap

Notice how `extendleft()` behaves when passing multiple items:

```python
from collections import deque

g = deque([1])

# extend() adds items to the right in order:
g.extend([7, 8, 9])
print(g)
# Output: deque([1, 7, 8, 9])

# extendleft() iterates over the input and prepends each element one by one.
# 7 is added first, then 8, then 9. Resulting order is reversed!
g.extendleft([7, 8, 9])
print(g)
# Output: deque([9, 8, 7, 1, 7, 8, 9])
```

### Rotating Elements (`rotate`)

The `rotate(n)` method shifts elements circularly:

- **Positive `n`:** Rotates to the right (forward).
- **Negative `n`:** Rotates to the left (backward).

```python
from collections import deque

g = deque([10, 20, 30, 40, 50])

# Rotate right by 2 places (items wrap from back to front)
g.rotate(2)
print(g)
# Output: deque([40, 50, 10, 20, 30])

# Rotate left by 1 place (items wrap from front to back)
g.rotate(-1)
print(g)
# Output: deque([50, 10, 20, 30, 40])
```

### Fixed-Size Sliding Windows (`maxlen`)

One of the most powerful features of `deque` is the optional `maxlen` parameter. Once the deque reaches its maximum capacity, adding items to one end automatically discards items from the opposite end:

```python
from collections import deque

# Keep only the last 3 logged events
recent_logs = deque(maxlen=3)

recent_logs.append("Login: User A")
recent_logs.append("Upload: File 1")
recent_logs.append("Download: File 2")
print(recent_logs)
# Output: deque(['Login: User A', 'Upload: File 1', 'Download: File 2'], maxlen=3)

# Adding a 4th event automatically drops the oldest item ("Login: User A")
recent_logs.append("Logout: User A")
print(recent_logs)
# Output: deque(['Upload: File 1', 'Download: File 2', 'Logout: User A'], maxlen=3)
```

Use `maxlen` for:

- Recent history buffers / undo stacks
- Moving averages in streaming data
- Fixed-size caching

---

## 6. Bonus: `ChainMap`: Merging Contexts Without Copying

### What is `ChainMap`?

`ChainMap` groups multiple dictionaries or mappings into a single, updateable view. Instead of copying data (like `{**dict1, **dict2}` or `dict1.update(dict2)`), `ChainMap` keeps references to the underlying dictionaries.

Lookups check each dictionary in order from left to right:

```python
from collections import ChainMap

# Practical use case: Configuration resolution order
default_config = {'theme': 'light', 'port': 8000, 'debug': False}
env_config     = {'port': 5000}
cli_args       = {'theme': 'dark'}

# CLI overrides Environment, which overrides Defaults
app_config = ChainMap(cli_args, env_config, default_config)

# 'theme' found in cli_args
print(app_config['theme'])  # Output: dark

# 'port' found in env_config
print(app_config['port'])   # Output: 5000

# 'debug' found in default_config
print(app_config['debug'])  # Output: False
```

Modifying a `ChainMap` only writes to the **first** dictionary in the chain, leaving default settings completely untouched:

```python
app_config['new_setting'] = True
print(cli_args)        # Output: {'theme': 'dark', 'new_setting': True}
print(default_config)  # Output: {'theme': 'light', 'port': 8000, 'debug': False}
```

---

## 7. Quick Reference & Decision Matrix

| Container         | Best Used For                                     | Key Advantage over Standard Types                                      |
| :---------------- | :------------------------------------------------ | :--------------------------------------------------------------------- |
| **`Counter`**     | Counting items, frequency maps, histograms        | Fast counting, `.most_common()`, math operations (`+`, `-`, `&`, `\|`) |
| **`namedtuple`**  | Storing structured records, database rows, points | Memory-efficient, readable dot syntax (`obj.field`), immutable         |
| **`OrderedDict`** | LRU caches, order-sensitive comparisons           | `.move_to_end()`, `.popitem(last=False)`, order-aware equality         |
| **`defaultdict`** | Grouping items, tallying without prior checks     | No `KeyError`, cleaner code without `if key not in d:` checks          |
| **`deque`**       | Queues, stacks, BFS traversal, sliding windows    | Fast $O(1)$ operations on both ends, bounded size with `maxlen`        |
| **`ChainMap`**    | Layered configurations, scoped contexts           | Zero-copy chaining, non-destructive default fallback                   |
