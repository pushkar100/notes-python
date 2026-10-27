# Python tutorial

[Course link: FCC Youtube Video](https://www.youtube.com/watch?v=rfscVS0vtbw)

# Table of contents

- [Python tutorial](#python-tutorial)
  - [Intro](#intro)
  - [First Python code](#first-python-code)
  - [Variables and Data Types](#variables-and-data-types)
  - [Strings in Python](#strings-in-python)
  - [Numbers in Python](#numbers-in-python)
  - [Getting input from users](#getting-input-from-users)
  - [Lists](#lists)
  - [Tuples](#tuples)
  - [Functions](#functions)
  - [If construct](#if-construct)
  - [Logical operators](#logical-operators)
  - [Relational operators](#relational-operators)
  - [Assignment shorthands](#assignment-shorthands)
  - [Dictionary](#dictionary)
  - [While loops](#while-loops)
  - [For loops](#for-loops)
  - [Exponent function](#exponent-function)
  - [2D lists and nested loops](#2d-lists-and-nested-loops)
  - [Comments](#comments)
  - [Try and except](#try-and-except)
  - [Reading from and writing to files](#reading-from-and-writing-to-files)
  - [Modules](#modules)
  - [Pip](#pip)
  - [Object oriented python](#object-oriented-python)
  - [Python interpreter](#python-interpreter)
  - [Practice Exercises](#practice-exercises)

## Intro

### Python download link

[Download python](https://www.python.org/downloads/)

### Python 2 vs Python 3

Python 2 is a legacy version of Python. All major development now and in the future will only happen on Python 3. Therefore, it is better to begin learning Python 3 itself.

One reason to use Python 2 is that a lot of the libraries written in Python 2 been around for so long. Therefore, if you intend to use libraries that don't have a stable Python 3 version of the same, use Python 2.

There are not too many differences between Python 2 & 3. Learning one will not add that much of an overhead to pick up the other.

On a Mac, Python 2 comes installed by default.

### Python IDE

You can write Python code on any editor & execute the code on a shell after python has been installed. However, there are some IDEs that make Python development easier! One such tool is [PyCharm](https://www.jetbrains.com/pycharm/download/#section=mac) from JetBrains.

PyCharm [getting started](https://www.jetbrains.com/help/pycharm/quick-start-guide.html) guide.

## First Python code

Create a python file (ending with `.py`) (In pycharm you would right click project, click new, click on python file)

Add the following `print` statement to the file

```python
print("Hello world")
```

To run the code, type in `python <path to the .py file>` in your terminal. If you are using PyCharm then select "Run" and choose which file to run.

The output is the following:

```python
Hello world
```

The python compiler executes the instructions in the order they are written.

Example:

```python
print("    /|")
print("   / |")
print("  /  |")
print(" /   |")
print("/____|")
```

This prints the following:

```
    /|
   / |
  /  |
 /   |
/____|
```

And this:

```python
print("/____|")
print("    /|")
print("   / |")
print("  /  |")
print(" /   |")
```

prints the following:

```
/____|
    /|
   / |
  /  |
 /   |
```

Therefore, the order of the instructions matters in Python.

**Comments** in Python start with **`#`**. The rest of the line becomes an inline comment

```python
# Adds two numbers
```

## Variables and Data Types

Variables in Python hold values you want to reuse or modify in a single place. They are placeholders & act as identifiers for the data you wish to store.

**Variable initialization:**

```python
character_name = "Pushkar"
character_age = 43
print("The main character's name is " + character_name)
print(character_name + " is " + str(character_age) + " years old")
```

```
The main character's name is Pushkar
Pushkar is 43 years old
```

You can concatenate strings with variables of type string but for other types, you need to cast them to strings with the **`str()`** method.

**Variable reassignment**:

We can re-assign variables by using the same syntax to initialize them:

```python
character_name = "Pushkar"
character_age = 43
print("The main character's name is " + character_name)
print(character_name + " is " + str(character_age) + " years old")

character_name = "Tom"
print("The side-kick's name is " + character_name + " and he is a teenager")
```

```
The main character's name is Pushkar
Pushkar is 43 years old
The side-kick's name is Tom and he is a teenager
```

**Data types:**

There are many data types in Python. The most commonly used ones are:

- Strings
- Numbers (including floating-point numbers) (45, 1.109, 100.50, ...)
- Booleans
  - Note that in Python, the two Boolean values are `True` & `False` i.e They are **capitalized**!

```python
character_name = "Pushkar"
isMale = True
print("The main character's name is " + character_name)
print("Is male? " + str(isMale))
```

```
The main character's name is Pushkar
Is male? True
```

## Strings in Python

- You may use double quotes ("") or single quotes ('')

```python
print('Hey')
```

```
Hey
```

- You may use the backslash (`\`) character as an escape string!

```python
print("Giraffe\nAcademy")

quote = "Baz \"for the win\""
print(quote)
```

```
Giraffe
Academy
Baz "for the win"
```

- String concatenation is done with the `+` character:

```python
print("Hello " + "friend")
```

```
Hello friend
```

- String methods: These are auto-suggested in PyCharm when you put a dot(`.`) in front of any string

  - `.lower()`: Lowercases the string
  - `.upper()`: Uppercases the string
  - `.isupper()`: Returns `True` if the string is uppercase
  - `.islower()`: Returns `True` if the string is lowercase
  - `.capitalize()`: Capitalizes the string

  We can also chain the methods such as these as they return the formatter string back!

```python
text = "FunKY tExT"
print(text.lower())
print(text.upper())
print(text.capitalize())
print(text.upper().isupper())
```

```
funky text
FUNKY TEXT
Funky text
True
```

- Fetching characters from an index of a string: Use `.index()` method
- Find the length of a string: Use `len()` function (Note: It is not a string method but a separate global)

```python
animal = "Giraffe"
print(animal[0])
print(animal[5])
print(len(animal))
```

```
G
f
7
```

- Finding the index of a character or a substring: Use the `.index()` method

```python
animal = "Giraffe"
print(animal.index("a"))
print(animal.index("ffe"))
```

```
3
4
```

- Finding the index of a *non-existent* substring throws an **error**! (unlike in JS where it returns -1):

```python
animal = "Giraffe"
animal.index("abc")  # Error
```

```
Traceback (most recent call last):
  File "/Users/pushkardk/PycharmProjects/Giraffe/app.py", line 4, in <module>
    animal.index("abc")  # Error
ValueError: substring not found
```

- Replace substrings: Use `.replace()` method. Arguments are the target substring & the replacer string. Note that this method does not modify the original string variable unless the variable is reassigned with the return value of the method

```python
academy = "Giraffe Academy"

print(academy.replace("Giraffe", "Elephant"))
print(academy)

academy = academy.replace("Giraffe", "Elephant")
print(academy)
```

```
Elephant Academy
Giraffe Academy
Elephant Academy
```

## Numbers in Python

- We can do arithmetic with numbers just like in JS:

```python
print(3 + 4.5)
print(4 * 5)
print(40 / 2)
print(10 % 3)
```

```
7.5
20
20.0
1
```

- The arithmetic for numbers follows well defined precedence & associativity rules like in other languages. Use `()` to override this

```python
print(3 * 4 + 5)
print(3 * (4 + 5))
```

```
17
27
```

- Numbers can be stored in variables since it is a data type too! We can print numbers as well

```python
my_num = 5
print(5)
```

```
5
```

- Concatenating numbers with strings: Use `str()` global method

```python
print(str(my_num))
print("My fave number: " + str(my_num))
```

```
5
My fave number: 5
```

- Global functions that work on numbers (They are not defined on the number type as a method)
  - `abs()`: Returns the absolute value
  - `pow()`: Returns the power of a base number (1st argument) to its exponent (2nd argument)
  - `max()`: Returns the max of two numbers
  - `min()`: Returns the min of two numbers
  - `round()`: Rounds off numbers to the nearest integer

```python
num = -4
print(abs(num))
print(pow(4, 2))
print(max(10, -12))
print(min(5.1, 5.3))
print(round(3.2))
print(round(3.7))
```

```
4
16.0
10
5.1
3
4
```

- Using external **modules**: Some functions are defined in other files known as modules and we "import" them into our application for use. Many more math related functions are not readily available unless we import them from the built-in **math** library
  - `floor()`: Returns the nearest integer less than the number
  - `ceil()`: Returns the nearest integer greater than the number
  - `sqrt()`: Returns the square root of a number

```python
from math import *

print(floor(4.1))
print(ceil(4.1))
print(sqrt(36))
```

```
4
5
6.0
```

## Getting input from users

We can make our programs interactive by asking for an input from the user. We do this by giving a **`input()`** to the user.

What is returned by this function is the value entered by the user. It can be saved in a variable and used later.

The command line data is a **string** even if you enter a number (default).

```python
user = input('Enter your name please: ')
age = input('What is your age? ')

print('You are ' + user + '! Your age is ' + age)
```

```
Enter your name please: Pushkar
What is your age? 28
You are Pushkar! Your age is 28
```

**Converting input string into a number**:

By default, inputs are stored as strings.

```python
num1 = input('Type 1st number: ')
num2 = input('Type 2nd number: ')
print(num1 + num2) # Does not print the sum but a string concatenated value
```

```
Type 1st number: 3
Type 2nd number: 5
35
```

There are two ways to store an input as a number i.e explicit typecasting:

1. Use `int()` global method: Converts a value to an integer (Note: This is more specific than converting to a number). When you are sure that both the numbers are integers, use this method. Else, it throws an error!

```python
num1 = input('Type 1st number: ')
num2 = input('Type 2nd number: ')
sum = int(num1) + int(num2)
print(sum)
```

```
Type 1st number: 4
Type 2nd number: 9
13
```

2. Use `float()` global method: converts a value into a floating point number. Therefore, more or less the same type as any kind of number. Can use on both integers as well as floating-point numbers

```python
num1 = input('Type 1st number: ')
num2 = input('Type 2nd number: ')
sum = float(num1) + float(num2)
print(sum)
```

```
Type 1st number: 2.56
Type 2nd number: 3
5.5600000000000005
```

## Lists

Lists are a bunch of data just like arrays in language like JS. Use the `[]` brackets and comma separator `,` to add items to a list.

The items in the list can be of any value. Ex: All strings, all numbers, a mix of strings, numbers, and booleans, and so on.

```python
friends = ["Tom", "Ram", "Sita"]
print(friends)
```

```
['Tom', 'Ram', 'Sita']
```

- Fetch individual array items using index values:

```python
print(friends[0])
print(friends[2])
```

```
Tom
Sita
```

- Lists can have items of different data types:

```python
data = [1, "Liverpool street", "NW3", 44, True]
print(data)
print(data[3])
print(data[4])
```

```
[1, 'Liverpool street', 'NW3', 44, True]
44
True
```

- Fetching **sub-lists**: Use the `:` operator within the `[]`
  - `[x, y]`: Fetches list from index `x` (inclusive) to `y`  (exclusive)
  - `[x:]`: Fetches list from index `x` to the very end (inclusive on both ends)
  - `[:y]`: Fetches list from start (inclusive) till `y` (exclusive)

```python
friends = ["Tom", "Ram", "Sita", "Oscar", "Justin"]
print(friends[1:])  # Includes data from index 1 till the end
print(friends[:1])  # Includes data from start to index 1 but does not include index 1 (exclusive)
print(friends[2:4])  # Includes data from index 2 (inclusive) to index 4 (exclusive)
```

```
['Ram', 'Sita', 'Oscar', 'Justin']
['Tom']
['Sita', 'Oscar']
```

- We can **re-assign** list items:

```python
friends = ["Tom", "Ram", "Sita", "Oscar", "Justin"]
friends[3] = "Mike"
print(friends)
```

```
['Tom', 'Ram', 'Sita', 'Mike', 'Justin']
```

### List methods

There are many built-in methods in Python that help us work with lists.

- Concatenate 2 lists with **`.extend()`**. It mutates the target array (no copy)

```python
luckyNumbers = [10, 92, 1, 49, 6, 64, 10]
luckyNames = ["Annabelle", "Joel", "Rahul", "Naina"]
luckyNames.extend(luckyNumbers)
print(luckyNames)
```

```
['Annabelle', 'Joel', 'Rahul', 'Naina', 10, 92, 1, 49, 6, 64, 10]
```

- Append values to the end of the list with **`.append`** (Similar to the push() method in JS):

```python
vals = [1, "hello"]
vals.append("bye")
print(vals)
```

```
[1, 'hello', 'bye']
```

- Insert a value in the middle of the list using **`insert()`**: Pass an index and a value. It shifts all elements from that index to the right and inserts the value

```python
nums = [1, 2, 3]
nums.insert(1, 2000)
print(nums)
```

```
[1, 2000, 2, 3]
```

- Remove an item by value with **`remove()`**:

```python
names = ["David", "Goliath", "Raavan", "Krishna"]
names.remove("Raavan")
print(names)
```

```
['David', 'Goliath', 'Krishna']
```

- Pop off the last element with **`.pop()`**:

```python
names = ["David", "Goliath", "Raavan", "Krishna"]

names.pop()
print(names)
```

```
['David', 'Goliath', 'Raavan']
```

- Get the index of a value in the list with **`.index()`**:

```python
names = ["David", "Goliath", "Raavan", "Krishna"]
print(names.index("David"))
print(names.index("Goliath"))
# print(names.index("DoesNotExist")) Will throw an error if it does not exist in the list
```

```
0
1
```

- Count the occurrences of an item in the list: Use **`.count()`**

```python
names = ["Ram", "Sita", "Ram", "Tim", "Tim", "Tim"]
print(names.count("Ram"))
print(names.count("Tim"))
```

```
2
3
```

- Sort a list: Use **`.sort()`**. For numbers, it is in the **ascending** order by default & for strings too it is in the ascending order

```python
luckyNumbers = [10, 92, 1, 49, 6, 64, 10]
luckyNumbers.sort()
print(luckyNumbers)

luckyNames = ["Annabelle", "Joel", "Rahul", "Naina", "Azhar"]
luckyNames.sort()
print(luckyNames)
```

```
[1, 6, 10, 10, 49, 64, 92]
['Annabelle', 'Azhar', 'Joel', 'Naina', 'Rahul']
```

- Reverse a list with **`.reverse()`**:

```python
luckyNumbers = [10, 92, 1, 49, 6, 64, 10]
luckyNames.reverse()
print(luckyNumbers)
```

```
[10, 92, 1, 49, 6, 64, 10]
```

- Copy one list to another with **`.copy()`**:

```python
nums = [10, 20, 30, 40]
nums2 = nums.copy()
print(nums2)

nums3 = nums[2:].copy()
print(nums3)
```

```
[10, 20, 30, 40]
[30, 40]
```

* Length of a list: Use **`len`** (The same function works for finding lengths of strings well)

## Tuples

Tuples are like lists except that they are **immutable**. That is, once the tuple is create it cannot be changed (modified) whereas a list can be.

Lists are more popular but there are a few reasons to use tuples. For example, we ca use them to store data that we know will not change: coordinates, config details, etc.

```python
coords = (3.1234, 5.2309)
print(coords)

magicNumbersAndNames = (13, 3456, "Pushkar")
print(magicNumbersAndNames)

coordsList = [(2,3), (9, -1), (5, 5)]
print(coordsList)
```

```
(3.1234, 5.2309)
(13, 3456, 'Pushkar')
[(2, 3), (9, -1), (5, 5)]
```

Attempting to change a tuple value will result in an **error**:

```python
coords = (3.1234, 5.2309)
coords[1] = 100
```

```
Traceback (most recent call last):
  File "/Users/pushkardk/PycharmProjects/Giraffe/app.py", line 2, in <module>
    coords[1] = 100
TypeError: 'tuple' object does not support item assignment
```

Note that while a tuple cannot be changed, the variable holding a tuple can be re-assigned to another value without errors (i.e it is not a constant:

```python
coords = (3.1234, 5.2309)
coords = "I am a string"
print(coords)
```

```
I am a string
```

## Functions

Functions start with a `def` keyword. The function body starts with a `:`. 

- Whatever we write inside a function **MUST** be indented. If not, it is not part of the function.
- The convention for function names is to use **underscores (`_`)** as *separators* (or write the name without spaces or capitalization). It is not a convention in python to use camelCase.

```python
def say_hi():
    print('Hello')  # Indentation is a must

say_hi()
```

```
Hello
```

- Functions can take arguments within parentheses `()`

```python
def greet(name):
    print('How are you, ' + name + '?')

greet("Pushkar")
greet("Mike")
```

```
How are you, Pushkar?
How are you, Mike?
```

- Functions can take in multiple arguments as well:

```python
def print_user_details(name, age, profession):
    print("Name: " + name)
    print("Age: " + str(age))
    print("Profession: " + profession)

print_user_details("Ralph", 22, "Software developer")
```

```
Name: Ralph
Age: 22
Profession: Software developer
```

- We can **return** values from a function and use them later:

```python
def cube(num):
    return num * num * num

print(cube(4))

result = cube(3)  # Save return value in a variable
print(result)
```

```
64
27
```

- If no value is returned from a function, the type is **`None`**:

```python
def cube(num):
    num * num * num
    # anything after return is not executed

print(cube(4))  # None
```

```
None
```

## If construct

**`If`** statement:

- Use the `if` keyword followed by a condition (boolean expression) and `:`
- Use indentation for each statement or body of statements inside a clause

```python
if 2 > 0:
    print('2 > 0')
```

```
2 > 0
```

**`elif`** statement:

- Same syntax as that of an `if`
- Cannot be written without a preceding`if` clause

```python
if 2 > 2:
    print('2 > 2')
elif 2 > 1:
    print('2 > 1')
```

```
2 > 1
```

**`else`** statement:

- The last clause in an if construct (optional)
- Does not allow us to provide a conditional expression

```python
a = 2
if a > 5:
    print('a > 5')
elif a == 5:
    print('a = 5')
else:
    print('a < 5')
```

```
a < 5
```

## Logical operators

- **`and`** returns `True` if both expressions are true
- **`or`** returns `True` if at least one of the expressions is true
- **`not()`** reverses the boolean value of an operand

```python
a = 6
name = 'Pushkar'
if a > 5 and name == 'Pushkar':
    print('a > 5 and name is Pushkar')
elif a == 5 or name == 'Tom':
    print('a == 5 and name is Tom')
elif not(name == 'Pushkar'):
    print('Name is not Pushkar')
else:
    print('Who cares')
```

```
a > 5 and name is Pushkar
```

## Relational operators

- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal to
- `<=`: Less than or equal to
- `==`: Is equal to
- `!=`: Not equal to

```python
a = 10
if a != 5:
    print('a is not equal to 5')
elif a <= 5:
    print('a is less than or equal to 5')
```

```
a is not equal to 5
```

## Assignment shorthands

- `+=`: Add to
- `*=`: Multiply to
- `/=`: Divide by
- `%=`: Modulus of division by
- ... and many more

```python
a = 10
a += 5
print(a)
a /= 3
print(a)
```

```
15
5.0
```

## Dictionary

**Dictionaries** in python are what **objects** are in Javascript. They are a storage for **key-value pairs**

Syntax:

- Use `{` & `}` to enclose the pairs
- Pairse are written as `<key>: <value>`

```python
monthMap = {
    "Jan": "January",
    "Feb": "February",
    "Mar": "March",
    "Apr": "April",
    "May": "May",
    "Jun": "June",
    "Jul": "July",
    "Aug": "August",
    "Sep": "September",
    "Oct": "October",
    "Nov": "November",
    "Dec": "December"
}
```

- The keys have to be **unique**
- Accessing the keys: Use the `.get()` method or the `[]` bracket notation

```python
print(monthMap["Jan"])
print(monthMap.get("Feb"))
```

```
January
February
```

- Fetching a non-existent key returns `None`.
- We can also supply a second argument to `.get()` for a *default return value* if the key does not exist!

```python
print(monthMap.get("Ggl"))  # None
print(monthMap.get("Ggl", "Invalid key"))  # Invalid key
```

```
None
Invalid key
```

## While loops

- Syntax is similar to `if` statements
- Indentation is required

```python
i = 1
while i <= 10:
    print(i)
    i += 1
print("done with loop")
```

```
1
2
3
4
5
6
7
8
9
10
done with loop
```

## For loops

- Syntax is similar to `if` & `while` 

- Indentation is required

- However, we use a couple of keywords and methods inside the loop condition:

  - Define a ***variable*** and an **`in`** keyword to iterate over items of a list (array) or characters of a string i.e *collections*. This variable exists only within the for loop and not outside. We can name it anything we want.

  ```python
  # collections: string
  password = "xDJhL.8"
  for char in password:
      print(char)
  ```

  ```
  x
  D
  J
  h
  L
  .
  8
  ```

  ```python
  # collections: list (array)
  names = ["Rohit", "Neha", "Vandana", "Akhil", "Pavan"]
  for name in names:
      print(name)
  ```

  ```
  Rohit
  Neha
  Vandana
  Akhil
  Pavan
  ```

  - To iterate over integers from 0 to a number, we use the **`range()`** method. 
    - If we supply one argument, it iterates from 0 to that number but excludes the number (exclusive). 
    - If we supply two arguments, it iterates from the first integer (inclusive) to the second integer (exclusive)

  ```python
  # Range: 0 to given num but exclusive
  for i in range(5):
      print(i)
  ```

  ```
  # Range: 0 to given num but exclusive
  for i in range(5):
      print(i)
  ```

  ```python
  # Range: Integers between two given nums but end is exclusive
  for i in range(3, 8):
      print(i)
  ```

  ```
  3
  4
  5
  6
  7
  ```

  - Alternate way to iterate over a list (array): Use the **`len`** function to compute the length of the list. It is a method useful to *partially iterate* over a list of items

  ```python
  names = ["Pavan", "Neha", "Vandana", "Joel", "Mal"]
  for i in range(len(names)):
      print(names[i])
  ```

  ```
  Pavan
  Neha
  Vandana
  Joel
  Mal
  ```

  ```python
  # Partially loop through a list (first half of the list in this example):
  names = ["Pavan", "Neha", "Vandana", "Joel", "Mal"]
  for i in range(floor(len(names) / 2)):
      print(names[i])
  ```

  ```
  Pavan
  Neha
  ```

## Exponent function

Use **`**`**

  ```python
  # Exponent function
  print(2 ** 3)
  ```

  ```
  8
  ```

  ## 2D lists and nested loops

  Add lists as items of a list to create 2D lists and other types of matrices

  ```python
  array2D = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [9, 10]
  ]
  ```

  *Looping through them:* Add two loops, one nested inside another

  ```python
  for row in array2D:
      for col in row:
          print(col)
  ```

  ## Comments

  - Inline comments:

  ```python
  # Comments: This style is recommended (inline or single line)
  a = 5 # A variable definition
  ```

  - Block comments:

  ```python
  '''
  This is a block comment
  but most ppl prefer to use multiple # comments
  to achieve the same thing
  '''
  ```

Python developers recommend using the **`#`** even for block comments. Therefore, it is more popular.

  ```python
  # This is a mutliline 
  # comment using the pound
  # symbol
  ```

## Try and except

It is a construct to help catch *runtime* errors. It allows us to gracefully handle unexpected errors without the system or the program crashing!

- The clause is similar to a `try..catch` in Javascript
- The syntax & indentation are similar to an`if` statement or a `for` loop
- We can have ***multiple*** except blocks for eeach type of error.

```python
try:
    number = int(input("Enter a number: ")) # Errors if input cannot be transformed into int
    print(number)
except:
    print('invalid input')
```

```
Enter a number: 4
4
```

```
Enter a number: rty
invalid input
```

- *Best practice:* Be ***specific*** about the kind of error you want to except. Generic `except` clauses catch all kind of errors. You might not want to catch all of them or you might want to handle each in a different manner. Therefore, the `except` clause takes a keyword depicting the nature of the error.

```python
try:
    val = 10 / 0 # error
    number = int(input("Enter a number: "))
    print(number)
except ZeroDivisionError:
    print('Divided by 0')
except ValueError:
    print('Invalid input')
```

```
Divided by 0
```

- Use `as` keyword and an identifer in the `except` clause to read the details of an error thrown:

```python
try:
    val = 10 / 0 # error
except ZeroDivisionError as err:
    print(err)
```

```
division by zero
```

## Reading from and writing to files

We can read from & write to files in python.

**Step 1:** Open files with a particular mode. 

Use the **`open`** method (1st argument: Path to file, 2nd argument: mode)

Modes:

- `w`: Write. Rewrites the entire file. Creates a new one if it doesn't exist
- `r`: Read. Read data partially or completely from a file
- `a`: Append. Write to the end of a file without overwriting it.
- `r+`: Read & write mode

**Step 2:** Read or write files using the file handler

The `open` method returns a file handler object that we can use to perform operations on the files. 

- `readable()`: Returns a boolean if the file contents can be read i.e The file was opened in `r` or `r+` mode
- `read()`: Returns the contents of the whole file
- `readline()`: Returns the contents of the file, one line at a time. Starts from the first line & moves the cursor to the next line everytime it is invoked.
- `readlines()`: Returns the contents of the file as a list (array). Each list item is a string representing one line of the file. We can fetch each line in the same way we fetch list items.
- `write()`: Writes data to a file. If mode is `w` then it replaces existing file contents. If the mode is `a` then it appends the data.

**Step 3:** Close the file

We do not wish to keep a connection to the file system open. It is good practice and efficient. To close the file, use the `close()` method on the file handler

Examples:

`employees.txt`:

```
Jim - Salesman
Dwight - Salesman
Pam - Receptionist
Michael - Manager
Oscar - Accountant

```

- Reading:

```python
employee_file = open('employees.txt', 'r')
print(employee_file.readable())
print(employee_file.read())
employee_file.close()
```

```
True
Jim - Salesman
Dwight - Salesman
Pam - Receptionist
Michael - Manager
Oscar - Accountant
```

- Reading line-by-line:

```python
employee_file = open('employees.txt', 'r')
print(employee_file.readline())
print(employee_file.readline())
employee_file.close()
```

```
Jim - Salesman

Dwight - Salesman

```

- Reading the file as a list of lines:

```python
employee_file = open('employees.txt', 'r')
lines = employee_file.readlines()
print(lines)
print(lines[1])
employee_file.close()
```

```
['Jim - Salesman\n', 'Dwight - Salesman\n', 'Pam - Receptionist\n', 'Michael - Manager\n', 'Oscar - Accountant\n']
Dwight - Salesman
```

- Iterating over the lines of a file using a `for` loop:

```python
employee_file = open('employees.txt', 'r')
for employee in employee_file.readlines():
    print(employee)
employee_file.close()
```

```
Jim - Salesman

Dwight - Salesman

Pam - Receptionist

Michael - Manager

Oscar - Accountant

```

- Writing to a file (Append mode):

```python
employee_file = open('employees.txt', 'a')
employee_file.write('Toby - Human Resources')
employee_file.write('\nKelly - Customer Service')
employee_file.close()
```

```
// employees.txt:
Jim - Salesman
Dwight - Salesman
Pam - Receptionist
Michael - Manager
Oscar - Accountant
Toby - Human Resources
Kelly - Customer Service
```

## Modules

We can split our code into modules for re-usability & structure. This is a powerful feature of python and enables us to architect our codebase better! It's extremely good for scalability & maintainability of our code.

Built-in modules are available in python but you can also create your own separate files (modules) & `import` them 

```python
# utils.py
meters_in_a_km = 1000

def get_filename_extension(filename):
    return filename[filename.index('.') + 1:]
```

```python
# app.py
import utils

print(utils.meters_in_a_km)
print(utils.get_filename_extension('employees.txt'))
```

```
1000
txt
```

- Partially import functions and variables from a module

```python
from utils import get_filename_extension

print(get_filename_extension('employees.txt'))
```

```
txt
```

## Pip

Apart from built-in modules & custom ones in your own codebase, there are millions of other python packages out there that we can use.

Some packages come as external modules that can be downloaded and found in the python folder's **`External Libraries`** directory.

Third party APIs have to be installed using a package manager like **`pip`** and they can found in the **`site-packages`** directory within our python folder.

1. **Searching for built-in external libraries:**

We can search python docs for external packages. [Link to page](https://docs.python.org/3/py-modindex.html)

2. **Using 3rd party modules:**

We can google these since there are so many developers who have published packages for use.

Once these are downloaded using `pip`, we can import them like any other module.

**Syntax for downloading a package**:

- Type `pip install <modulename>` in the terminal (Ex: `pip install python-docx`
- To install package for a specific python version use `<pythonversion> -m pip install <modulename>`.
  - Ex: `python3.7 -m pip install python-docx`

## Object oriented python

- Define classes with the **`class`** keyword
- Indentation is a must (similar to functions and if/loop statements)
- The constructor function is **`__init__`**
  - Takes in a `self` parameter first followed by other constructor arguments
- For any other method, the `self` parameter is available as the first argument, before defining the real ones.
- Invoke the class constructor like you'd invoke a function to create the object.

```python
class Student:
    def __init__(self, name, course, gpa, is_on_probation):
        self.name = name
        self.course = course
        self.gpa = gpa
        self.is_on_probation = is_on_probation

    def is_on_honor_roll(self):
        if self.gpa > 3.5:
            return True
        return False

    def change_name(self, new_name):
        self.name = new_name

    def read_name(self):
        print(self.name)
```

```python
from Student import Student

student1 = Student('Jim', 'Business', 3.45, False)
print(student1.gpa)
print(student1.is_on_honor_roll())

student2 = Student('Jam', 'Art', 3.8, True)
student2.change_name('Pam')
student2.read_name()
```

```
3.45
False
Pam
```

### Inheritance

- Pass in the base class in the class signature as an argument.
- Any base class not in the scope must be imported into the module
- We can override existing methods
- We can add additional methods too!

```python
class Chef:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def prepare_salad(self):
        print('preparing salad')

    def make_special_dish(self):
        print('serving special dish: Pizza')
```

```python
from Chef import Chef

class ChineseChef(Chef):
    # Override a base class function:
    def make_special_dish(self):
        print('serving special dish: Daal Makhani')

    # Own functions:
    def make_chinese_dish(self):
        print('serving chinese dish: Noodles')

```

```python
from ChineseChef import ChineseChef

chinese_chef = ChineseChef('Sun Tzu', 25)
chinese_chef.prepare_salad()
chinese_chef.make_special_dish()
chinese_chef.make_chinese_dish()
```

```
preparing salad
serving special dish: Daal Makhani
serving chinese dish: Noodles
```

## Python interpreter

Python installs come with a **`python`** CLI tool.

Use it to test out commands and prototype stuff. It's a good debugging , quick-coding tool

Do not use it to build complete programs or develop anything for production.

---

## Practice Exercises

These hands-on coding exercises test the fundamental concepts covered throughout this tutorial, ranging from basic variables to object-oriented programming.

---

### Exercise 1: Mad Libs Story Generator
- **Concepts Covered:** Variables, strings, user input (`input()`), string concatenation/formatting.
- **Problem Statement:**
  Prompt the user for 4 inputs: a color, a plural noun, a celebrity name, and an adjective. Then, plug those inputs into a short story template and print the finished story to the console.

**Starter Code:**
```python
# Prompt the user for 4 words and print the story
color = input("Enter a color: ")
# complete the rest...
```

**Solution:**
```python
color = input("Enter a color: ")
plural_noun = input("Enter a plural noun: ")
celebrity = input("Enter a celebrity name: ")
adjective = input("Enter an adjective: ")

print("\n--- Here is your Mad Libs Story! ---")
print("Roses are " + color)
print(plural_noun + " are blue")
print("I ran into " + celebrity + " today")
print("And they were feeling super " + adjective + "!")
```

**Sample Output:**
```
Enter a color: magenta
Enter a plural noun: sneakers
Enter a celebrity name: Keanu Reeves
Enter an adjective: energized

--- Here is your Mad Libs Story! ---
Roses are magenta
sneakers are blue
I ran into Keanu Reeves today
And they were feeling super energized!
```

---

### Exercise 2: Temperature Converter & Formatter
- **Concepts Covered:** Numbers, floating-point arithmetic, type casting (`float()`), `round()`, string concatenation.
- **Problem Statement:**
  Write a program that takes a temperature in Celsius from the user (via `input()`), converts it to Fahrenheit using the formula:
  $$F = (C \times 1.8) + 32$$
  Display the result rounded to 2 decimal places.

**Starter Code:**
```python
celsius_input = input("Enter temperature in Celsius: ")
# Cast to float, calculate Fahrenheit, and print result
```

**Solution:**
```python
celsius_input = input("Enter temperature in Celsius: ")
celsius = float(celsius_input)

fahrenheit = (celsius * 1.8) + 32
rounded_fahrenheit = round(fahrenheit, 2)

print(str(celsius) + "°C is equal to " + str(rounded_fahrenheit) + "°F")
```

**Sample Output:**
```
Enter temperature in Celsius: 28.5
28.5°C is equal to 83.3°F
```

---

### Exercise 3: Palindrome String Checker
- **Concepts Covered:** Strings, string methods (`lower()`, `replace()`), string indexing and reverse slicing.
- **Problem Statement:**
  Write a function `is_palindrome(word)` that takes a string, normalizes it (lowercases it and removes spaces), and checks whether it reads the same forward and backward. Return `True` if it is a palindrome and `False` otherwise.

**Starter Code:**
```python
def is_palindrome(text):
    # Your code here
    pass

print(is_palindrome("Radar"))  # Should print True
print(is_palindrome("Python")) # Should print False
```

**Solution:**
```python
def is_palindrome(text):
    # Normalize: lowercase and remove spaces
    cleaned = text.lower().replace(" ", "")
    # In Python, [::-1] reverses any string sequence
    reversed_cleaned = cleaned[::-1]
    return cleaned == reversed_cleaned

print(is_palindrome("Radar"))              # True
print(is_palindrome("Python"))             # False
print(is_palindrome("Never odd or even"))  # True
```

**Sample Output:**
```
True
False
True
```

---

### Exercise 4: Shopping Cart & List Operations
- **Concepts Covered:** Lists, list methods (`append()`, `remove()`, `count()`, `sort()`, `copy()`), `len()`.
- **Problem Statement:**
  Start with a list of grocery items: `["apples", "milk", "bread", "apples", "bananas", "milk"]`.
  1. Print the total count of `"apples"`.
  2. Create a deduplicated copy of the list (remove duplicate `"apples"` and `"milk"`).
  3. Append `"oranges"` and `"eggs"` to the list.
  4. Sort the final list alphabetically and print the sorted cart along with the total item count.

**Starter Code:**
```python
cart = ["apples", "milk", "bread", "apples", "bananas", "milk"]
# 1. Count apples
# 2. Remove duplicates
# 3. Append new items
# 4. Sort and print
```

**Solution:**
```python
cart = ["apples", "milk", "bread", "apples", "bananas", "milk"]

# 1. Count occurrences of "apples"
print("Number of apple occurrences: " + str(cart.count("apples")))

# 2. Work on a copy and remove duplicates
unique_cart = []
for item in cart:
    if item not in unique_cart:
        unique_cart.append(item)

# 3. Add new items
unique_cart.append("oranges")
unique_cart.append("eggs")

# 4. Sort alphabetically
unique_cart.sort()

print("Final shopping cart: " + str(unique_cart))
print("Total unique items to buy: " + str(len(unique_cart)))
```

**Sample Output:**
```
Number of apple occurrences: 2
Final shopping cart: ['apples', 'bananas', 'bread', 'eggs', 'milk', 'oranges']
Total unique items to buy: 6
```

---

### Exercise 5: 2D Coordinate Distance with Tuples
- **Concepts Covered:** Tuples, immutability, `math.sqrt()`, exponent operator `**`.
- **Problem Statement:**
  Coordinates in a game are stored as 2-item tuples: `(x, y)`. Write a function `calculate_distance(point1, point2)` that computes the Euclidean distance between two points:
  $$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$
  Also demonstrate what happens if you attempt to reassign `point1[0] = 100` (catch the `TypeError`).

**Starter Code:**
```python
from math import sqrt

def calculate_distance(point1, point2):
    # Unpack or index tuples, calculate distance
    pass
```

**Solution:**
```python
from math import sqrt

def calculate_distance(point1, point2):
    x1, y1 = point1
    x2, y2 = point2
    distance = sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
    return round(distance, 2)

p1 = (3, 4)
p2 = (7, 1)

print("Distance between points:", calculate_distance(p1, p2))

# Demonstrate tuple immutability
try:
    p1[0] = 100
except TypeError as err:
    print("Caught expected tuple error:", err)
```

**Sample Output:**
```
Distance between points: 5.0
Caught expected tuple error: 'tuple' object does not support item assignment
```

---

### Exercise 6: Bill Splitter with Tip Calculator
- **Concepts Covered:** Functions, multiple parameters, default values, `if/elif/else`, return values.
- **Problem Statement:**
  Write a function `calculate_bill(total, tip_percent, num_people)` that:
  - Adds the tip amount to the subtotal.
  - Divides the final total among `num_people`.
  - If `num_people <= 0`, returns `"Error: Number of people must be at least 1"`.
  - Returns the per-person amount rounded to 2 decimal places.

**Starter Code:**
```python
def calculate_bill(total, tip_percent, num_people=1):
    # Your logic here
    pass
```

**Solution:**
```python
def calculate_bill(total, tip_percent, num_people=1):
    if num_people <= 0:
        return "Error: Number of people must be at least 1"
    
    tip_amount = total * (tip_percent / 100.0)
    grand_total = total + tip_amount
    per_person = grand_total / num_people
    return round(per_person, 2)

print("Individual share (Party of 4, 15% tip on $120):", calculate_bill(120.0, 15, 4))
print("Solo diner (Default 1 person, 20% tip on $50):", calculate_bill(50.0, 20))
print("Invalid party test:", calculate_bill(50.0, 20, 0))
```

**Sample Output:**
```
Individual share (Party of 4, 15% tip on $120): 34.5
Solo diner (Default 1 person, 20% tip on $50): 60.0
Invalid party test: Error: Number of people must be at least 1
```

---

### Exercise 7: Contact Phonebook with Dictionaries
- **Concepts Covered:** Dictionaries, `.get()` method, dictionary lookups, inserting/updating key-value pairs, `in` keyword.
- **Problem Statement:**
  Create a dictionary `phonebook` storing initial names and phone numbers. Write a helper function `lookup_contact(phonebook, name)` that returns the contact's number or `"Contact not found"` if the name doesn't exist. Add a new contact and update an existing contact's number.

**Starter Code:**
```python
phonebook = {
    "Alice": "555-0199",
    "Bob": "555-0142",
    "Charlie": "555-0188"
}
# Write lookup function and update entries
```

**Solution:**
```python
phonebook = {
    "Alice": "555-0199",
    "Bob": "555-0142",
    "Charlie": "555-0188"
}

def lookup_contact(contacts, name):
    # .get() allows specifying a default fallback when key is not present
    return contacts.get(name, "Contact not found")

# Test existing and missing contacts
print("Alice:", lookup_contact(phonebook, "Alice"))
print("David:", lookup_contact(phonebook, "David"))

# Add new contact
phonebook["David"] = "555-0177"
print("David (after adding):", lookup_contact(phonebook, "David"))

# Update an existing contact
phonebook["Alice"] = "555-9999"
print("Alice (after update):", lookup_contact(phonebook, "Alice"))
```

**Sample Output:**
```
Alice: 555-0199
David: Contact not found
David (after adding): 555-0177
Alice (after update): 555-9999
```

---

### Exercise 8: Number Guessing Game
- **Concepts Covered:** While loops, `input()`, conditionals (`if/elif/else`), `break`, loop counters.
- **Problem Statement:**
  Write a number guessing script. Pick a secret number (e.g. `7`). Give the user up to 3 attempts to guess the number.
  - If the user guesses correctly, print `"You won!"` and break out of the loop.
  - If the guess is wrong, inform them if the guess was too high or too low.
  - If they exhaust all 3 guesses, print `"Game Over! The number was X"`.

**Starter Code:**
```python
secret_number = 7
guess_count = 0
guess_limit = 3

while guess_count < guess_limit:
    # Get user guess and compare
    pass
```

**Solution:**
```python
secret_number = 7
guess_count = 0
guess_limit = 3
out_of_guesses = False

while guess_count < guess_limit:
    guess = int(input("Guess a number (1-10): "))
    guess_count += 1
    
    if guess == secret_number:
        print("Congratulations! You guessed it in " + str(guess_count) + " tries!")
        break
    elif guess < secret_number:
        print("Too low!")
    else:
        print("Too high!")
else:
    print("Out of guesses! The secret number was " + str(secret_number))
```

**Sample Output:**
```
Guess a number (1-10): 3
Too low!
Guess a number (1-10): 9
Too high!
Guess a number (1-10): 7
Congratulations! You guessed it in 3 tries!
```

---

### Exercise 9: FizzBuzz with `range()`
- **Concepts Covered:** For loops, `range()`, modulo operator (`%`), `if/elif/else` precedence.
- **Problem Statement:**
  Loop through numbers from 1 to 20 (inclusive) using `range()`.
  - For multiples of 3, print `"Fizz"`.
  - For multiples of 5, print `"Buzz"`.
  - For numbers that are multiples of both 3 and 5, print `"FizzBuzz"`.
  - Otherwise, print the number itself.

**Starter Code:**
```python
for num in range(1, 21):
    # Your condition logic here
    pass
```

**Solution:**
```python
for num in range(1, 21):
    # Check 15 first because both 3 and 5 must match
    if num % 3 == 0 and num % 5 == 0:
        print("FizzBuzz")
    elif num % 3 == 0:
        print("Fizz")
    elif num % 5 == 0:
        print("Buzz")
    else:
        print(num)
```

**Sample Output:**
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
Fizz
19
Buzz
```

---

### Exercise 10: 2D Matrix Sum and Row Counter
- **Concepts Covered:** 2D lists (nested lists), nested `for` loops, accumulator variables.
- **Problem Statement:**
  Given a 2D list of numbers representing a matrix:
  ```python
  matrix = [
      [10, 20, 30],
      [40, 50, 60],
      [70, 80, 90]
  ]
  ```
  Write a program that uses nested loops to:
  1. Print the sum of each individual row.
  2. Compute and print the grand total of all numbers in the matrix.

**Starter Code:**
```python
matrix = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]
# Nested loops to compute row totals and matrix total
```

**Solution:**
```python
matrix = [
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
]

grand_total = 0
row_index = 1

for row in matrix:
    row_sum = 0
    for val in row:
        row_sum += val
        grand_total += val
    print("Row " + str(row_index) + " sum: " + str(row_sum))
    row_index += 1

print("Grand total of matrix:", grand_total)
```

**Sample Output:**
```
Row 1 sum: 60
Row 2 sum: 150
Row 3 sum: 240
Grand total of matrix: 450
```

---

### Exercise 11: Robust Safe Division Calculator
- **Concepts Covered:** `try...except`, specific exceptions (`ZeroDivisionError`, `ValueError`), input casting.
- **Problem Statement:**
  Write a function `safe_divide()` that prompts the user for a numerator and a denominator. Use a `try...except` block to gracefully handle:
  - Non-numeric inputs (`ValueError`)
  - Division by zero (`ZeroDivisionError`)
  - Return the division result when valid.

**Starter Code:**
```python
def safe_divide():
    try:
        # Prompt user, convert, divide
        pass
    except ZeroDivisionError:
        pass
    except ValueError:
        pass
```

**Solution:**
```python
def safe_divide():
    try:
        raw_num = input("Enter numerator: ")
        raw_den = input("Enter denominator: ")
        
        num = float(raw_num)
        den = float(raw_den)
        
        result = num / den
        return "Result: " + str(round(result, 3))
    except ZeroDivisionError:
        return "Error: Cannot divide by zero!"
    except ValueError:
        return "Error: Please enter valid numbers only!"

# Run example
print(safe_divide())
```

**Sample Output:**
```
Enter numerator: 10
Enter denominator: 0
Error: Cannot divide by zero!
```

---

### Exercise 12: Bank Account Class with SavingsAccount Inheritance
- **Concepts Covered:** Object-oriented programming, `class`, `__init__`, `self`, instance methods, subclass inheritance, method overriding.
- **Problem Statement:**
  1. Create a `BankAccount` class with attributes `account_holder` and `balance` (default 0.0). Provide methods `deposit(amount)`, `withdraw(amount)`, and `get_balance()`. Guard against withdrawing more money than available.
  2. Create a subclass `SavingsAccount` that inherits from `BankAccount` and adds an `interest_rate` attribute. Add an `apply_interest()` method that calculates and deposits interest into the balance.

**Starter Code:**
```python
class BankAccount:
    def __init__(self, account_holder, initial_balance=0.0):
        # Your constructor code
        pass

class SavingsAccount(BankAccount):
    def __init__(self, account_holder, initial_balance=0.0, interest_rate=0.05):
        # Inherit and add interest rate
        pass
```

**Solution:**
```python
class BankAccount:
    def __init__(self, account_holder, balance=0.0):
        self.account_holder = account_holder
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print("Deposited $" + str(amount) + ". New balance: $" + str(self.balance))
        else:
            print("Deposit amount must be positive.")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Declined: Insufficient funds! Current balance: $" + str(self.balance))
        elif amount <= 0:
            print("Withdrawal amount must be positive.")
        else:
            self.balance -= amount
            print("Withdrew $" + str(amount) + ". Remaining balance: $" + str(self.balance))

    def get_balance(self):
        return self.balance


class SavingsAccount(BankAccount):
    def __init__(self, account_holder, balance=0.0, interest_rate=0.05):
        # Initialize parent attributes
        super().__init__(account_holder, balance)
        self.interest_rate = interest_rate

    def apply_interest(self):
        interest = self.balance * self.interest_rate
        self.deposit(interest)
        print("Interest of $" + str(interest) + " applied at " + str(self.interest_rate * 100) + "% rate.")


# Demonstration:
account = SavingsAccount("Pushkar", 1000.0, 0.04)
account.deposit(500.0)
account.withdraw(200.0)
account.withdraw(2000.0)  # Insufficient funds
account.apply_interest()  # 4% on $1300 = $52
print("Final Balance:", account.get_balance())
```

**Sample Output:**
```
Deposited $500.0. New balance: $1500.0
Withdrew $200.0. Remaining balance: $1300.0
Declined: Insufficient funds! Current balance: $1300.0
Deposited $52.0. New balance: $1352.0
Interest of $52.0 applied at 4.0% rate.
Final Balance: 1352.0
```

---



