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
      - [String interpolation](#string-interpolation)
      - [Escaping characters in a string](#escaping-characters-in-a-string)
      - [Stripping whitespaces from strings](#stripping-whitespaces-from-strings)
      - [Casting a value into a string](#casting-a-value-into-a-string)
      - [Indexing and slicing strings](#indexing-and-slicing-strings)
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
      - [Concatenating lists](#concatenating-lists)
      - [Replicating lists](#replicating-lists)
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
      - [Accessing a value in a dictionary in a safe way using get](#accessing-a-value-in-a-dictionary-in-a-safe-way-using-get)
      - [Adding a new key-value pair to a dictionary](#adding-a-new-key-value-pair-to-a-dictionary)
      - [Modifying values in a dictionary](#modifying-values-in-a-dictionary)
      - [Removing key-value pairs from a dictionary](#removing-key-value-pairs-from-a-dictionary)
      - [Setting a default value for a key](#setting-a-default-value-for-a-key)
      - [Pretty print a dictionary](#pretty-print-a-dictionary)
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
      - [Functions are first class objects](#functions-are-first-class-objects)
      - [Nesting functions as inner functions](#nesting-functions-as-inner-functions)
      - [Fetching the name of a function](#fetching-the-name-of-a-function)
    + [Scopes and closures](#scopes-and-closures)
      - [Variable shadowing](#variable-shadowing)
      - [Modifying a global variable inside a function](#modifying-a-global-variable-inside-a-function)
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
      - [Class multiple inheritance](#class-multiple-inheritance)
      - [Class operator overloading](#class-operator-overloading)
      - [Importing classes](#importing-classes)
    + [The pass keyword](#the-pass-keyword)
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
      - [User defined exceptions](#user-defined-exceptions)
    + [Unit testing your code](#unit-testing-your-code)
      - [Unit test](#unit-test)
      - [Test case](#test-case)
      - [Creating a test case](#creating-a-test-case)
      - [Understanding the test case output](#understanding-the-test-case-output)
      - [Common assertions](#common-assertions)
      - [Setup code](#setup-code)
    + [Lambda functions](#lambda-functions)
    + [Python standard library](#python-standard-library)
    + [PIP package manager](#pip-package-manager)
      - [Verifying the system has pip installed](#verifying-the-system-has-pip-installed)
      - [Running pip as a module](#running-pip-as-a-module)
      - [Best setup by creating a virtual environment](#best-setup-by-creating-a-virtual-environment)
        * [Virtual environment variable](#virtual-environment-variable)
        * [pip config file](#pip-config-file)
      - [Installing pip packages](#installing-pip-packages)
      - [Listing the installed packages and their versions](#listing-the-installed-packages-and-their-versions)
      - [Get more information about an installed package](#get-more-information-about-an-installed-package)
      - [Importing an installed package](#importing-an-installed-package)
      - [Uninstalling a package via pip](#uninstalling-a-package-via-pip)
      - [Using a custom package index](#using-a-custom-package-index)
      - [Pinning requirements](#pinning-requirements)
      - [Alternatives to PIP](#alternatives-to-pip)
    + [Debugging python with pdb](#debugging-python-with-pdb)
      - [Adding a breakpoint](#adding-a-breakpoint)
      - [Running the program with the debugger](#running-the-program-with-the-debugger)
      - [Quit pdb](#quit-pdb)
      - [Print an expression](#print-an-expression)
      - [Stepping through code](#stepping-through-code)
      - [Listing the function source code](#listing-the-function-source-code)
      - [Setting and removing breakpoints](#setting-and-removing-breakpoints)
      - [Trace the caller function](#trace-the-caller-function)
      - [pdb cheatsheet](#pdb-cheatsheet)
      - [pdb vs ipdb](#pdb-vs-ipdb)

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

#### String interpolation 

String interpolation is a special way to concatenate strings i.e interpolate expression, including variables, into a string.

Strings can be interpolated in two ways:
1. Using the `%s` operator
2. Using the new **`f` strings** in Python3.6+

```python
name = 'Pushkar'
age = 29
message = 'My name is %s. I am %s years old.' % (name, age)
print(message) # My name is Pushkar. I am 29 years old.
```

```python
# Valid from python 3.6 only!
# Do not forget to prefix the string with `f`
name = 'Pushkar'
age = 29
message = f'My name is {name}. I am {age} years old.'
print(message) # My name is Pushkar. I am 29 years old.
```

_Comparison with JavaScript:_
- Use \` character to open a string where interpolation is possible. Use `${}` within such a string to input an expression
- Ex: `Hello, ${name}! You are ${age} years old.` where `name` and `age` are single value expressions i.e variables

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

#### Indexing and slicing strings

This is done pretty much the same way as with lists (arrays)

**Note:** Strings are immutable (unlike lists) therefore accessing strings work like lists but not modifications (which are not allowed)

```python
foo = 'Hello Boy!'

print(foo[1]) # 'e'

print(foo[2:5]) # 'llo'

print(foo[2:]) # 'llo Boy!'

print(foo[:3]) # 'Hel'

print(foo[-1]) # '!'

print(foo[-3:]) # 'oy!'

print(foo[:-3]) # 'Hello B'
```

_Comparsion with JavaScript:_
- String characters can be accessed like arrays (same as python)
- However, for getting substrings use `substr()` or `substr()` 
- Negative indices do not fetch a character from the end of the string
- Strings are immutable in JS too!

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

#### Accessing a value in a dictionary in a safe way using get

In case the key-value pair does not exist, we get around an error in accessing a dictionary value by using `.get()`
- Two arguments: The key and an optional fallback value to return if the key-value pair is not present

```python
foo = {
  'a': 10,
  'b': 20,
  'names': ['Jon', 'Ron', 'Emma']
}

# When value exists:
print(foo['a']) # 10
print(foo.get('a', 0)) # 10

# When value does not exist:
# print(foo['nonexistent']) # ✕ (KeyError: 'nonexistent')
print(foo.get('nonexistent', 100)) # 100
```

_Comparison with JavaScript:_
- No error in accessing a non-existent key-value pair in an object. You receive the value `undefined`
- Perform truthy checks on the value before processing it

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

#### Setting a default value for a key

Helpful shorthand for checking if a key-value pair exists
- Use `.setdefault()`
- First parameter is the key and the second is a default value to set if the key does not exist
- If key does not exist, the value is set for it and returned
- If key exists, the existing value is returned (ignoring the second argument)

```python
spam = {'name': 'Pooka', 'age': 5}

return_val = spam.setdefault('color', 'black')

print(return_val) # black
print(spam) # {'name': 'Pooka', 'age': 5, 'color': 'black'}

return_val = spam.setdefault('color', 'white')

print(return_val) # black
print(spam) # {'name': 'Pooka', 'age': 5, 'color': 'black'}
```

_Comparison with JavaScript:_
- Nothing like this exists in-built to set a default or shorthand
- Use `Object.values(obj)` and `.includes()` on the returned list to check for existence of a key-value pair

#### Pretty print a dictionary

Use the `pprint` module (import it!)

```python
import pprint

spam = {'name': 'Pooka', 'age': 5, 'color': 'black', 'sky': 'blue', 'last_name': 'Bro', 'a': 10000, 'f': 1.344 }

print(spam)
# {'name': 'Pooka', 'age': 5, 'color': 'black', 'sky': 'blue', 'last_name': 'Bro', 'a': 10000, 'f': 1.344

pprint.pprint(spam)
# {'a': 10000,
#  'age': 5,
#  'color': 'black',
#  'f': 1.344,
#  'last_name': 'Bro',
#  'name': 'Pooka',
#  'sky': 'blue'}
```

_Comparison with JavaScript:_
- There is no in-built prettifier but the browser console makes it collapsible and tabbed


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

#### Functions are first class objects

In Python, functions are first-class objects. This means that functions can be _passed around_ and used as arguments, just like any other object (string, int, float, list, and so on).

```python
def add(a, b):
  return a + b

def print_result_of_adder(callback, x, y):
  print(callback(x, y))

print_result_of_adder(add, 3, 5) 

# 8
```

_Comparison with JavaScript:_
- Same.

#### Nesting functions as inner functions

A function can contain an inner function, one or many.

```python
def print_result_of_adder(x, y):
  def add(a, b):
    return a + b

  print(add(x, y))

print_result_of_adder(3, 5) # 8
```

_Comparison with JavaScript:_
- Same.

#### Fetching the name of a function

Use the `.__name__` property

```python
def greet(name):
    return f'Hello, {name}'
    
print(greet.__name__) # greet
```

Note: A decorator for a function can end up overriding this. To preserve the function details when wrapped by a decorator, use the [`functools`](https://realpython.com/primer-on-python-decorators/#who-are-you-really) module 

_Comparison with JavaScript:_
- Similar. The `name` data property of a Function instance indicates the function's name as specified when it was created, or it may be either `anonymous` or `''` (an empty string) for functions created anonymously.

### Scopes and closures

- Parameters and variables assigned inside a function are in the **Local scope**
- Variables assigned outside all functions are in the **Global scope**

**Local scope**
- Created when a function is created
- Destroyed when a function returns (i.e Parameters and variables are forgotten)

**Global scope**
- Created when the program begins
- Destroyed when the program terminates

**(A) Global variables can be used in a function's local scope but not vice-versa! Known as CLOSURE**
**(B) One function cannot access the local scope of another function!**

**Note:**
- It is fine to use global variables
- However, it is **bad practice** to rely on a lot of gloabl variables, especially when your programs get larger

```python
# Local variables

def foo():
  bar = 1
  baz = 2
  
  # Can be used locally
  print(f'I can access bar and baz in the local scope: {bar}, {baz}')

bar # ✕ (NameError: name 'bar' is not defined)
```

```python
# Local variables in one function cannot be used in another function:

def foo_1():
  bar = 1
  print(f'I can only access bar inside foo_1: {bar}')

def foo_2():
  baz = 2
  print(f'I can only access bar inside foo_2: {bar}')
  
  bar # ✕ (NameError: name 'bar' is not defined - when the function executes)

foo_1()
foo_2()
```

```python
# Global variables can be accessed inside a function's local scope

bar = 5

def foo():
  baz = 1
  print(f'I can access bar inside foo: {baz}')
  print(f'I can also access bar as well: {bar}')

# I can access bar inside foo: 1
# I can also access bar as well: 5
```

#### Variable shadowing

- Local variables will shadow the global variable with the same name inside the function!
- Avoid using the same names for both global and variables (namespace them if needed) as it gets confusing!

```python
# Variable shadowing

bar = 1

def foo():
  bar = 2
  print(bar)
  goo()

def goo():
  bar = 3
  print(bar)

print(bar)
foo()

# 1
# 2
# 3
```

#### Modifying a global variable inside a function 

- We can read a global variable inside a function.
- However, assigning a variable inside a function will create a local one always!!
- Therefore, how do we modify global variables inside a function (other than passing by reference, if possible)?

```python
bar = 1

def foo():
  bar = 2 # This line creates a local variable always!
  print(bar)

print(bar)
foo()
print(bar)

# 1
# 2
# 1
```

- Modify global variables inside a function by marking them as **`global <variablename>`**
- Better to place this at the top of the function before modifying it
- It tells Python that it the variable used inside it is the one available globally

```python
bar = 1

def foo():
  global bar
  bar = 2 # This line creates a local variable always!
  print(bar)

print(bar)
foo()
print(bar)

# 1
# 2
# 2
```

_Comparison with JavaScript:_
- These scopes and closure principles apply to JavaScript too!
- First difference: Functions can contain other functions within them so closure works not just between the global scope and a function but also within nested functons
- Second difference: We can edit a global variable inside a function. That is because, in JavaScript, the variable declaration and assignment can happen separately. If a variable is assigned inside a local scope without declaring it, JavaScript will look for it in the outer scope (which maybe an enclosing function or the global scope)

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

#### Class multiple inheritance

A single class can inherit from multiple parent classes. Use the comma `,` to list all the parent classes within `()`

```python
class ParentClass1:
    # features of ParentClass1

class ParentClass2:
    # features of ParentClass2

class MultiDerived(ParentClass1, ParentClass2):
    # features of ParentClass1 + ParentClass2 + MultiDerived class
```

**Method Resolution Order (MRO)** in Python
If two parent classes have the _same method name_ and the derived class calls that method, Python uses the *MRO* to search for the right method to call. 
```python
class SuperClass1:
    def info(self):
        print("Super Class 1 method called")

class SuperClass2:
    def info(self):
        print("Super Class 2 method called")

class Derived(SuperClass1, SuperClass2):
    pass

d1 = Derived()
d1.info()  

# Output: "Super Class 1 method called"
```
The MRO specifies that _methods should be inherited from the leftmost superclass first_, so `info()` of `SuperClass1` is called rather than that of `SuperClass2`.

#### Class operator overloading

Class functions that begin with double underscore `__` are called **special functions** in Python.

| Function | Description |
|----------|-------------|
| `__init__()` |	initialize the attributes of the object |
| `__str__()` |	returns a string representation of the object |
| `__len__()` |	returns the length of the object |
| `__add__()` |	adds two objects |
| `__call__()` |	call objects of the class like a normal function |

To overload the `+` operator, we will need to implement `__add__()` function in the class.

Example:
```python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def __str__(self):
        return "({0},{1})".format(self.x, self.y)

    def __add__(self, other):
        x = self.x + other.x
        y = self.y + other.y
        return Point(x, y)


p1 = Point(1, 2)
p2 = Point(2, 3)

print(p1 + p2)

# Output: (3,5)
```

| Operator | Expression | Internally |
|----------|------------|------------|
| Addition |	p1 + p2 | p1.__add__(p2) |
| Subtraction |	p1 - p2	| p1.__sub__(p2) |
| Multiplication | p1 * p2 | p1.__mul__(p2) |
| Power |	p1 ** p2	| p1.__pow__(p2) |
| Division |	p1 / p2 |	p1.__truediv__(p2) |
| Floor | Division	p1 // p2	| p1.__floordiv__(p2) |
| Remainder | (modulo)	p1 % p2	| p1.__mod__(p2) |
| Bitwise | Left Shift	p1 << p2	| p1.__lshift__(p2) |
| Bitwise | Right Shift	p1 >> p2	| p1.__rshift__(p2) |
| Bitwise | AND	p1 & p2	| p1.__and__(p2) |
| Bitwise | OR	p1, p2	| p1.__or__(p2) |
| Bitwise | XOR	p1 ^ p2	| p1.__xor__(p2) |
| Bitwise | NOT	~p1	| p1.__invert__() |
| Less than	| p1 < p2	| p1.__lt__(p2) |
| Less than or equal to |	p1 <= p2	| p1.__le__(p2) |
| Equal to	| p1 == p2	| p1.__eq__(p2) |
| Not equal to |	p1 != p2	| p1.__ne__(p2) |
| Greater than |	p1 > p2	| p1.__gt__(p2) |
| Greater than or equal to |	p1 >= p2 | p1.__ge__(p2) |

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

### The pass keyword

The `pass` statement is used as a placeholder for future code.
- Empty code is not allowed in if statements, in loops, function definitions, or in class definitions
- When the `pass` statement is executed, nothing happens, but you avoid getting an error when empty code is not allowed

```python
def myfunction():
  pass
```

```python
class Person:
  pass
```

Using the pass keyword in an `if` statement:
```python
a = 33
b = 200

if b > a:
  pass
```

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

#### User defined exceptions

For a normal exception, we can `try-except` to catch errors in the try block of code.

How can we create a custom exception?

In Python, we can define custom exceptions by creating a new class that is _derived_ from the built-in `Exception` class.

```python
class CustomError(Exception):
    ...
    pass

try:
   ...

except CustomError:
    ...
```

To manually raise an error, use the **`raise`** keyword!

Example:
```python
# define Python user-defined exceptions
class InvalidAgeException(Exception):
    "Raised when the input value is less than 18"
    pass

# you need to guess this number
number = 18

try:
    input_num = int(input("Enter a number: "))
    if input_num < number:
        raise InvalidAgeException
    else:
        print("Eligible to Vote")
        
except InvalidAgeException:
    print("Exception occurred: Invalid Age")
```

_Comparison with JavaScript:_
- We can create a custom error object too!

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

### Python standard library

The Python Standard Library is a collection of script modules accessible to a Python program.
It does so by simplifying the programming process and removing the need to rewrite commonly used commands. 
They can be used by 'calling/importing' them at the beginning of a script.

Common built-in modules (need to `import` them):

1. `datetime` ([docs](https://docs.python.org/3/library/datetime.html))
2. `math` ([docs](https://docs.python.org/3/library/math.html))
3. `random` ([docs](https://docs.python.org/3/library/random.html))
4. `os` ([docs](https://docs.python.org/3/library/os.html))

### PIP package manager

The standard package manager for Python is `pip`. Essentially, a _dependency manager_.
- It allows you to _install and manage_ packages that _are not part of_ the Python standard library.
- The Python community is very active and you will find a lot of packages created by people
- There exist alternatives to PIP as well!

**Note:** Python’s installers have included pip since versions 3.4 and 2.7.9, for Python 3 and Python 2, respectively.
(If you do not have PIP, you need to manually install it. Ex: `sudo apt install python3-pip`)

#### Verifying the system has pip installed

Check for `pip` or `pip3` executable in the CLI:
```bash
$ pip3

Usage:   
  pip3 <command> [options]
  # ...
  # ...


$ pip3 --version
pip 21.2.3 from /Users/pushkar/Desktop/practice/venv/lib/python3.9/site-packages/pip (python 3.9)
```

To know where it is installed, use the `where` command:
```bash
$ where pip
/Users/pushkar/opt/anaconda3/bin/pip

$ where pip3
/usr/local/bin/pip3
/usr/bin/pip3
/Users/pushkar/opt/anaconda3/bin/pip3
```

#### Running pip as a module

This has one benefit: Making sure we are using the right pip version when we run the basic `pip` executable without the version! (For python2.7 or Python3)

Example of making sure pip3 is being run:
- Use a specific python interpreter (Ex: 2.7 or 3)
- Use the `-m` flag to run a file as a module
- Pass `pip` as the file
```bash
$ python3 -m pip

Usage:   
  /usr/local/opt/python@3.11/bin/python3.11 -m pip <command> [options]

Commands:
  install                     Install packages.
  download                    Download packages.
  # ...
  # ...
```

#### Best setup by creating a virtual environment

To avoid installing packages directly into your system Python installation, you can use a **virtual environment**. 

- A virtual environment provides an isolated Python interpreter for your project
- Any packages that you use inside this environment will be independent of your system interpreter
- This means that you can keep your project’s dependencies separate from other projects and the system at large.

Using `pip` inside a virtual environment has three main advantages. You can:

1. Be sure that you’re using the right Python version for the project at hand
2. Be confident that you’re referring to the correct pip instance when running pip or pip3
3. Use a specific package version for your project without affecting other projects

Python 3 has the built-in **`venv`** module for creating virtual environments. 

- This module helps you create virtual environments with an isolated Python installation
- Once you’ve **activated** the virtual environment, then you can install packages into this environment. 
- The packages that you install into one virtual environment are ***isolated*** from all other environments on your system.

```bash
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip3 --version
pip 21.2.3 from .../python3.10/site-packages/pip (python 3.10)
(venv) $ pip --version
pip 21.2.3 from .../python3.10/site-packages/pip (python 3.10)
```

You create a virtual environment named `"venv"` by using Python’s built-in `venv` module. Then you activate it with the source command. The parentheses (`()`) surrounding your venv name indicate that you successfully activated the virtual environment.

You check the version of the pip3 and pip executables inside your activated virtual environment. 
- Both point to the same pip module, so once your virtual environment is activated, you can use either `pip` or `pip3`.

##### Virtual environment variable

```shell
# MacOS / Linux
(venv) $ echo $VIRTUAL_ENV
/Users/pushkar/Desktop/practice/venv
```

##### pip config file

Every virtual environment has a pip config file:
We can see the values of each config by using the `config list` command. Ex:
```shell
(venv) $ pip config list
global.disable-pip-version-check='True'
global.index-url='https://pypi.org/simple'
global.trusted-host='pypi.org'


(venv) $ pip config get global.index-url
https://pypi.org/simple


(venv) $ pip config set global.index-url https://custom.com/pypi/simple


# Find which pip.conf is going to be used and where are they all located:
(venv) $ pip config list -vv
For variant 'global', will try loading '/Library/Application Support/pip/pip.conf'
For variant 'user', will try loading '/Users/pushkar/.pip/pip.conf'
For variant 'user', will try loading '/Users/pushkar/.config/pip/pip.conf'
For variant 'site', will try loading '/Users/pushkar/Desktop/practice/venv/pip.conf'
global.disable-pip-version-check='True'
global.index-url='https://pypi.org/simple'
global.trusted-host='pypi.org'
```

#### Installing pip packages

Community packages are published to the [**Python Package Index**](https://pypi.org/), also known as PyPI (pronounced ***Pie Pea Eye***).

- PyPI hosts an extensive collection of packages, including development frameworks, tools, and libraries. 
- Many of these packages provide friendly interfaces to the Python standard library’s functionality.

Example package used: `requests`. This library helps you to interact with web services by abstracting the complexities of HTTP requests

To install packages, pip provides an `install` command. You can run it to install the `requests` package:
It’s also possible to install multiple packages in a single command (Space separated package names)

```shell
(venv) $ pip install requests
```

1. The pip command looks for the package in PyPI
2. Resolves its dependencies, and 
3. Installs everything in your current Python environment to ensure that requests will work

The `pip install <package>` command always looks for the ***latest version*** of the package and installs it. It also searches for dependencies listed in the package metadata and installs them to ensure that the package has all the requirements that it needs.

Installing specific versions. Examples:
- `pip install example-package==1.2.2`
- `pip install example-package>=2.0.1`
- `pip install example-package<=2.0.1`
- `pip install 'example-package>=1.3.0,<1.4.0'`

#### Listing the installed packages and their versions

Use the `list` command provided by pip.

```shell
(venv) $ pip list

Package            Version
------------------ ---------
certifi            2022.12.7
charset-normalizer 3.1.0
idna               3.4
pip                21.2.3
requests           2.28.2
setuptools         57.4.0
urllib3            1.26.15
```

#### Get more information about an installed package

Run the `show <package>` command provided by pip

```shell
(venv) $ pip show requests

Name: requests
Version: 2.28.2
Summary: Python HTTP for Humans.
Home-page: https://requests.readthedocs.io
Author: Kenneth Reitz
Author-email: me@kennethreitz.org
License: Apache 2.0
Location: /Users/pushkar/Desktop/practice/venv/lib/python3.9/site-packages
Requires: idna, urllib3, charset-normalizer, certifi
Required-by: 
```

Notice the last two fields, `Requires` and `Required-by`. 
- The `show` command tells you that requests requires `certifi`, `idna`, `charset-normalizer`, and `urllib3`. You probably want to uninstall those too. 
- Notice that requests isn’t required by any other package. So it’s _safe_ to uninstall it.

#### Importing an installed package

Importing a package is done just like it is done with a standard library (or a module within the same directory)
- Use the `import` statement as you would with any other module

```python
import requests

print(requests.__version__)

# 2.28.2
```

#### Uninstalling a package via pip

**Unfortunately: `pip` does not uninstall dependencies when you uninstall the original package**

You should run the show command against all of the requests dependencies to ensure that no other libraries also depend on them (`Required-by`). Once you understand the dependency order of the packages that you want to uninstall, then you can remove them using the **`uninstall`** command:

```shell
(venv) $ pip uninstall certifi
(venv) $ pip uninstall urllib3 -y # `-y` suppresses the information dialog
(venv) $ pip uninstall -y charset-normalizer idna requests
```

#### Using a custom package index

`pip` also gives you the option to define a custom package index.

- You can use the `-i` flag to provide a custom URL in your `pip install` command
- You can also download the package directly from github. Ex: `pip install git+https://github.com/realpython/rptree`

#### Pinning requirements

Using the virtual environment `venv`, one can install packages as dependencies for a project. But, how can we pin these dependencies so that when someone else needs to use your project on their system, they download the exact same packages and versions as you did?

**Why?**
Maybe a specific version of a package contains a new feature that you rely on, or the version of a package that you’re using is incompatible with former versions.

These external dependencies are also called requirements. You’ll often find Python projects that pin their requirements in a file called `'requirements.txt'` or similar. The requirements file format allows you to specify precisely which packages and versions should be installed.

- Running `pip freeze` command that outputs the installed packages in requirements format. 
- You can use this command, redirecting the output (`>`) to a file to generate a requirements file.
- The file can be named anything but the general convention is `requirements.txt`

```shell
(venv) $ pip freeze
certifi==2022.12.7
charset-normalizer==3.1.0
idna==3.4
requests==2.28.2
urllib3==1.26.15


(venv) $ pip freeze > requirements.txt

# Contents of requirements.txt:
# certifi==2022.12.7
# charset-normalizer==3.1.0
# idna==3.4
# requests==2.28.2
# urllib3==1.26.15
```

**Using the requirements file to install dependencies on another system**

When you want to replicate the environment in another system, you can run `pip install`, using the **`-r` switch** to specify the requirements file:
```shell
(venv) $ pip install -r requirements.txt
```

You can submit `requirements.txt` into a version control system like `Git`.

[Read more about pip](https://realpython.com/what-is-pip/#:~:text=The%20pip%20command%20looks%20for,the%20package%20and%20installs%20it)

_Comparison with JavaScript:_
- Node Package Manager (**NPM**) is the NodeJS equivalent of PIP (a standard package manager)
- We do not have a virtual environment but every project can have its own `node_modules` folder (similar to the folder created for `venv`) where packages defined in `package.json` file are installed. In this way, we avoid using any globally (system) installed versions of packages for any of our projects (thus, avoiding version mismatches)
- Pinning requirements (like `requirements.txt`): To avoid auto-update of package versions for dependencies within the different libraries used inside a Node project, we can use `yarn` to create `yarn.lock` file to freeze versions (Alternative: `npm > version 5` with `package-json.lock`)
- Even with NPM, we can `import` our NPM packages by name. Only custom modules need a path (Core & NPM installed packages do not)

#### Alternatives to PIP

1. **Conda:** Conda is a package, dependency, and environment manager for many languages, including Python. It comes from Anaconda, which started as a data science package for Python. Consequently, it’s widely used for data science and machine learning applications. Conda operates its own index to host compatible packages.
2. **Poetry:** Poetry will look very familiar to you if you’re coming from JavaScript and npm. Poetry goes beyond package management, helping you build distributions for your applications and libraries and deploying them to PyPI.
3. **Pipenv:** Pipenv is another package management tool that merges virtual environment and package management in a single tool. Pipenv: A Guide to the New Python Packaging Tool is a great place to start learning about Pipenv and its approach to package management.

### Debugging python with pdb

**`pdb`** is part of Python’s standard library, so it’s always there and available for use.

#### Adding a breakpoint

Insert the following code at the location where you want to break into the debugger:
```python
import pdb; pdb.set_trace()
```

Starting in Python 3.7, we can just add a simpler function `breakpoint()` that does the same thing.

Example:
```python
# add_module.py
age = 29
min_age = 18

def add_nums(*nums):
  sum = 0
  for num in nums:
    sum += num
  return sum

def add_two_nums(num1, num2):
  return num1 + num2

import pdb; pdb.set_trace()

add_nums(1, 5, 4)
add_two_nums(age, min_age)
```

#### Running the program with the debugger

Once `pdb` has been imported and the trace has been set, execute the program normally (Ex: `python <module>`).
You should be able to see the `(pdb)` Command Line program execute

```shell
$ python add_module.py
> ./add_module.py(12)<module>()
-> add_nums(1, 5, 4)
(Pdb) 
```

- `>` starts the 1st line and tells you which source file you are in
- After the filename, there is the current line number in parentheses
- Next is the name of the function. 
- (In this example, since we’re not paused inside a function and at module level, we see `<module>()`)

- `->` starts the 2nd line and is the current source line where Python is paused
- This line hasn’t been executed yet. 

- `(Pdb)` is pdb’s prompt. It is waiting for a command

#### Quit pdb

Type the `q` command
```shell
$ python add_module.py
> ./add_module.py(12)<module>()
-> add_nums(1, 5, 4)
(Pdb) q
# Exits pdb
$ _
```

#### Print an expression

Print an expression (including variables) with `p <expression>`:
```shell
$ python add_module.py
> ./add_module.py(15)<module>()
-> add_nums(1, 5, 4)
(Pdb) p age
29
(Pdb) p min_age
18
(Pdb) p add_nums
<function add_nums at 0x7f87c11d3f70>
(Pdb) p add_nums(1, 3)
4
(Pdb) 
```

#### Stepping through code

- Use `n` (next) : execute program until the next line in the current function (or return statement)
- Use `s` (step) : similar to next but it will stop at the next line in a foreign (invoked) function as well - if it is the next line! "Step into"

```shell
$ python add_module.py
> ./add_module.py(15)<module>()
-> add_nums(1, 5, 4)
(Pdb) n
> ./add_module.py(16)<module>()
-> add_two_nums(age, min_age)
(Pdb) 
```

```shell
$ python add_module.py
> ./add_module.py(15)<module>()
-> add_nums(1, 5, 4)
(Pdb) s
--Call--
> ./add_module.py(4)add_nums()
-> def add_nums(*nums):
```

#### Listing the function source code

- Use the `l` (list) command (Lists a shorter version of the function or frame, 11 lines by default)
```shell
$ python add_module.py
> ./add_module.py(15)<module>()
-> add_nums(1, 5, 4)
(Pdb) s
--Call--
> ./add_module.py(4)add_nums()
-> def add_nums(*nums):
(Pdb) ll
def add_nums(*nums):
  5       sum = 0
  6       for num in nums:
  7         sum += num
  8       return sum
```

- You can also use the `ll` (long list) command (list the whole source code for the current function or frame)

#### Setting and removing breakpoints

Instead of breaking line-by-line (`n` or `s`), add breakpoints using `b` (break)

- Can specify a line number (or)
- Can specify a function name

Syntax: `b(reak) [ ([filename:]lineno | function) [, condition] ]`

Provide a **condition** (Extremely useful feature)
- We can conditionally break at a line or function i.e only if the condition is `True`

The command `c` (continue) continues execution until a breakpoint is found.

```shell
$ python add_module.py
> ./add_module.py(15)<module>()
-> add_nums(1, 5, 4)
(Pdb) b add_two_nums
Breakpoint 1 at ./add_module.py:10
(Pdb) c
> ./add_module.py(11)add_two_nums()
-> return num1 + num2
```

View all the set breakpoints with `b` (& no arguments):
```shell
(Pdb) b
Num Type         Disp Enb   Where
1   breakpoint   keep yes   at /Users/pushkar/Desktop/practice/add_module.py:10
```

It changes output when a breakpoint is hit:
```shell
(Pdb) b
Num Type         Disp Enb   Where
1   breakpoint   keep yes   at /Users/pushkar/Desktop/practice/add_module.py:10
        breakpoint already hit 1 time
```

Disable breakpoints with `disable bpnumber` (where `bpnumber` is the one that appears for a breakpoint in `b` list)
```shell
(Pdb) disable 1
Disabled breakpoint 1 at /Users/pushkar/Desktop/practice/add_module.py:10
(Pdb) b
Num Type         Disp Enb   Where
1   breakpoint   keep no    at /Users/pushkar/Desktop/practice/add_module.py:10
        breakpoint already hit 1 time
```

Remove breakpoints using the `cl` (clear) command.
- Simple syntax: `cl bpnumber`
- (Complex syntax (by filename & line number): `cl filename:lineno`)
```shell
(Pdb) cl 1
Deleted breakpoint 1 at /Users/.../add_module.py:10
(Pdb) b
(Pdb) 
```

#### Trace the caller function

Use the `w` (where) command to see from where the current function was called.
- It prints a stack trace of the function call stack

```shell
(Pdb) w
  /add_module.py(16)<module>()
-> add_two_nums(age, min_age)
> ./add_module.py(11)add_two_nums()
-> return num1 + num2
```

#### pdb cheatsheet

| Command | Description |
| ------- |:------------:|
| p       | Print the value of an expression. |
| pp	    | Pretty-print the value of an expression. |
| n	      | Continue execution until the next line in the current function is reached or it returns. |
| s       |	Execute the current line and stop at the first possible occasion (either in a function that is called or in the current function). |
| c       |	Continue execution and only stop when a breakpoint is encountered. |
| unt	    | Continue execution until the line with a number greater than the current one is reached. With a line number argument, continue execution until a line with a number greater or equal to that is reached. |
| l       |	List source code for the current file. Without arguments, list 11 lines around the current line or continue the previous listing. |
| ll	    | List the whole source code for the current function or frame. |
| b       |	With no arguments, list all breaks. With a line number argument, set a breakpoint at this line in the current file. |
| w       |	Print a stack trace, with the most recent frame at the bottom. An arrow indicates the current frame, which determines the context of most commands. |
| a       | Prints out all the arguments the current function received |
| r       | Continues execution until the current function returns |
| u       |	Move the current frame count (default one) levels up in the stack trace (to an older frame). |
| d       |	Move the current frame count (default one) levels down in the stack trace (to a newer frame). |
| h       |	See a list of available commands. |
| h <topic> |	Show help for a command or topic. |
| h pdb	  | Show the full pdb documentation. |
| q       |	Quit the debugger and exit. |

#### pdb vs ipdb

Same thing but with enhanced interactive experience provided by _IPython_.

`pdb`: the Python Debugger, is an interactive debugger that is part of the Python standard library. It allows you to jump into a shell at arbitrary breakpoints in your code, where you can inspect the code and runtime, walkthrough the code line by line, change the values of objects, and more.

`ipdb`: the IPython-enabled Python Debugger, is a third party interative debugger with all pdb's functionality and adds IPython support for the interactive shell, like tab completion, color support, magic functions and much more. You use `ipdb` just as you use `pdb` but with an enhanced user experience.

[Read more about pdb](https://realpython.com/python-debugging-pdb/#essential-pdb-commands)

_Comparison with JavaScript:_
- In JavaScript, we use the `debugger;` command to debug.
- Browser consoles provide an interactive debuggign experience
- Code editors can be modified to allow interactive debugging on seeing a `debugger;` 
- Terminal-only debugging like in python is not really possible (?unsure)
