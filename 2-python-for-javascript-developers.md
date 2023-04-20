# Python notes for JavaScript developers

Learning Python as a JavaScript developer by comparing the syntax and constructs of each language with the other.

- [Python notes for JavaScript developers](#python-notes-for-javascript-developers)
  * [Basics](#basics)
    + [Opening a REPL](#opening-a-repl)
    + [Data types](#data-types)
    + [Finding the type of a value](#finding-the-type-of-a-value)
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
      - [Slicing a list to work with a part of it](#slicing-a-list-to-work-with-a-part-of-it)
      - [Copying a list](#copying-a-list)
      - [Check if two lists are the same](#check-if-two-lists-are-the-same)
      - [Creating immutable lists aka Tuples](#creating-immutable-lists-aka-tuples)
      - [Looping through items in a list](#looping-through-items-in-a-list)
    + [Generate a series of integers](#generate-a-series-of-integers)
      - [Skipping values while generating a series of integers](#skipping-values-while-generating-a-series-of-integers)
      - [Creating a list from a range of integers](#creating-a-list-from-a-range-of-integers)
      - [Looping through a series of integers](#looping-through-a-series-of-integers)
      - [Using list comprehension to combine list creation with generating a range of integers](#using-list-comprehension-to-combine-list-creation-with-generating-a-range-of-integers)
      - [Simple statistics with a list of numbers](#simple-statistics-with-a-list-of-numbers)
    + [Conditional checks](#conditional-checks)
      - [Equality checks](#equality-checks)
      - [Comparing numerical values](#comparing-numerical-values)
    + [Logical operators](#logical-operators)
      - [Making sure both conditions are true](#making-sure-both-conditions-are-true)
      - [Making sure at least one condition is true](#making-sure-at-least-one-condition-is-true)
    + [If statements](#if-statements)
      - [An if statement](#an-if-statement)
      - [An if-else statement](#an-if-else-statement)
      - [An if-elif-else chain](#an-if-elif-else-chain)
      - [If statements with lists](#if-statements-with-lists)
    + [User input](#user-input)
    + [Looping](#looping)
      - [For loop](#for-loop)
      - [While loop](#while-loop)
      - [Using break to exit a loop](#using-break-to-exit-a-loop)
      - [Using continue to skip a loop interation](#using-continue-to-skip-a-loop-interation)
    + [Dictionaries](#dictionaries)
      - [Defining a dictionary](#defining-a-dictionary)
      - [Empty dictionary](#empty-dictionary)
      - [Accessing a value in an dictionary](#accessing-a-value-in-an-dictionary)
      - [Adding a new key-value pair to a dictionary](#adding-a-new-key-value-pair-to-a-dictionary)
      - [Modifying values in a dictionary](#modifying-values-in-a-dictionary)
      - [Removing key-value pairs from a dictionary](#removing-key-value-pairs-from-a-dictionary)
      - [Looping through key-value pairs in dictionaries](#looping-through-key-value-pairs-in-dictionaries)
      - [Looping through just the values in dictionaries](#looping-through-just-the-values-in-dictionaries)
      - [Looping through just the keys in dictionaries](#looping-through-just-the-keys-in-dictionaries)
      - [Nesting dictionaries](#nesting-dictionaries)
      - [List of dictionaries](#list-of-dictionaries)
      - [Dictionary containing lists](#dictionary-containing-lists)
    + [Sets](#sets)
      - [Defining a set](#defining-a-set)
      - [Fetching a set value](#fetching-a-set-value)
      - [Checking if a set contains a value](#checking-if-a-set-contains-a-value)
      - [Adding a value to a set](#adding-a-value-to-a-set)
      - [Removing a value from a set](#removing-a-value-from-a-set)
      - [Size of a set](#size-of-a-set)
      - [Looping through a set](#looping-through-a-set)
    + [Functions](#functions)
      - [Defining a function](#defining-a-function)
      - [Docstring for a function in python](#docstring-for-a-function-in-python)
      - [Parameters for a function](#parameters-for-a-function)
      - [Keyword arguments in Python](#keyword-arguments-in-python)
      - [Unmatched arguments in Python cause an error](#unmatched-arguments-in-python-cause-an-error)
      - [Declaring default arguments](#declaring-default-arguments)
      - [Return value of a function](#return-value-of-a-function)
      - [Passing an arbitrary number of arguments](#passing-an-arbitrary-number-of-arguments)
      - [Passing an arbitrary number of keyword arguments](#passing-an-arbitrary-number-of-keyword-arguments)
      - [Passing a value by reference and by value](#passing-a-value-by-reference-and-by-value)
    + [Modules](#modules)
      - [Importing an entire module](#importing-an-entire-module)
      - [Importing a specific function](#importing-a-specific-function)
      - [Defining an alias while importing a function](#defining-an-alias-while-importing-a-function)
      - [Defining an alias while importing the whole module](#defining-an-alias-while-importing-the-whole-module)
      - [Importing all functions from a module](#importing-all-functions-from-a-module)
    + [Classes](#classes)
      - [Defining a class](#defining-a-class)
      - [Instantiating a class](#instantiating-a-class)
      - [Accessing attributes and methods](#accessing-attributes-and-methods)
      - [Default attribute values](#default-attribute-values)
      - [Modifying an attribute value](#modifying-an-attribute-value)
      - [Inheritance](#inheritance)
      - [Importing classes](#importing-classes)
    + [Files](#files)
      - [Opening a file](#opening-a-file)
      - [Closing a file](#closing-a-file)
      - [Correctly opening and closing a file](#correctly-opening-and-closing-a-file)
      - [Reading the entire contents of a file](#reading-the-entire-contents-of-a-file)
      - [Reading the file contents one line at a time](#reading-the-file-contents-one-line-at-a-time)
      - [Storing lines of a file into a list](#storing-lines-of-a-file-into-a-list)
      - [Writing to a file](#writing-to-a-file)
      - [Appending to file](#appending-to-file)
      - [Loading and dumping JSON data](#loading-and-dumping-json-data)
    + [Exceptions](#exceptions)
    + [Unit testing your code](#unit-testing-your-code)
      - [Unit test](#unit-test)
      - [Test case](#test-case)
      - [Creating a test case](#creating-a-test-case)
      - [Understanding the test case output](#understanding-the-test-case-output)
      - [Common assertions](#common-assertions)
      - [Setup code](#setup-code)
    + [Python standard library](#python-standard-library)

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
 - Integer (`int`)
 - Float (`float`)
 - Complex Number
2. String (`str`)
3. Boolean (`bool`): There are two values, `True` and `False`
4. Dictionary (`{}`)
5. Sequence
 - Lists (`[]`)
 - Tuples (`()`)
6. None

There are many more advanced types that are imported from core libraries or third party modules 

_Comparison with JavaScript:_
- In python too, `int`, `float`, etc are internal representations of a **Number or numeric** type - same as in JavaScript
- In JavaScript, the boolean values `true` and `false` are **not** capitalized
- **Dictionary** is what we call as an **object** in JavaScript
- **Lists** are nothing but **arrays** in JavaScript
- **Tuples** are a special type of a list. They are like fixed size, immutable arrays in JavaScript
- `None` is an empty type when a function returns nothing. It is similar to `undefined` in JavaScript
- JavaScript has more built-in types: `NaN`, Symbol

### Finding the type of a value

Use the `type()` function

```python
type(5) # int
type(5.0) # float
type('Hello') # str
type([1, 2, 3]) # list
type({ 'a': 1, 'b': 2 }) # dict

def foo():
  print('Foo')

type(foo) # function

type(SomeClass) # type (? unsure)
```

_Comparison with JavaScript:_
- Use the `typeof` operator / expression.

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
- There is no `del` operator (There is a `delete` operator but usually used with objects. On lists it marks the item as empty rather than removing it - quirky behaviour)
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
- Interestingly, trying to dynamically define a value for an out-of-bounds array index, **JS creates the item**! It extends the array length
 - It fills the empty indices in-between as `undefined`!

#### Slicing a list to work with a part of it

**1. Slice a list to create a subset (immutable)**
- Use the `list[start:end]` syntax
- It includes the start index item but not the end index one
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
foo[2:5] # [{'a': 1}, 20, 30]

foo # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]
```

**2. Slice a list from the beginning of a list (immutable)**
- Omit the start index: `list[:end]`
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
foo[:4] # [10, 'bar', {'a': 1}, 20]

foo # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]
```

**3. Slice a list that includes the end of a list (immutable)**
- Omit the end index: `list[start:]`
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
foo[4:] # [30, 4.1, True]

foo # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]
```

**4. Slice the last few items from a list (immutable)**
- Use a negative index for the start and omit the end: `list[-start:]`
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
foo[-3:] # [30, 4.1, True]

foo # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]
```

**5. Using a sliced subset in a for loop**
- Use a `for` loop (i.e `for-in`) on the sliced list
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
for item in foo[3:5]:
  print(item)

# 20
# 30
```

_Comparison with JavaScript:_
- Use the spread (`...`) operator to generate new arrays (immutably) (or)
- Use the `.slice()` method for generating a subset (immutably)

#### Copying a list

Use `list[:]` to copy a list
- This is useful when you want to pass by value instead of by reference so that the original list is not tampered with
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]
x = foo[:]

x # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]

x[1] = 'changed'
x # [10, 'changed', {'a': 1}, 20, 30, 4.1, True]
foo # [10, 'bar', {'a': 1}, 20, 30, 4.1, True]
```

Note: To hold the reference simply assign the original list to a variable or pass it by name to a function

_Comparison with JavaScript:_
- Use the spread (`...`) operator to generate new arrays (immutably) (or)
- Use the `.slice()` method for generating a subset (immutably)

#### Check if two lists are the same

- The `==` operator on lists match the lists **by value**! 
- In order to match lists by reference, use the `is` expression! (i.e check if the variables point to the same list in memory)
```python
foo = [10, 'bar', { 'a': 1 }, 20, 30, 4.1, True]

# Copied list
x = foo[:]
x == foo # True (Matches by value)
x is foo # False (Matches by reference)

# Same reference
x = foo
x == foo # True (Matches by value)
x is foo # True (Matches by reference)
```

_Comparison with JavaScript:_
- In JavaScript, both equality (`==`) and strict equality (`===`, types must match too!) match **by reference**!
- In order to compare two lists by value in JS,
  - Try looping through them and matching individual items (OR)
  - Use a `JSON.stringify()` method and then compare (OR)
  - Use the `.toString()` return value and then compare (OR)
  - Use `.every()` to match the value at the index of current array with the value at the index of the other array

#### Creating immutable lists aka Tuples

Tuples are immutable lists that cannot be changed!
1. They are represented by parentheses `()` rather than square brackets `[]`
2. Tuples cannot be altered once created
  - We cannot modify an item
  - We cannot insert / append an item
  - We cannot delete an item
3. List methods also work on tuples except those that try to mutate it (in which case we get an error)
4. Variables assigned to a tupl can, however, be re-assigned (either to another tuple or a value of another data type)
```python
record = (14, 'Pushkar', 'Desai', 29)

# Accessing an item
record[1] # 'Pushkar

# Modifying an item (Error)
record[1] = 3 # ✕ (TypeError: 'tuple' object does not support item assignment)

# Appending/Inserting an item (Error)
record.append(10) # ✕ (AttributeError: 'tuple' object has no attribute 'append')

# Re-assigning a variable containing a tuple
record = 10
record # 10
```

_Comparison with JavaScript:_
- Tuples do not exist in JavaScript!
- Typecheckers like **TypeScript** and **Flow** can enforce this new type. However, executable JS can never contain it

#### Concatenating lists

Use the `+` operator on two list operands to create a new list

```python
foo = ['x', 'y', 'z']
bar = [5, 6, 7]
print(foo + bar) # ['x', 'y', 'z', 5, 6, 7]
```

_Comparison with JavaScript:_
- Use the spread operator: `[...arr_1, ...arr_2]`

#### Replicating lists

Use the `*` on a list and an integer to replicate the list that many times

```python
foo = ['x', 'y', 'z']

print(foo * 3) # ['x', 'y', 'z', 'x', 'y', 'z', 'x', 'y', 'z']
```

_Comparison with JavaScript:_
- Such an operator does not exist. Do it manually using loops or a `.reduce()`/`.map()` logic

#### Looping through items in a list

**1. Loop through items using a for (`for-in`) loop**
- Can choose any name for the temporary variable in the loop (Ex: `for temporary_variable in list_to_loop:`)
- Do not forget the trailing colon `:` of the `for` statement
- The body of the for loop must be indented by one additional tab from the left (Python is meant to be easy to read)
```python
foo = [10, 15, 4, 20, 69, 30, 4.1]

for num in foo:
  print(num)

# 10
# 15
# 4
# 20
# 69
# 30
# 4.1
```

**2. Using the loop variable outside the loop**
- The loop variable is accessible outside of the for loop! 
- It will contain the last value of the list after the for loop has!
```python
foo = [10, 15, 4, 20, 69, 30, 4.1]

for num in foo:
  print(num)

num # 4.1
```

_Comparison with JavaScript:_
- In JavaScript, only the `var` keyword loop variable is available outside the loop since it is function scoped. 
- It will also contain the last item value.
- `let` loop variable is block scoped, so it will not be available outside the loop (Trying to access it will throw an error)

### Generate a series of integers

Use the `range()` function
- It begins from a start integer and finishes before an end integer (does not include it)!
- It has no output or return of its own, but we can use it for loops!
```python
# Range of the first four natural numbers
range(1, 5) # Generates a series of numbers: 1, 2, 3, 4
```

#### Skipping values while generating a series of integers

The `range()` function can take a third argument: A step value
- The default step value is `1` so we don't have to write it for continuous integers
- If we supply a step, it skips the in-between values
```python
# Even numbers from 0 to 10
range(0, 11, 2) # Generates a series of numbers: 0, 2, 4, 6, 8, 10
```

#### Creating a list from a range of integers

Use a special syntax with a list method invocation with an argument of a range function invocation:
- Ex: `list(range(start, end, [step]))`
```python
natural_nums = list(range(1, 11)) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odd_nums = list(range(1, 11, 2)) # [1, 3, 5, 7, 9]
```

#### Looping through a series of integers

Use the for (`for-in`) loop over a `range()` function (instead of a list or object)
```python
print('First few odd numbers:')
for odd in range(1, 11, 2):
  print(odd)

# First few odd numbers:
# 1
# 3
# 5
# 7
# 9
```

_Comparison with JavaScript:_
- Nothing like this `range()` function exists built in to JS! 
- We need to build our own custom iterator & generator functions to make this happen.

#### Using list comprehension to combine list creation with generating a range of integers

Shorthand for combining two operations:
1. Generating a series of integers AND
2. Creating a list from those integers

The syntax is: `[<expression> for <loopvariable> in <range_function>]` where the `expression` depends on the `loopvariable`

```python
odd_cubes = [odd ** 3 for odd in range(1, 11, 2)]
odd_cubes # [1, 27, 125, 343, 729]

# The above code is equivalent to:
# odd_cubes = []
# for odd in range(1, 11, 2):
#   odd_cubes.append(odd ** 3)
```

_Comparison with JavaScript:_
- Such a shorthand does not exist in JS!

#### Simple statistics with a list of numbers

**1. Minimum value of a list of numbers**

Use `min()`
```python
even_nums = [2, 4, 6, 8 , 10]
min(even_nums) # 2
```

**2. Maximum value of a list of numbers**

Use `max()`
```python
even_nums = [2, 4, 6, 8 , 10]
max(even_nums) # 10
```

**3. Sum of a list of numbers**

Use `sum()`
```python
even_nums = [2, 4, 6, 8 , 10]
sum(even_nums) # 30
```

_Comparison with JavaScript:_
- Use the `Math` core module: `Math.min(...even_nums)`, `Math.max(...even_nums)`. We need to spread out the array into many arguments of array items.
- For finding the sum, use the `.reduce()` method and supply it a reducer function that adds successive items and an accumulator

### Conditional checks

Conditional checks return boolean values.

#### Equality checks

- Use `==` for equality
- Use `!=` for inequality

```python
'foo' == 5 # False
13.4 == 13.4 # True

# Lists and Dictionaries are matched BY VALUE:
['a', 'b'] == ['a', 'b'] # True
['a', 'b'] != ['a', 'b'] # False

{ 'a': 5 } == { 'a': 5 } # True
{ 'a': 5 } != { 'a': 5 } # False
```

**Note**: Use the `is` expression to match lists and dictionaries BY REFERENCE
```python
# Lists and Dictionaries are matched BY VALUE:
['a', 'b'] is ['a', 'b'] # False
{ 'a': 5 } is { 'a': 5 } # False
```

_Comparison with JavaScript:_
- In JavaScript, we use the same operators `==` and `!=` for equality checks
- However, since type coercion happens, it is more common to use `===` and `!==` for strict equality (Value + Type exact match)
- Note that for objects & arrays, the default match is **BY REFERENCE** (opposite of python)
  - If you wish to match objects and lists by value, loop through them or use functional programming methods (`.some`, `.every`)

#### Comparing numerical values

- `<`: Less than a value check
- `>`: Greather than a value check
- `<=`: Less than or equal to a value check
- `>=`: Greater than or equal to a value check
```python
2 < 4 # True
2 <= 4 # True
2 > 4 # False
2 >= 4 # False

# Comparing alphabetically:
'aa' > 'ab' # False
'aa' <= 'ab' # True
```

_Comparison with JavaScript:_
- Same.

### Logical operators

#### Making sure both conditions are true

- Use the `and` operator (`condition1 and condition2`)

```python
6 >= 5 and 6 < 10 # True
6 >= 5 and 6 >= 10 # False
```

#### Making sure at least one condition is true

- Use the `or` operator (`condition1 or condition2`)

```python
6 >= 5 or 6 < 10 # True
6 >= 5 or 6 >= 10 # True
6 >= 10 or 7 < 3 # False
```

_Comparison with JavaScript:_
- Same, but the corresponding operators in JavaScript are `&&` for and-ing and `||` for or-ing.

### If statements

If statement introduces branching in our programs based on a condition.
We can even branch based on multiple conditions or a default condition.

- *Indentation by one tab inside an if statement is mandatory* (Applies to loop statement bodies as well!)
- *Do not forget the trailing colon (`:`)* at the end of the if statement (Applies to loop statements as well!)
 
#### An if statement

Syntax:
```python
if condition:
  do something
```

```python
if 6 > 5:
  print('5 is greater than 6')
# '6 is greater than 5'

if 5 > 6:
  print('5 is greater than 6')
# Prints nothing
```

#### An if-else statement

- Do not forget the `else` and the colon (`:`) for it

Syntax:
```python
if condition:
  do something
else:
  do some other thing
```

```python
if 6 > 5:
  print('6 is greater than 5')
# '6 is greater than 5'

if 5 > 6:
  print('5 is greater than 6')
else:
# Prints nothing
```

#### An if-elif-else chain

```python
name = 'Pushkar'
if name == 'push':
  print('name is push')
elif name == 'dk':
  print('name is dk')
else:
  print('dunno the name')

# 'dunno the name'
```

**Note**: Omitting the `else` block. This block is optional

```python
name = 'Pushkar'
if name == 'push':
  print('name is push')
elif name == 'dk':
  print('name is dk')
elif name == 'Pushkar:
  print('name is Pushkar')

# 'name is Pushkar'
```

_Comparison with JavaScript:_
- Same `if` behaviour. 
- The syntax is different though. We use `{ ... }` to contain the statement if it is more than one line
- We do not use tabs for the statement body and no colon `:` at the end of an if statement

#### If statements with lists

**1. Checking a particular item exists in a list**

- Use the `in` condition to check for the existence of a value
- Use the above condition in an `if` statement

```python
cities = ['Bangkok', 'Bangalore', 'London', 'Chennai']
'Bangalore' in cities # True

if 'Bangalore' in cities:
  print('Bangalore is a city')
else:
  print('Bangalore is not a city')

# Bangalore is a city
```

**2. Checking a particular item does not exist in a list**

- Use the `not in` condition to check for the non-existence of a value
- Use the above condition in an `if` statement

```python
cities = ['Bangkok', 'Bangalore', 'London', 'Chennai']
'Bangalore' not in cities # False

if 'Bangalore' not in cities:
  print('Bangalore is not a city')
else:
  print('Bangalore is a city')

# Bangalore is a city
```

**3. Checking for an empty list**

- When the name of the list is used in a for loop as the conditional: It returns `True` if it is **not empty** (Else, `False`)
```python
cities = ['Bangkok', 'Bangalore', 'London', 'Chennai']
if cities:
  print('There is at least one city in the list')
else:
  print('There are no cities in the list')

# There is at least one city in the list
```

_Comparison with JavaScript:_
- In JavaScript, we can check for the existence of a value in an array with either `.includes()` or `.indexOf() !== -1`
- Checking for an empty array is slightly different: 
  - The name of the array returns true as long as it is, in fact, an array (& not `undefined` or a falsy value)!
  - Use the `.length` or `.length > 0` conditional to make sure the list is not empty!

### User input

**1. Accepting user input**

Use the `input()` method.
- It takes one argument: A string _prompt_
- The return value is a **string**
- Store the return value in a variable
- The python interpreter pause while executing `input()` so that the user can input a value
- After providing the input, press **ENTER**

```python
message = input('What is your message?')
# What is your message?Nothing
message # 'Nothing'

message = input('What is your message?\n')
# What is your message?
# Nothing much
message # 'Nothing much'
```

**Note:** Accepting user input in Python 2.7
- Use `raw_input()` function instead
- The `input()` method in Python2.7 tries to execute the input string as code
- This is a security risk (Similar to `eval()` in JavaScript)

**2. Storing input as a number**

Default input type is a string.
To store a numerical value, typecast it into a number like `int()` or `float()`

```python
favourite_num = int(input('Enter your favourite number between 1 & 100? '))
# Enter your favourite number between 1 & 100? 45
favourite_num # 45
```

_Comparison with JavaScript:_
- In JavaScript, we use the `prompt()` function to prompt the user to type something in a GUI dialog
- This works in a browser & similar to python, will be a string value that is returned
- However, in NodeJS console, we need to read from `process.stdin` and output to `process.stdout` ([An example](https://nodejs.dev/en/learn/accept-input-from-the-command-line-in-nodejs/))

### Looping

#### For loop

**Loops through all the items of a list**

- Syntax: `for loopvariable(s) in iterable:`
- Do not forget to (a) Indent the body of the if by one tab, and (b) Add a trailing colon (`:`)

```python
for value in [1, 10, 6, 23]:
  print('value: ' + str(value))
# value: 1
# value: 10
# value: 6
# value: 23

for num in range(1, 11):
  print(num)
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
```

_Comparison with JavaScript:_
- The most basic `for` loop in JavaScript has the following syntax:
  - `for (initialization; condition; afterthought) statement` where the statement can also be a complex statement within `{...}`
- There are two variations of a for loop:
  1. `for...in` loop: Iterate over all the entries of an object (Ex: iterates over properties of an `{}` object)
  2. `for...of` loop: Iterate over iterable object (Ex: Array (`[]`), Map, Set, arguments, ...)

#### While loop

**Loops until a condition is true**
- Syntax: `while condition:`
- Do not forget to (a) Indent the body of the if by one tab, and (b) Add a trailing colon (`:`)

```python
active = True

while active:
  name = input('What is your name? ')
  if name == 'quit':
    active = False
  else:
    print('Your name is ' + name)

# What is your name? Pushkar
# Your name is Pushkar
# What is your name? Rahul
# Your name is Rahul
# What is your name? Vandana
# Your name is Vandana
# What is your name? quit
```

#### Using break to exit a loop

Use `break`

```python
for num in range(1,6):
  if num == 4:
    break
  print('num: ' + str(num))
# num: 1
# num: 2
# num: 3

num = 1
while num < 6:
  if num == 4:
    break
  print('num: ' + str(num))
  num = num + 1
# num: 1
# num: 2
# num: 3
```

_Comparison with JavaScript:_
- Same.

#### Using continue to skip a loop interation

Use `continue`

```python
for num in range(1,6):
  if num == 4:
    continue
  print('num: ' + str(num))
# num: 1
# num: 2
# num: 3
# num: 5

num = 1
while num < 6:
  if num == 4:
    num = num + 1
    continue
  print('num: ' + str(num))
  num = num + 1
# num: 1
# num: 2
# num: 3
# num: 5
```

_Comparison with JavaScript:_
- Same.

### Dictionaries

A dictionary is a set of **key-value** pairs.

#### Defining a dictionary

- Use `{ 'key': value }` syntax

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals # {'India': 'New Delhi', 'United Kingdom': 'London', 'France': 'Paris'}
```

- Using a key other than string is also allowed (Ex: lists, dictionaries, functions, numbers, boolean)
```python
def some_method():
  print('I am some method')

some_method # <function __main__.some_method()>

complex_key_object = { some_method: 10 }

complex_key_object # {<function __main__.some_method()>: 10}
```

_Comparison with JavaScript:_
- Dictionaries in JavaScript are known as objects `{}`. The syntax is pretty much the same.
- Keys for objects can only be **strings** or a **Symbol**.
- For string keys, you do not need to wrap the keys in quotes (`'` or `"`) but in Python, you need to!
- If you want to assign other types as keys (Ex: objects, functions, etc) then use a `Map` or a `WeakMap`

#### Empty dictionary

Use `{}`
- Useful for dynamically building up key-value pairs in your program (similar to dynamically building a list of items)

```python
empty_dict = {}
empty_dict # {}
```

_Comparison with JavaScript:_
- Same.

#### Accessing a value in an dictionary

Use the square bracket notation `[]`

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}
country_capitals['India'] # 'New Delhi'
```

_Comparison with JavaScript:_
- Same.

#### Adding a new key-value pair to a dictionary

Use the square bracket notation `[]`

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals['Sri Lanka'] = 'Colombo'

country_capitals
# {'India': 'New Delhi',
#  'United Kingdom': 'London',
#  'France': 'Paris',
#  'Sri Lanka': 'Colombo'}
```

_Comparison with JavaScript:_
- Same.

#### Modifying values in a dictionary

Use the square bracket notation `[]`

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals['India'] = 'Bangalore'

# {'India': 'Bangalore',
#  'United Kingdom': 'London',
#  'France': 'Paris',
#  'Sri Lanka': 'Colombo'}
```

_Comparison with JavaScript:_
- Same.

#### Removing key-value pairs from a dictionary

Use the `del` keyword

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

del country_capitals['India']

country_capitals # {'United Kingdom': 'London', 'France': 'Paris'}
```

_Comparison with JavaScript:_
- Use the `delete` operator in a similar way.

#### Looping through key-value pairs in dictionaries

Use `.items()` to get the key-value pairs as list of tuple items (Each tuple = key, value).

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals.items() # dict_items([('India', 'New Delhi'), ('United Kingdom', 'London'), ('France', 'Paris')])

for key, value in country_capitals.items():
  print('key ' + key + ' | ' + value)

# key India | New Delhi
# key United Kingdom | London
# key France | Paris
```
**Note:** Order of keys is not guaranteed while looping through dictionary keys!

_Comparison with JavaScript:_
- We can use an object method called `Object.entries(objectVariable)` to get an array of the key-value pairs.

#### Looping through just the values in dictionaries

Use `.values()` to get just the keys in a list

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals.values() # dict_values(['New Delhi', 'London', 'Paris'])

for value in country_capitals.values():
  print('value: ' + value)

# value: New Delhi
# value: London
# value: Paris
```

**Note:** If you want to maintain the order of the values in the list, you can do so using the sorted() function on the return of `.keys()`

_Comparison with JavaScript:_
- We can use a similar object method called `Object.values(objectVariable)` to get an array of the values.

#### Looping through just the keys in dictionaries

Use `.keys()` to get just the keys in a list

```python
country_capitals = {
  'India': 'New Delhi',
  'United Kingdom': 'London',
  'France': 'Paris'
}

country_capitals.keys() # dict_keys(['India', 'United Kingdom', 'France'])

for key in country_capitals.keys():
  print('key: ' + key)

# key: India
# key: United Kingdom
# key: France
```

**Note:** If you want to maintain the order of the keys in the list, you can do so using the sorted() function on the return of `.keys()`

_Comparison with JavaScript:_
- We can use a similar object method called `Object.keys(objectVariable)` to get an array of the keys.

#### Nesting dictionaries

You can assign a dictionary to another dictionary as a value to a prop.

```python
nested_object = {
  'a': 10,
  'b': {
    'c': 'I am a nested value'
  }
}
```

_Comparison with JavaScript:_
- Same.

#### List of dictionaries

Python lists can contain dictionaries as items

```python
foo = { 'some': 'object' }
bar = { 'another': 'object', 'a': 1 }
my_list = [foo, bar]

my_list # [{'some': 'object'}, {'another': 'object', 'a': 1}]
```

_Comparison with JavaScript:_
- Same with arrays.

#### Dictionary containing lists

Python dictionaries can also contain lists as values to props
```python
foo = { 
  'bar': ['list', 1, 'of', 2, 'objects']
}

foo # {'bar': ['list', 1, 'of', 2, 'objects']}
```

_Comparison with JavaScript:_
- Same with arrays.

### Sets

A set is a list that contains no duplicate values (& they are indexed for constant time operations)

- To create a set of values, use the `set()` function.
- Like dictionaries, set values are **unordered**

#### Defining a set

Use `set()` by passign it a list.
- It creates a set data structure
- The values contained are all unique (**duplicates are removed!**)

```python
set_of_countries = set(['India', 'Brazil', 'Australia', 'India'])

set_of_countries # {'Australia', 'Brazil', 'India'}
```

#### Fetching a set value

**Note:** You cannot access items in a set by referring to an index or a key.

```python
set_of_countries = set(['India', 'Brazil', 'Australia', 'India'])

set_of_countries[1] # ✕ (Error)

# ---------------------------------------------------------------------------
# TypeError                                 Traceback (most recent call last)
# <ipython-input-40-cfca302c0359> in <module>
# ----> 1 set_of_countries[1]

# TypeError: 'set' object is not subscriptable
```

_Comparison with JavaScript:_
- Same.

#### Checking if a set contains a value

You can check if a set has a value using the `in` operator. (Similar to lists)

```python
set_of_countries = set(['India', 'Brazil', 'Australia', 'India'])

'India' in set_of_countries # True

'Bahrain' in set_of_countries # False

# Use such conditionals in if statements and while loops
```

_Comparison with JavaScript:_
- Use the `.has(value)` method

#### Adding a value to a set

Use the `.add()` method

```python
set_of_countries = set(['India', 'Brazil', 'Australia', 'India'])

set_of_countries.add('China') 
set_of_countries # {'Australia', 'Brazil', 'China', 'India'}

# Duplicate insertions still result in only storing values that are unique

set_of_countries.add('China') 
set_of_countries # {'Australia', 'Brazil', 'China', 'India'}
```

_Comparison with JavaScript:_
- Same (`.add(value)` method)

#### Removing a value from a set

- Use the `.remove()` method

```python
set_of_countries = set(['India', 'Brazil', 'Australia'])

set_of_countries.remove('Brazil')
set_of_countries # {'Australia', 'India'}
```

_Comparison with JavaScript:_
- Use the `.delete(value)` method

#### Size of a set

- Use the `len()` function (similar to lists)

```python
set_of_countries = set(['India', 'Brazil', 'Australia'])

len(set_of_countries) # 3
```

_Comparison with JavaScript:_
- Use the `.size()` method

#### Looping through a set

Use a `for` (for-in) loop similar to lists

```python
set_of_countries = set(['India', 'Brazil', 'Australia'])

for value in set_of_countries:
  print(value)

# Brazil
# Australia
# India
```

_Comparison with JavaScript:_
- Similar. `for`, `.forEach`, `.keys()`, `.values()`, ... etc work!

### Functions

Functions are units of logic that perform an operation.
- They can be invoked
- Some can accept arguments that are defined as parameters
- They can be re-used by re-invocation
- Extremely helpful

#### Defining a function

- Use the `def` keyword
- Give a descriptive name in `snake_case` (convention)
- Add parenthese `()` and optional arguments
- Do not forget the colon `:` at the end of function signature
- List the function body (code) in a single tabbed space

```python
def print_hello():
  print('Hello!')

print_hello()

# Hello!
```

To invoke a function, type the function name along with parenthese (to invoke).
Pass in any arguments to match the parameters

_Comparison with JavaScript:_
- Same but we use the `function` keyword and `{}` for the body (No tabbing)
- Also, our convention for function names are `camelCase`

#### Docstring for a function in python

- Triple quote comment at the beginning of the function body is called a **docstring**
- It must describe what the function does
- Python automatically picks up the docstring when generating documentation for a piece of code
- Hence, it is not a regular comment that is ignored
- It can be _multiline_ too!

```python
def print_hello():
  """This function prints hello"""
  print('Hello!')

print_hello()

# Hello!
```

_Comparison with JavaScript:_
- Nothing like this exists in-built in JavaScript!
- Sometimes we use `@jsdoc` to provide docs for a function but it is a library and the params/description are documented above the function definition

#### Parameters for a function

Define parameters in via the `()` in the function signature
- Use comma `,` to separate out multiple parameters
- The order of the parameters matter

These are the default **position based parameters** and arguments to a function

```python
def add(num1, num2):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))

add(5, 6) # 5 + 6 = 11
```

_Comparison with JavaScript:_
- Same.

#### Keyword arguments in Python

- We can pass keyword arguments to a function (instead of the positional parameters)
- The parameter name is used as the key in the function call to pass the argument
- Since these are keyword arguments, the **order does not matter**

```python
def add(num1, num2):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))

add(num1=5, num2=6) # 5 + 6 = 11
```

- You can also mix positional arguments with keyword ones! (However, this may not be best practice)
- If you do so, **keyword arguments must come after positional arguments**!

```python
def add(num1, num2):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))

add(5, num2=6) # 5 + 6 = 11

add(num2=6, 5) # ✕ (SyntaxError: positional argument follows keyword argument)

# Make sure all the mandatory parameters match:
add(5, num1=5) # ✕ (TypeError: add() got multiple values for argument 'num1')

# The number of arguments (positional + keyword) must match the count of parameters:
add(5, 6, num1=2) # ✕ (TypeError: add() got multiple values for argument 'num1')
```

_Comparison with JavaScript:_
- No support for keyword arguments / named parameters in JavaScript
- If you want to pass by key then define an object `{}` as a parameter

#### Unmatched arguments in Python cause an error

```python
def add(num1, num2):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))
  
add(1) # ✕ (TypeError: add() missing 1 required positional argument: 'num2')
```

_Comparison with JavaScript:_
- The unmatched parameters receive the value, `undefined`. 
- Depending on how this value is used inside the function, it may or may not cause a runtime error.

#### Declaring default arguments

- Sometimes, we want to make parameters/arguments **OPTIONAL**
- To do so, define a parameter and provide a default argument with `=`
- If the argument for the parameter is not passed during invocation, the default value is used (making it optional)
- Else, if the argument is passed, it overrides the default value for the parameter
- **Note:** Define the parameters with default arguments AFTER all the positional parameters (in order to interpret arguments positionally)

```python
def add(num1, num2 = 5):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))

add(1) # 1 + 5 = 6 (Used the default)
add(1, 10) # 1 + 10 = 11 (Used the argument passed)


def add(num1=5, num2): # ✕ (SyntaxError: non-default argument follows default argument)
```

_Comparison with JavaScript:_
- Same but default argument parameters need not come after positional ones! (All are considered positional parameters)

#### Return value of a function

- Use the `return` keyword
```python
def add(num1, num2):
  return num1 + num2

add_result = add(1, 4)
add_result # 5
```

- Empty return / nothing returned case: The returned type will be `None`

```python
def add(num1, num2):
  print(str(num1) + ' + ' + str(num2) + ' = ' + str(num1 + num2))

add_result = add(1, 4)
print(add_result) # None
print(type(add_result)) # <class 'int'>
```

_Comparison with JavaScript:_
- Same keyword but when you return nothing, the returned value is `undefined`

#### Passing an arbitrary number of arguments

To pass an arbitrary number of arguments (Suppose we do not know how many the function will need), use the `*` prefixed parameter
- Python will take this parameter and create a tuple for it from the set of arguments it receives from a function call
- It is useful when you do not know the number of arguments before hand

```python
def add(*numbers):
  sum = 0
  for number in numbers:
    sum += number
  return sum

print(add(1, 2, 3, 4)) # 10
```

_Comparison with JavaScript:_
- Use the `spread` and `rest` (`...value`) to spread the many arguments during invocation and to group the arguments into a parameter representing an array, respectively.

#### Passing an arbitrary number of keyword arguments

In Python, apart from passing an arbitrary number of arguments, we can pass an arbitrary number of keyword arguments as well!
- Use the `**` prefix for the parameter
- All the keyword arguments are packed into a **dictionary** created for this parameter
- You can loop through the keys of a dictionary to obtain the values

- **Python rule**: The argument representing arbitrary args must come after positional and default args

```python
def remove_age_from_record(**record_details):
  filtered_record = {}
  for attribute, value in record_details.items():
    if attribute != 'age':
      filtered_record[attribute] = value
  return filtered_record

print(remove_age_from_record(name='Pushkar', age=29, location='London')) # {'name': 'Pushkar', 'location': 'London'}
```

_Comparison with JavaScript:_
- Nothing like this exits in JavaScript. Add an object `{}` parameter to collect key-value pairs. 

#### Passing a value by reference and by value

A list or a dictionary passed by name to a function or a method is passed by reference (default!)
- Modifying the list or dictionary within a function modifies it outside too 
- (i.e in-place since it is a reference to the same list or dictionary)

```python
my_list = [10, 200, 40, 61, 1]
def mutate_list(list):
  list[2] = 10000

print(my_list) # [10, 200, 40, 61, 1]
mutate_list(my_list)
print(my_list) # [10, 200, 10000, 61, 1]
```

```python
my_dict = { 'a': 100, 'b': 200 }

def mutate_dict(dict):
  dict['a'] = 0

print(my_dict) # {'a': 100, 'b': 200}
mutate_dict(my_dict)
print(my_dict) # {'a': 0, 'b': 200}
```

_Comparison with JavaScript:_
- Same!

- Passing an object or a list by value (immutability):

In order to **maintain immutability**, create a **clone** of the list or object and pass it to the function!

```python
my_list = [10, 200, 40, 61, 1]
def mutate_list(list):
  list[2] = 10000

print(my_list) # [10, 200, 40, 61, 1]
mutate_list(my_list[:])
print(my_list) # [10, 200, 40, 61, 1] (Has not changed)
```

Need to manually clone an object! (No workaround - at least not in basic python)

_Comparison with JavaScript:_
- To clone an array in JS, use the `[...originalArray]` syntax (i.e the spread operator as an aid)
- For objects, you have to write your own function to manually deep clone it (Using `JSON.stringify` and `JSON.parse`, maybe)
- Methods for shallow cloning exist: `{ ...originalObject }` or `Object.assign()`


### Modules

- Modules help store functionality, functions, and classes that can be imported by another python program
- Save modules in `.py` files 
- **Place the modules you want to import in the same directory as the executor python program/script.** (unless, it's standard library)
- Use the `import` syntax to import a module
- By convention, all `import` statements are placed at the top of the file
- Module (or just general python file naming) convention suggests using the `snake_case` 

Example module:

```python
# add_module.py
def add_nums(*nums):
  sum = 0
  for num in nums:
    sum += num
  return sum

def add_two_nums(num1, num2):
  return num1 + num2
```

#### Importing an entire module

- Use the dot (`.`) notation to access functions from the import

```python
import add_module

print(add_module.add_nums(1, 3, 5, 7)) # 16
print(add_module.add_two_nums(1, 3)) # 4
```

_Comparison with JavaScript:_
- We also use the `import` statement: Ex: `import * as Module from './some/module`
- Modules in JavaScript have the concept of a **default** import. Ex: `import defaultImport from './some/module'`
- Just `import './some/module'` will execute the module i.e including side-effects but provides no function or class to work with

#### Importing a specific function

```python
from add_module import add_nums

print(add_nums(1, 3, 5, 7)) # 16
```

Use commas `,` to import multiple specific functions:
- Syntax: `from module_name import function_1, function_2, function_3`

_Comparison with JavaScript:_
- Syntax would be `import { someFunction } from './some/module'`
- Multiple functions' import ``import { func_1, func_2, func_3 } from './some/module'`

#### Defining an alias while importing a function

Use the `as` keyword for the function

```python
from add_module import add_nums as add_numbers

print(add_numbers(1, 3, 5, 7)) # 16
```

_Comparison with JavaScript:_
- Same. Syntax would be `import { someFunction as someOtherName } from './some/module'`

#### Defining an alias while importing the whole module

Use the `as` keyword for the module

```python
import add_module as custom_add_module

print(custom_add_module.add_nums(1, 3, 5, 7)) # 16
```

_Comparison with JavaScript:_
- Same (we have to do this by default). Ex: `import * as Module from './some/module`
- For a default export: Ex: `import defaultExport as someName from './some/module`

#### Importing all functions from a module

Use the `*` operator
- Do not use it unless you have a valid reason!
- Pollutes the namespace: Can lead to name collisions between the imported module and the current script!

```python
from add_module import *

print(add_nums(1, 3, 5, 7)) # 16 (note: no dot notation (.) needed!)
print(add_two_nums(1, 3)) # 4 (note: no dot notation (.) needed!)
```

_Comparison with JavaScript:_
- Name collision is not possible as we always need to provide an `as` to import the whole module
- I.e the functions are not imported unless each is specified or is imported as a property of the module import.

### Classes

- Classes are used to model real-world objects
- Classes are blueprints for an object

#### Defining a class

1. Syntax:

```python
class ClassName():
  """Docstring for a class"""

  def __init__(self):
    # ...

  def method_1():
    # ...

  def method_1():
    # ...
```

a. Classes have the `class` keyword. We need parentheses after the name: It is necessary and accept another class to inherit from
b. Class names are usually written in `PascalCase` (Note that object names, functions, & variables are `snake_case`)
c. The _constructor_ executed when the class is instantiated, i.e object created, is named as `__init__`
d. The object created by the class can be referred to by `self` within the class. All the methods receive `self` as the first argument!
e. Do not forget the colon `:` and the tabbing for the class methods.
f. **Optional**: Adding a docstring at the beginning of the class to document it

Example:
```python
class Restaurant():
  """Restaurant class"""

  def __init__(self, restaurant_name, cuisine_type):
    self.restaurant_name = restaurant_name
    self.cuisine_type = cuisine_type
    self.number_served = 0
  
  def describe_restaurant(self):
    print('Restaurant, ' + self.restaurant_name + ', serving ' + self.cuisine_type + ' cuisine')

  def open_restaurant(self):
    print(self.restaurant_name + ' is now open')

  def set_number_served(self, count):
    self.number_served += count
```

**Note:** Making python2.7 classes behave like python3 classes by passing `object`
- Python2.7 syntax: `class ClassName(object):`

_Comparison with JavaScript:_
- In JavaScript, classes are nothing but syntactic sugar over **[prototypal inheritance](https://levelup.gitconnected.com/prototypal-inheritance-the-big-secret-behind-classes-in-javascript-e7368e76e92a)**
- Class syntax is: `class ClassName { constructor() { /*...*/ }}`. Instead of `__init__`, we use `constructor`
- We use `this` instead of `self. However, it is implicitly available to every class method (Not required to pass as first argument)
- Functions inside clasess are known as **methods** and they do not need to prefixed with the `function` keyword (like `def` is needed for python methods)

#### Instantiating a class

Instantiating a class i.e object creation: 
- Invoke the class with arguments meant for the `__init__` constructor
- **Note**: You do not need to pass the `self` argument (will be auto-added). Ignore it and pass in the other arguments.

```python
my_restaurant = Restaurant('Best Taste', 'Indian')
print(my_restaurant) # <Restaurant object at 0x7f8bb21227c0>
```

_Comparison with JavaScript:_
- Similar but you need to instantiate the class using the `new` keyword

#### Accessing attributes and methods

Use the dot `.` notation

```python
my_restaurant = Restaurant('Best Taste', 'Indian')
print(my_restaurant.cuisine_type) # Indian
my_restaurant.open_restaurant() # Best Taste is now open
```

_Comparison with JavaScript:_
- Same.

#### Default attribute values

Add more attributes to the `self` object inside the `__init__` method (these do not depend on the `__init__` parameters)

```python
class Adder():
  def __init__(self, num_1=0, num_2=1): # Constructor, i.e init, parameters can accept default arguments!
    self.num_1 = num_1
    self.num_2 = num_2
    self.sum = 0 # A DEFAULT ATTRIBUTE!

  def add(self):
    self.sum = self.num_1 + self.num_2

  def view_result(self):
    return self.sum

add_five_and_six = Adder(5, 6)
add_five_and_six.add()
print(add_five_and_six.view_result()) # 11
```

_Comparison with JavaScript:_
- Same (but inside a constructor, using `this`)

#### Modifying an attribute value

1. Direct modification

```python
my_restaurant = Restaurant('Best Taste', 'Indian')

my_restaurant.number_served = 5
print(my_restaurant.number_served) # 5
```

2. Modification via a method

```python
my_restaurant = Restaurant('Best Taste', 'Indian')

my_restaurant.set_number_served(5)
print(my_restaurant.number_served) # 5
```

_Comparison with JavaScript:_
- Same (unless _access modifiers_ prevent one from updating an attribute directly)

#### Inheritance

1. Creating a child class from the parent: 

- Pass in the parent class in the class signature as an argument `()`!
- Call `super().__init__` with the arguments required for parent class' `__init__` method i.e we must invoke the parent class constructor first!

```python
class JapaneseRestaurant(Restaurant):
  """A Japanese restaurant class"""

  def __init__(self, restaurant_name):
    super().__init__(restaurant_name, 'Japanese')
    self.cuisine_type = 'special japanese'
```

**Note**: Inheritance in Python2.7 
- We need to pass a reference to the child class & `self `in `super()`
- Ex: `super(JapaneseRestaurant, self).__init__()`

2. Adding attributes/methods to or overriding parent class attributes/methods in a child class

- We can add new attributes and methods (OR) override the parent class ones too! 

```python
class JapaneseRestaurant(Restaurant):
  """A Japanese restaurant class"""

  def __init__(self, restaurant_name):
    super().__init__(restaurant_name, 'Japanese')
    self.cuisine_type = 'special japanese' # overriding the parent class attribute
    self.japanese_welcome_message = 'いらっしゃいませ' # new child class attribute

  # Overriding a method of the parent class
  def describe_restaurant(self):
    print(self.restaurant_name + ' is a special Japanese restaurant!')

  # Adding a new method to the child class:
  def welcome_in_japanese(self):
    print(self.japanese_welcome_message)

my_japanese_restaurant = JapaneseRestaurant('Arigato')
my_japanese_restaurant.describe_restaurant() # Arigato is a special Japanese restaurant!
my_japanese_restaurant.welcome_in_japanese() # いらっしゃいませ
```

_Comparison with JavaScript:_
- Similar. We only need to invoke `super()` inside the child constructor but the arguments are passed to `super` itself (not to `__init__()`)
- We can also override attributes and methods of a parent class inside a child class by default
- We can also add new attributes and methods to a child class
- **Note:** access modifiers (Ex: `private`, `protected`) might affect default behaviour

#### Importing classes

1. Importing a single class

```python
from restaurant import Restaurant
```

2. Importing multiple classes from a module

Better to store _related classes_ in the same module if you have to.

```python
from restaurant import Restaurant, JapaneseRestaurant
```

3. Importing an entire module

Use the dot `.` notation to access specific classes of the module

```python
import restaurant_classes # Assume this holds Restaurant and JapaneseRestaurant

my_restaurant = restaurant_classes.Restaurant()
my_japanese_restaurant = restaurant_classes.JapaneseRestaurant()
```

4. Importing all classes from a module

Against best practices as this can pollute the current module's namespace (leads to collisions possibly) if names overlap

```python
from restaurant_classes import *

my_restaurant = Restaurant()
my_japanese_restaurant = JapaneseRestaurant()
```

_Comparison with JavaScript:_
- Either as a named export or default export: `import ClassName from '...'` or `import { ClassName } from '...'`

### Files

Reading, writing and appending to files in python is straight-forward

File used with examples below: `cities.txt` in the same directory as the python script.
```
Bangalore
London
New Delhi
Beijing
New York
```

#### Opening a file

Use `open(file_path)`: It returns an **object representing the file**!
(File paths can be either relative to the executing python directory or an absolute path)

#### Closing a file

Use `close(file_path)`

#### Correctly opening and closing a file

Opening and closing file manually everytime in the correct way is prone to error!
Example: If there is an error before closing or if file is not closed properly then the program might crash or file get corrupted.

- Use the `with` expression along with (a) `open()` and (b)`as` expression to properly open, work with, and close a file!
- The with statement body must be tabbed!

Syntax:
```python
with open(file_path) as open_object_name:
  # do
  # whatever you want
  # with the file & its contents
```

**Note:** When the `with` clause ends, the file is also closed! Python takes care of safely closing the file when the clause ends.

Example:
```python
with open('cities.txt') as cities_file_object:
  contents = cities_file_object.read()
  print(contents)
```

#### Reading the entire contents of a file

Use `.read()` method on the file object.

```python
with open('cities.txt') as cities_file_object:
  contents = cities_file_object.read()
  print(contents)

# Bangalore
# London
# New Delhi
# Beijing
# New York
```

**Note:** File contents are read as **strings**!

#### Reading the file contents one line at a time

- The file object, when used as an iterable in a `for` loop (`for-in`), returns contents by line (& moves the pointer to the next time each time)
- **Note:** Each line will also contain the invisible newline `\n` at the end (If you print it, the print statement too inserts a newline)
- In order to get rid of the newline `\n`, use `.rstrip()` (or `.strip()`)

```python
with open('cities.txt') as cities_file_object:
  for city in cities_file_object:
    print('city: ' + city)

# city: Bangalore

# city: London

# city: New Delhi

# city: Beijing

# city: New York
```

By stripping whitespaces:

```python
with open('cities.txt') as cities_file_object:
  for city in cities_file_object:
    print('city: ' + city.rstrip())

# city: Bangalore
# city: London
# city: New Delhi
# city: Beijing
# city: New York
```

#### Storing lines of a file into a list

- Use `.readlines()` method on the file object to generate a list containing each line string as an item (including the newline `\n`)
- Tip: Remove the `\n` character from the end of each line in the file using `.rstrip()` or `.strip()` later

```python
with open('cities.txt') as cities_file_object:
  cities = cities_file_object.readlines()

print(cities) # ['Bangalore\n', 'London\n', 'New Delhi\n', 'Beijing\n', 'New York']
```

```python
with open('cities.txt') as cities_file_object:
  cities = cities_file_object.readlines()

cities = [city.rstrip() for city in cities]

print(cities) # ['Bangalore', 'London', 'New Delhi', 'Beijing', 'New York']
```

#### Writing to a file

Different modes in which to `open()` a file in:
1. Read (`r`) - The default and need not be specified
2. Write (`w`) - Write mode: Creates a file if it does not exist. If it exists, clears the existing contents
3. Append (`a`) - Append mode: Creates a file if it does not exist. If it exists, preserves the existing contents and appends to it

Pass the mode as the _second argument_ to the `open()` function.

- Use the `.write()` method on the file object

```python
with open('cities.txt', 'w') as cities_file_object:
  cities_file_object.write('Paris') # String does not include a newline
  cities_file_object.write('Berlin') # String does not include a newline

# FILE CONTENTS:
# ParisBerlin
```

#### Appending to file

```python
with open('cities.txt', 'a') as cities_file_object:
  cities_file_object.write('Paris') # String does not include a newline

# FILE CONTENTS:
# Bangalore
# London
# New Delhi
# Beijing
# New York
# Paris
```

#### Loading and dumping JSON data

There exists an easier way to work with a specific type of file, a json file.

1. `import json`. This is the module required to load and dump json (Standard library)
2. `json.dump(data, file_object)`: Takes data (list / object) and a JSON file object
3. `json.load(file_object)`: Loads the data from a JSON file object

Example JSON:
```json
{
  "cities": ["Bangalore", "London", "New Delhi", "Beijing", "New York"],
  "person": "Pushkar",
  "age": 29,
  "location": "London"
}
```

Loading JSON data:
```python
import json

with open('data.json') as json_file_object:
  json_data = json.load(json_file_object)

print(json_data)
# {'cities': ['Bangalore', 'London', 'New Delhi', 'Beijing', 'New York'], 'person': 'Pushkar', 'age': 29, 'location': 'London'}
```

Dumping JSON data:
```python
import json

json_data = {
  'cities': ['Bangalore', 'London'],
  'person': 'James',
  'age': 20
}

with open('data.json', 'w') as json_file_object:
  json.dump(json_data, json_file_object)

# FILE CONTENTS:
# {"cities": ["Bangalore", "London"], "person": "James", "age": 20}
```

_Comparison with JavaScript:_
- NodeJS has a similar way of working with files ([Tutorial](https://www.w3schools.com/nodejs/nodejs_filesystem.asp))
- It uses a core module called `fs` which stands for file system

### Exceptions

1. The `try-except` block 

- `Exception` catches all types of errors (Least specific)
```python
try:
  print(5/0)
except Exception:
  print('Caught an error')

# Caught an error
```

- To access the error object, use the `as` expression:

```python
try:
  print(5/0)
except Exception as e:
  print(e)

# division by zero
```

- Generally, try to be more specific in trying to catch an error! (Good practice: Catch only errors you meant to catch)
```python
try:
  print(5/0)
except ZeroDivisionError:
  print('Cannot divide by zero')

# Cannot divide by zero
```

2. The `else` block

- Any code to be executed when the `try` block has no errors (successful), is added to `else`

```python
try:
  print(5/1)
except ZeroDivisionError:
  print('Cannot divide by zero')
else:
  print('Great! You did not divide by zero')

# 5.0
# Great! You did not divide by zero
```

_Comparison with JavaScript:_
- Similar. We use a `try { /* ... */ } catch (e) { /* ... */ }` block
- The `catch()` block catches all errors (unlike python where we need to specify the type)
- The `catch(e)` argument is the error object. It tells us the type of error
- The `else` block in python does not exist in JavaScript.
- However, a `finally { /* ... */ }` handles code to be run in all the cases i.e Error / No error!
```javascript
try {
  // tryCode - Code block to run
}
catch(e) {
  // catchCode - Code block to handle errors
}
finally {
  // finallyCode - Code block to be executed regardless of the try result
}
```

### Unit testing your code

Python provides a standard library called `unittest` in order to unit test our code.

#### Unit test

Verifies that one specific aspect of a function's behaviour is correct

#### Test case
A collection of unit tests which together prove that a function is supposed to behave as it is supposed to (within the full range of situations you expect it to handle)

#### Creating a test case

1. Import `unittest` (and import any python program files that need to be tested)
2. Create a class that inherits from `unittest.TestCase` (Not required to write the `__init__` method)
3. Unit tests must be class methods starting with the `test_` prefix. Write your code for each unit test inside such a method
4. Assertions must be written the `self.assert*` methods ([Python unittest assertions cheatsheet](https://kapeli.com/cheat_sheets/Python_unittest_Assertions.docset/Contents/Resources/Documents/index))
5. Write `unittest.main()` at the end of the file. It tells python to execute the unit tests in that file

Example module to test:
```python
# add_module.py

def add_nums(*nums):
  sum = 0
  for num in nums:
    sum += num
  return sum

def add_two_nums(num1, num2):
  return num1 + num2
```

The test file:
```python
import unittest
import add_module

class AddTestCase(unittest.TestCase):
  """Tests for add_module"""

  def test_adds_two_nums(self):
    """Tests if two numbers can be added"""
    sum = add_module.add_two_nums(4, 3)
    self.assertEqual(sum, 7)

unittest.main()
```

#### Understanding the test case output

Execute the test file like you would any other python script.

1. A passing test example

```
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

2. A failing test example (Needs fixing)
```
F
======================================================================
FAIL: test_adds_two_nums (__main__.AddTestCase)
Tests if two numbers can be added
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/Users/pushkar/Desktop/test.py", line 10, in test_adds_two_nums
    self.assertEqual(sum, 7)
AssertionError: 8 != 7

----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (failures=1)
```

3. Adding a new unit test

Add a new `test_` prefixed method

```python
class AddTestCase(unittest.TestCase):
  # ...

  def test_adds_many_numbers(self):
    """Tests if two numbers can be added"""
    sum = add_module.add_nums(4, 3, 2, 1)
    self.assertEqual(sum, 10)

  # ...
```

#### Common assertions

1. `assertEqual(a, b)` : `a == b`
2. `assertNotEqual(a, b)` : `a != b`
3. `assertTrue(x)` : `x == True`
4. `assertFalse(x)` : `x == False`
5. `assertIn(item, list)` : `item in list`
6. `assertNotIn(item, list)` : `item not in list`

#### Setup code

The `setUp` method (A bit like `beforeAll` in JavaScript)
- Useful for setting up code before all your unit tests execute. Ex: class set up
- The code set up in `setUp` will be available via `self` to all test methods depending on how it was set up (as attributes or not)

```python
import unittest
import add_module

class AddTestCase(unittest.TestCase):
  """Tests for add_module"""

  def setUp(self):
    """Sets up data for the tests"""
    self.num_1 = 4
    self.num_2 = 3
    self.num_3 = 2
    self.num_4 = 1

  def test_adds_two_nums(self):
    """Tests if two numbers can be added"""
    sum = add_module.add_two_nums(self.num_1, self.num_2)
    self.assertEqual(sum, 7)

  def test_adds_many_numbers(self):
    """Tests if two numbers can be added"""
    sum = add_module.add_nums(self.num_1, self.num_2, self.num_3, self.num_4)
    self.assertEqual(sum, 10)

unittest.main()
```

_Comparison with JavaScript:_
- No standard library such as `unittest` exists in JavaScript, either for the web or NodeJS.
- NodeJS does have a primitve, built-in `assert` module though

### Python standard library

The Python Standard Library is a collection of script modules accessible to a Python program.
It does so by simplifying the programming process and removing the need to rewrite commonly used commands. 
They can be used by 'calling/importing' them at the beginning of a script.

Common built-in modules (need to `import` them):

1. `datetime` ([docs](https://docs.python.org/3/library/datetime.html))
2. `math` ([docs](https://docs.python.org/3/library/math.html))
3. `random` ([docs](https://docs.python.org/3/library/random.html))
4. `os` ([docs](https://docs.python.org/3/library/os.html))

### Lambda functions

Lambda is an anonymous function
- Syntax: `lambda arg_1[, arg_2, ...] : expression`
- Can take any number of arguments (comma `,` separated)
- However, they have only one expression whose result becomes the return value of that lambda function
```python
square = lambda x : x ** 2
print(square)
print(square(5))
```

Benefits of Lambda functions:
- We can have anonymous functions _inside another function_ (Creating reusable units of code within that function's logic)
- They offer a _concise syntax_ for a function
- Lambdas can be used to construct *higher order functions* (HOCs)

Debugging a lambda function is more difficult than regular functions (missing name in traceback).

_Comparison with JavaScript:_
- Lambdas are very similar to arrow functions `() => {}`
