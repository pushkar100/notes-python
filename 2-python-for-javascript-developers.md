# Python for JavaScript Developers Notes

Learning Python as a JavaScript developer by comparing the syntax and constructs of each language with the other.

- [Python for JavaScript Developers Notes](#python-for-javascript-developers-notes)
  * [Basics](#basics)
    + [Opening a REPL](#opening-a-repl)
    + [Data types](#data-types)
    + [Type casting](#type-casting)
    + [Variables](#variables)
      - [Declaring a variable](#declaring-a-variable)
      - [Data type of a variable](#data-type-of-a-variable)
      - [Default value of a variable](#default-value-of-a-variable)
      - [Re-assigning variables](#re-assigning-variables)
      - [Variable naming rules](#variable-naming-rules)
      - [Variable naming conventions](#variable-naming-conventions)
    + [Printing to console](#printing-to-console)
    + [Comments](#comments)
      - [Single-line comments](#single-line-comments)
      - [Multi-line comments](#multi-line-comments)
    + [Strings](#strings)
      - [Defining a string](#defining-a-string)
      - [Changing the case of strings](#changing-the-case-of-strings)
      - [Concatenating strings](#concatenating-strings)
      - [Escaping characters in a string](#escaping-characters-in-a-string)
      - [Stripping whitespaces from strings](#stripping-whitespaces-from-strings)
      - [Casting a value into a string](#casting-a-value-into-a-string)
    + [Numbers](#numbers)
      - [Arithmetic operations on integers](#arithmetic-operations-on-integers)
      - [Floating point numbers](#floating-point-numbers)
      - [Casting a value into a number](#casting-a-value-into-a-number)
    + [Boolean values](#boolean-values)
    + [Lists](#lists)
      - [Defining a list](#defining-a-list)
      - [Accessing a list item](#accessing-a-list-item)
      - [Modifying a list item](#modifying-a-list-item)
      - [Appending an item to a list](#appending-an-item-to-a-list)
      - [Inserting an item to a list](#inserting-an-item-to-a-list)
      - [Deleting an item from a list](#deleting-an-item-from-a-list)
      - [Searching for an item in a list](#searching-for-an-item-in-a-list)
      - [Sorting a list](#sorting-a-list)
      - [Reversing a list](#reversing-a-list)
      - [Length of a list](#length-of-a-list)
      - [Index error when selecting a list item](#index-error-when-selecting-a-list-item)

## Basics

**Versions used**
- Python version: `3+`
- JavaScript version: `ES6+`

### Opening a REPL

Read, Evaluate, Print, Loop (REPL) program is an easy way to test out language constructs quickly

In Python, we use the python REPL
- Make sure python3 is supported by typing `python` and viewing the version number when the REPL starts
- Usually, it is better to use the `ipython` REPL since it is a bit more enhanced program

_Comparison with JavaScript:_
- We can use a browser console as the REPL
- If using NodeJS, typing `node` should open up the Node JS REPL on our system
- Check the node version using `node -v`

### Data types

1. Numeric
  1. Integer (`int`)
  2. Float (`float`)
  3. Complex Number
2. String (`str`)
3. Boolean (`bool`): There are two values, `True` and `False`
4. Dictionary (`{}`)
5. Sequence
  1. Lists (`[]`)
  2. Tuples (`()`)
6. None

There are many more advanced types. 

_Comparison with JavaScript:_
- In python too, `int`, `float`, etc are internal representations of a **Number or numeric** type - same as in JavaScript
- In JavaScript, the boolean values `true` and `false` are **not** capitalized
- **Dictionary** is what we call as an **object** in JavaScript
- **Lists** are nothing but **arrays** in JavaScript
- **Tuples** are a special type of a list. They are like fixed size, immutable arrays in JavaScript
- `None` is an empty type when a function returns nothing. It is similar to `undefined` in JavaScript
- JavaScript has more built-in types: `NaN`, Symbol

### Type casting

1. Converting to a string: **`str()`**
2. Converting to an integer: **`int()`**
3. Converting to a float: **`float()`**

Other data types have similar functions

_Comparison with JavaScript:_
- Converting a number: `Number()`
- Parsing a string as an integer: `parseInt()`
- Parsing a string as a float: `parseFloat()`
- String conversion is usually done with string interpolation

### Variables

#### Declaring a variable

```python
variable = value
```

Example:
```python
my_name = 'Pushkar'
```

_Comparison with JavaScript:_
- JavaScript variable declarations are prefixed with a scope identifier like `var`, `const`, `let`

#### Data type of a variable

Python is dynamically typed i.e The type of a variable is inferred at runtime and is updated when the assignment changes
Example
```python
my_name = 'Pushkar' # string
my_name = 20 # integer
```

_Comparison with JavaScript:_
- JavaScript is also dynamically typed

#### Default value of a variable

Declaration comes with assignment. Both have to be done

```python
foo # NameError: name 'foo' is not defined

foo = 'bar' # ✓
```

_Comparison with JavaScript:_
- In JavaScript, it is possible to have variable declarations that are unassigned
- The value in such a case will be `undefined`

#### Re-assigning variables

Variables can be re-assigned in Python

```python
foo = 5
foo = 'bar' # ✓
```

_Comparison with JavaScript:_
- In JavaScript, only `var` and `let` can be re-assigned.
- However, `const` cannot be re-assigned (In fact, it has to be assigned a value at the time of declaration)

#### Variable naming rules

1. Only the following characters are allowed in Python variable names:
  1. Letters (`a-z` and `A-Z`)
  2. Numbers (`0-9`)
  3. Underscore (`_`)
2. A variable name cannot start with a Number (`0-9`)
3. Avoid Python keywords (i.e reserved words) while naming variable. Else, it causes errors.

```python
my_name # ✓
_my_name # ✓
my_name_1 # ✓
my_1_name # ✓
1_my_name # ✕
with # ✕ (Python keyword)
```

_Comparison with JavaScript:_
- These rules apply to JavaScript as well but with one difference: `$`
- `$` is allowed in JavaScript variable names and can even begin with it
- Every other rule is the same

#### Variable naming conventions

Python uses **`snake_case`** for naming things like variables, function names and so on as a convention

```python
my_car
foo_bar
```

Only class names use `PascalCase`.

_Comparison with JavaScript:_
- The convention in JavaScript is to use `camelCase` for variables, functions, etc
- Classes use the `PascalCase`

### Printing to console

Use the `print()` statement

```python
name = 'Pushkar'
print('Hello, ' + name + '!') # Prints: Hello, Pushkar!
```
Note about Python2:
- We do not use parentheses to print stuff out: `print 'Hello, ' + name + '!'`
- If we add parentheses, the behaviour can be a bit different from the python3 `print()` statement

_Comparison with JavaScript:_
- In JavaScript, we use `console.log()` to print to the browser or node console (terminal)

### Comments

#### Single-line comments

Use a `#` (pound) symbol

```python
# This is a single line comment 
japanese_restaurant.open_restaurant() # This is a single line comment
```

#### Multi-line comments

Use multiple `#` (pound) symbols. One for each 

```python
# This is a single line comment 
# but we can use multiple such lines
# to make multi-line comments
japanese_restaurant.open_restaurant() # This is a single line comment
```

Note:
- There exists a comment style using `"""` to begin and end a comment. 
- However, these comments are called **docstrings** used to document a unit of code
- They should appear when a function or class begins. This text will appear in the generated documentation.

```python
def foo():
  """I am a docstring. This function prints 'foo'"""
  print('foo')
```

_Comparison with JavaScript:_
- Single line comments: `//`
- Multi line comments: Multiple `//` or `/* ... */`
- There are no docstrings (There used to be a library called `@jsdoc` for it but the syntax is different)

### Strings

#### Defining a string

Use `''` or `""` (Single or double quotes)

_Comparison with JavaScript:_
- Same in JavaScript but you can also use the ` `` ` for strings with interpolation

#### Changing the case of strings

**1. Capitalize a string using `.capitalize()`**

Only updates the first letter to be upper case in the string (instead of every word in the string)

```python
x = 'pushkar dk'
x.capitalize() # 'Pushkar dk'
```
Does not affect the original string variable (immutable)

**2. Title-ify a string using `.title()`**

```python
x = 'pushkar dk'
x.title() # 'Pushkar Dk'
```
Does not affect the original string variable (immutable)

**3. Change to upper case using `.upper()`**

```python
x = 'pushkar dk'
x.upper() # 'PUSHKAR DK'
```
Does not affect the original string variable (immutable)

**4. Change to upper case using `.lower()`**

```python
x = 'pushkar dk'
x.lower() # 'pushkar dk'
```
Does not affect the original string variable (immutable)

_Comparison with JavaScript:_
- The corresponding string method for uppercasing is: `.toUpperCase()`
- The corresponding string method for lowercasing is: `.toLowerCase()`
- There is not built-in method to title-ify or capitalize every word in a string in JavaScript

#### Concatenating strings

In python, we use the `+` symbol to concatenate strings.
However, in order to concatenate non-string values with strings (Ex: integers), we must typecast them first (Ex: `str()`)
```python
'my ' + 'name is ' + 'Pushkar' + ' and I am ' + 15 + ' years old' # ✕
'my ' + 'name is ' + 'Pushkar' + ' and I am ' + str(15) + ' years old' # ✓
```

_Comparison with JavaScript:_
- In JavaScript, you can use the same `+` operator to concatenate strings
- However, **sometimes** we do not have to explicitly convert numbers. JS will try type coerce them into a string
  - Ex: `'My age is' + 15 // 'My age is 15'`
- There is another way to build strings in JS: Interpolation. 
  - Ex: `age = 15; x = `My age is ${age}`;`

#### Escaping characters in a string

1. Escape newlines with `\n`
2. Escape tabs with `\t`
3. Escape characters with a backslash. Ex: `\"` and `\'`

_Comparison with JavaScript:_
- Same

#### Stripping whitespaces from strings

**1. Remove whitespace from the right of a string with `.rstrip()`**

```python
name = '  pushkar  '
name.rstrip() # '  pushkar'
```

**2. Remove whitespace from the left of a string with `.lstrip()`**

```python
name = '  pushkar  '
name.lstrip() # 'pushkar  '
```

**3. Remove all leading and trailing spaces with `.strip()`**

```python
name = '  pushkar  '
name.strip() # 'pushkar'
```

_Comparison with JavaScript:_
- In JavaScript, we originally only had a `.trim()` method to trim all leading and trailing spaces (Like `.strip()`)
- In later versions. [`.trimEnd()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trimEnd) and [`.trimStart()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trimStart) have been added with good browser support

#### Casting a value into a string

Use the `str()` function

```python
str(4) # '4'
str(True) # 'True'
```

_Comparison with JavaScript:_
- In JavaScript, we use the `String()` function or just type coerce by `''` or `""` or ` `${}` `

### Numbers

#### Arithmetic operations on integers

Operators: `+` (Add), `-` (Subtract), `*` (Multiply), `/` (Divide), `//` (Integer division), `**` (Exponent), `%` (Modulo)

```python
2 + 3 # 5
3 - 2 # 1
3.2 / 5 # 0.64
14 // 5 # 2 (Divides and returns only the integer quotient)
2 ** 5 # 32
15 % 4 # 3 (Returns the remainder)
```

Note involving division in Python2:
- Division causes integer division by default.
- `3 / 2 # 1`. To avoid this, make sure at least one of the values is a `float`
- `3 / float(2) # 1.5`

#### Floating point numbers

Use the decimal point (`.`) to represent floating point numbers
```python
0.245
```

Floating point numbers have a precision problem.
```python
0.2 + 0.1 # 0.30000000000000004
```

- The same arithmetic operations that apply to integers apply to floating point values also

_Comparison with JavaScript:_
- Same
- In JavaScript too we have the floating point precision problem! :/ 

#### Casting a value into a number

**1. Casting a string to a number**

```python
int('133') # 133
int('133x') # ✕ (Error)
```

**2. Casting a string to a float**

```python
float('133') # 133.0
float('133.11') # 133.11
float('133x') # ✕ (Error)
```

**3. Casting a boolean to an integer**

```python
int(True) # 1
int(False) # 0
```

**4. Casting a boolean to a float**

```python
float(True) # 1.0
float(False) # 0.0
```

_Comparison with JavaScript:_
- We can use similar functions to explicitly cast values: `Number()`, `parseInt()`, `parseFloat()`
- Sometimes, we end up implicitly type-casting (type coercion) one type to another. 

### Boolean values

- The boolean type is represented by `bool`
- There are two boolean values: `True` and `False`
- A conditional expression results in a boolean value always
- Many values can be typecast into a boolean

```python
5 > 1 # True
'Pushkar' == 'Pushkar Dk' # False

bool(1) # True
bool(0) # False

bool('x') # True
bool('1') # True
bool('0') # True
bool('') # False
```

_Comparison with JavaScript:_
- Same
- However, the two values are represented in lower case (`true` and `false`)
- Explicit typecasting can be done with `Boolean()` but also there is a concept of **Truthy** and **Falsy** values

### Lists 

Lists are arrays (collection of items in an order) in which we can add items of different types.

The indices start from `0` like most other languages, including JavaScript.

#### Defining a list

Use square brackets (`[]`)

```python
cities = ['Delhi', 'Bangalore', 'London']
print(cities) # ['Delhi', 'Bangalore', 'London']
```

We can have mixed items in the list

```python
foo = [10, 'bar', { 'a': 1 }]
print(foo) # [10, 'bar', {'a': 1}]
```

_Comparison with JavaScript:_
- Same

#### Accessing a list item

**1. Accessing a list item using the index inside square brackets (`[]`)**
```python
foo = [10, 'bar', { 'a': 1 }]
foo[1] # 'bar'
```

**2. Accessing the last item of a list**

We can access it by the ending index or by using `-1` as the index.
```python
foo = [10, 'bar', { 'a': 1 }]
foo[2] # {'a': 1} (2 is the last index)
foo[-1] # {'a': 1} (-1 refers to the first element from the end of the list)

# Can access more elements from the end of the list
foo[-2] # 'bar' (second last element)
```

**3. Accessing the first item of a list using `0` index**
```python
foo = [10, 'bar', { 'a': 1 }]
foo[0] # 10
```

_Comparison with JavaScript:_
- Almost the same!
- However, we do **not** have **negative indices** (Ex: `-1`) to access the elements of a list starting backwards from the end of it

#### Modifying a list item

Use the square bracket notation to access the item and assign it using `=`
```python
foo = [10, 'bar', { 'a': 1 }]
foo[0] = 'blah'
foo[0] # 'blah'
```

_Comparison with JavaScript:_
- Same

#### Appending an item to a list

Use the `.append()` method
```python
foo = [10, 'bar', { 'a': 1 }]
foo.append(20)
foo # [10, 'bar', {'a': 1}, 20]
```

`.append()` method allows us to dynamically build a list.

_Comparison with JavaScript:_
- In JavaScript, we use the `.push()` method

#### Inserting an item to a list

Use the `.insert()` method
- It takes two arguments: An index and a value
- The value is insert at the index
- The earlier set of items starting from that index is shifted to the right
```python
foo = [10, 'bar', { 'a': 1 }]
foo.insert(1, 20)
foo # [10, 20, 'bar', {'a': 1}, 20]
```

_Comparison with JavaScript:_
- There is a method called `.splice()`
- `.splice()` has a different syntax. It takes at least 3: 
  - Index
  - Number of existing elements to delete from index
  - The elements to insert at index (can be one or many comma separated values)
- Other ways to do it:
  - Use rest & spread `...`operators (Immutable way) `[...existing elements, new element, ...remaing elements]`

#### Deleting an item from a list

**1. Removing an item from anywhere in a list using the index**
- Use the `del` operator
- Use the `.pop(index)` method to remove an element from the given index
  - The method returns the removed top element for post-processing
```python
foo = [10, 'bar', { 'a': 1 }]
del foo[1]
foo # [10, {'a': 1}]

foo = [10, 'bar', { 'a': 1 }]
foo.pop(1) # 'bar'
foo # [10, {'a': 1}]
```

_Comparison with JavaScript:_
- There is no `del` operator
- Again, you can use the `.splice()` method without inserting any elements but only removing them
- The `.pop()` method in JavaScript is used to remove **only** the last element

**2. Removing an item from the end of a list**
- Use the `.pop()` method (i.e without `index` argument)
- The method returns the removed top element for post-processing
```python
foo = [10, 'bar', { 'a': 1 }]
foo.pop() # { 'a': 1 }
foo # [10, 'bar']
```

_Comparison with JavaScript:_
- Same. There is a `.pop()` method in JavaScript arrays too. 
- It too returns the removed top element

**3. Removing an item by value from the beginning of a list**
- Again, use the `del` operator
```python
foo = [10, 'bar', { 'a': 1 }]
del foo[0]
foo # ['bar', { 'a': 1 }]
```

_Comparison with JavaScript:_
- Use the `.shift()` method. It also returns the removed first element

**4. Removing an item by value from a list**
- Use the `.remove()` method
- This method removes only the **first matching element** of a list
```python
foo = [10, 'bar', { 'a': 1 }]
foo.remove('bar')
foo # [10, {'a': 1}]
```

Note: 
- To remove the second matching value, run the `.remove()` method a second time, and so on.
- To remove all occurrences, use a while loop

_Comparison with JavaScript:_
- No method like `.remove()` in JS
- Use `Array.filter(filterMethod)` (functional programming) (OR) 
- Use `.indexOf(value)` to find the first index of an item and then `.splice()` to remove it

#### Searching for an item in a list

**1. Searching for an item in a list**
- Use an `in` expression (Returns `True` or `False` based on existence of the value)
- Use a `.count()` method. It returns the number of occurrences of that value in the list.
```python
10 in foo # True
'google' in foo # False

foo = [10, 'bar', { 'a': 1 }]
foo.count('bar') # 1
foo.count('google') # 0
```

_Comparison with JavaScript:_
- Use the `.includes(value)` method

**2. Fetching the index of an item in a list**
- Use `.index()` method. It returns an index if first occurrence is found else raises a `ValueError` exception
```python
foo = [10, 'bar', { 'a': 1 }]
foo.index('bar') # 1

foo.index('baz') # ✕ (ValueError)
```

_Comparison with JavaScript:_
- Use the `.indexOf(value)` method to get the index of the first occurrence of the value
- Use the `.lastIndexOf(value)` method to get the index of the last occurrence of the value

#### Sorting a list

- Use the `.sort()` method to alphabetically sort it (But, it fails for mixed elements' list) (Mutable)
- To temporarily sort it (immutably), use the built-in `sorted()` function
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
foo.sort()
foo # ['aa', 'aba', 'b', 'bi', 'c', 'coo']
```

```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
sorted(foo) # ['aa', 'aba', 'b', 'bi', 'c', 'coo']
foo # ['aa', 'b', 'aba', 'c', 'coo', 'bi']
```

Note:
- Both `.sort()` and `sorted()` can take a keyword argument `reverse=True` to reverse sort
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
sorted(foo, reverse=True) # ['coo', 'c', 'bi', 'b', 'aba', 'aa']
foo # ['aa', 'b', 'aba', 'c', 'coo', 'bi']
```
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
foo.sort(reverse=True)
foo # ['coo', 'c', 'bi', 'b', 'aba', 'aa']
```
- Both `.sort()` and `sorted()` take a `key` argument that is a function (takes one argument) to define the custom sorting technique
```python
def sort_fn(b):
  return len(b)

foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
foo.sort(key=sort_fn)
foo # ['b', 'c', 'aa', 'bi', 'aba', 'coo']
```

_Comparison with JavaScript:_
- There is a `.sort()` method. Sorts it alphabetically by default
- It can take a custom sorting functio (takes two arguments) as an argument but it does not have a `reverse` option
- Your sorting method must manually reverse it if needed
- There is no built-in `sorted()` function

#### Reversing a list 

Reversing is not equal to reverse sorting. This is completely different.

- Use the `.reverse()` method. This mutates the list
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
foo.reverse()
foo # ['bi', 'coo', 'c', 'aba', 'b', 'aa']
```

Comparison with JavaScript:
- Same. The `.reverse()` method mutates the array too.

#### Length of a list

Use the `len` function
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
len(foo) # 6
```

_Comparison with JavaScript:_
- We need to use an array method called `.length()`. Ex: `foo.length()`

#### Index error when selecting a list item 

When requesting an item at an index that does not exist for a list.
- Python throws an `IndexError`
```python
foo = ['aa', 'b', 'aba', 'c', 'coo', 'bi']
foo[6] # ✕ (IndexError: list index out of range)

foo[-1] # 'bi'

foo[-6] # 'aa'

foo[-7] # ✕ (IndexError: list index out of range)
```

_Comparison with JavaScript:_
- JavaScript simply returns an `undefined` value for out-of-bounds indices i.e No error
- However, if you search for an out-of-bounds index item and try to process it, then you may get an error depending on the operation.
- JavaScript does not have negative index search from the end of a list but even a negative out-of-bounds item check returns `undefined`
