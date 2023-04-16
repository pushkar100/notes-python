# Python for JavaScript Developers Notes

Learning Python as a JavaScript developer by comparing the syntax and constructs of each language with the other.

- [Python for JavaScript Developers Notes](#python-for-javascript-developers-notes)
  * [Basics](#basics)
    + [Data types](#data-types)
    + [Type casting](#type-casting)
    + [Variables](#variables)
      - [Declaring a variable](#declaring-a-variable)
      - [Data type of a variable](#data-type-of-a-variable)
      - [Default value of a variable](#default-value-of-a-variable)
      - [Re-assigning variables](#re-assigning-variables)
      - [Variable naming rules](#variable-naming-rules)
      - [Variable naming conventions](#variable-naming-conventions)
    + [Strings](#strings)
      - [Defining a string](#defining-a-string)
      - [Changing the case of strings](#changing-the-case-of-strings)
      - [Concatenating strings](#concatenating-strings)
      - [Escaping characters in a string](#escaping-characters-in-a-string)
      - [Stripping whitespaces from strings](#stripping-whitespaces-from-strings)

## Basics

**Versions used**
- Python version: `3+`
- JavaScript version: `ES6+`

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

Comparison with JavaScript:
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

Comparison with JavaScript:
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

Comparison with JavaScript:
- JavaScript variable declarations are prefixed with a scope identifier like `var`, `const`, `let`

#### Data type of a variable

Python is dynamically typed i.e The type of a variable is inferred at runtime and is updated when the assignment changes
Example
```python
my_name = 'Pushkar' # string
my_name = 20 # integer
```

Comparison with JavaScript:
- JavaScript is also dynamically typed

#### Default value of a variable

Declaration comes with assignment. Both have to be done

```python
foo # NameError: name 'foo' is not defined

foo = 'bar' # ✓
```

Comparison with JavaScript:
- In JavaScript, it is possible to have variable declarations that are unassigned
- The value in such a case will be `undefined`

#### Re-assigning variables

Variables can be re-assigned in Python

```python
foo = 5
foo = 'bar' # ✓
```

Comparison with JavaScript:
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

Comparison with JavaScript:
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

Comparison with JavaScript:
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

Comparison with JavaScript:
- In JavaScript, we use `console.log()` to print to the browser or node console (terminal)

### Strings

#### Defining a string

Use `''` or `""` (Single or double quotes)

Comparison with JavaScript:
- Same in JavaScript but you can also use the ` `` ` for strings with interpolation

#### Changing the case of strings

1. Capitalize a string using `.capitalize()`

Only updates the first letter to be upper case in the string (instead of every word in the string)

```python
x = 'pushkar dk'
x.capitalize() # 'Pushkar dk'
```
Does not affect the original string variable (immutable)

2. Title-ify a string using `.title()`

```python
x = 'pushkar dk'
x.title() # 'Pushkar Dk'
```
Does not affect the original string variable (immutable)

3. Change to upper case using `.upper()`

```python
x = 'pushkar dk'
x.upper() # 'PUSHKAR DK'
```
Does not affect the original string variable (immutable)

4. Change to upper case using `.lower()`

```python
x = 'pushkar dk'
x.lower() # 'pushkar dk'
```
Does not affect the original string variable (immutable)

Comparison with JavaScript:
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

Comparison with JavaScript:
- In JavaScript, you can use the same `+` operator to concatenate strings
- However, **sometimes** we do not have to explicitly convert numbers. JS will try type coerce them into a string
  - Ex: `'My age is' + 15 // 'My age is 15'`
- There is another way to build strings in JS: Interpolation. 
  - Ex: `age = 15; x = `My age is ${age}`;`

#### Escaping characters in a string

1. Escape newlines with `\n`
2. Escape tabs with `\t`
3. Escape characters with a backslash. Ex: `\"` and `\'`

Comparison with JavaScript:
- Same

#### Stripping whitespaces from strings

1. Remove whitespace from the right of a string with `.rstrip()`

```python
name = '  pushkar  '
name.rstrip() # '  pushkar'
```

2. Remove whitespace from the left of a string with `.lstrip()`

```python
name = '  pushkar  '
name.lstrip() # 'pushkar  '
```

3. Remove all leading and trailing spaces with `.strip()`

```python
name = '  pushkar  '
name.strip() # 'pushkar'
```

Comparison with JavaScript:
- In JavaScript, we originally only had a `.trim()` method to trim all leading and trailing spaces (Like `.strip()`)
- In later versions. [`.trimEnd()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trimEnd) and [`.trimStart()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trimStart) have been added with good browser support

#### Casting a value into a string

1. Use the `str()` function

```python
str(4) # '4'
str(True) # 'True'
```

Comparison with JavaScript:
- In JavaScript, we use the `String()` function or just type coerce by `''` or `""` or ` `${}` `
