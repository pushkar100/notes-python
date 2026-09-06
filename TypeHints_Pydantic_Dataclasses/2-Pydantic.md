# Pydantic Crash Course - Build Reliable Python & AI Applications

**Based on the Tutorial by Dave Ebbelaar (Data Lumina)**

- [1. Introduction](#1-introduction)
  - [The problem with Python](#the-problem-with-python)
  - [When things go wrong](#when-things-go-wrong)
  - [The real-world impact](#the-real-world-impact)
  - [Mental Model: The Data Bouncer](#mental-model-the-data-bouncer)
  - [Feature Comparison](#feature-comparison)
  - [Static vs Runtime Validation](#static-vs-runtime-validation)
  - [What Pydantic does](#what-pydantic-does)
  - [Pydantic in the Python ecosystem](#pydantic-in-the-python-ecosystem)
  - [Installation](#installation)
  - [Why learn Pydantic](#why-learn-pydantic)
  - [Learn more](#learn-more)
- [2. Type Hints](#2-type-hints)
  - [What are type hints?](#what-are-type-hints)
  - [Mental Model: Sticky Notes on Boxes](#mental-model-sticky-notes-on-boxes)
  - [Python does not enforce type hints](#python-does-not-enforce-type-hints)
  - [Benefits of type hints](#benefits-of-type-hints)
  - [IDE Autocomplete Breakdown](#ide-autocomplete-breakdown)
  - [Basic primitive types](#basic-primitive-types)
  - [Container types](#container-types)
  - [Union types](#union-types)
  - [Optional values](#optional-values)
  - [Literal types](#literal-types)
  - [Any type](#any-type)
  - [Function type hints](#function-type-hints)
  - [Static type checking with MyPy](#static-type-checking-with-mypy)
  - [Common type hint patterns](#common-type-hint-patterns)
  - [Type hints don't validate at runtime](#type-hints-dont-validate-at-runtime)
  - [Learn more](#learn-more)
- [3. Your First Model](#3-your-first-model)
  - [What is a model?](#what-is-a-model)
  - [Anatomy of a Pydantic Model](#anatomy-of-a-pydantic-model)
  - [Dataclasses vs Pydantic](#dataclasses-vs-pydantic)
  - [Creating instances](#creating-instances)
  - [Validation in action](#validation-in-action)
  - [Catching and Inspecting ValidationError](#catching-and-inspecting-validationerror)
  - [Automatic type coercion](#automatic-type-coercion)
  - [Required vs optional fields](#required-vs-optional-fields)
  - [Converting models to dictionaries and JSON](#converting-models-to-dictionaries-and-json)
  - [Serialization & Deserialization Reference](#serialization-deserialization-reference)
  - [Creating models from dictionaries](#creating-models-from-dictionaries)
  - [Creating models directly from JSON strings](#creating-models-directly-from-json-strings)
  - [Models as type hints](#models-as-type-hints)
  - [Real-world example: Weather API Response Parser](#real-world-example-weather-api-response-parser)
  - [Common mistakes](#common-mistakes)
  - [Strict mode](#strict-mode)
  - [Learn more](#learn-more)
- [4. Validation and Fields](#4-validation-and-fields)
  - [Beyond basic type checking](#beyond-basic-type-checking)
  - [The Field function](#the-field-function)
  - [Field Constraints Reference](#field-constraints-reference)
  - [String constraints](#string-constraints)
  - [Numeric constraints](#numeric-constraints)
  - [Default values with Field](#default-values-with-field)
  - [Dynamic Defaults with `defaultfactory`](#dynamic-defaults-with-default_factory)
  - [Field Aliases](#field-aliases)
  - [Field descriptions](#field-descriptions)
  - [Custom validators](#custom-validators)
  - [Specialized Pydantic Types](#specialized-pydantic-types)
  - [Real-world example: Payment Form Validator](#real-world-example-payment-form-validator)
  - [JSON Schema generation](#json-schema-generation)
  - [Learn more](#learn-more)
- [5. Nested Models](#5-nested-models)
  - [Real-world data is nested](#real-world-data-is-nested)
  - [Mental Model: Building Blocks](#mental-model-building-blocks)
  - [Models inside models](#models-inside-models)
  - [Creating from nested dictionaries](#creating-from-nested-dictionaries)
  - [Lists of models](#lists-of-models)
  - [Optional nested models](#optional-nested-models)
  - [Deep nesting](#deep-nesting)
  - [Exporting nested models](#exporting-nested-models)
  - [Selective Export (`include` and `exclude`)](#selective-export-include-and-exclude)
  - [Self-referencing models](#self-referencing-models)
  - [Learn more](#learn-more)
- [6. Pydantic Settings](#6-pydantic-settings)
  - [The problem with environment variables](#the-problem-with-environment-variables)
  - [Installation](#installation)
  - [Your first settings class](#your-first-settings-class)
  - [How field mapping works](#how-field-mapping-works)
  - [Automatic type conversion](#automatic-type-conversion)
  - [Loading from .env files](#loading-from-env-files)
  - [Environment variable prefix](#environment-variable-prefix)
  - [Handling secrets securely with `SecretStr`](#handling-secrets-securely-with-secretstr)
  - [Real-world example: Production Application Settings](#real-world-example-production-application-settings)
  - [Singleton settings instance pattern](#singleton-settings-instance-pattern)
  - [Learn more](#learn-more)
- [7. Structured LLM Output](#7-structured-llm-output)
  - [The problem with LLM responses](#the-problem-with-llm-responses)
  - [Mental Model: The Mold / Stencil](#mental-model-the-mold-stencil)
  - [OpenAI Integration with Pydantic](#openai-integration-with-pydantic)
  - [Adding Field Descriptions for LLM Context](#adding-field-descriptions-for-llm-context)
  - [Enforcing Choices using `Literal`](#enforcing-choices-using-literal)
  - [Generic Validation for Any LLM Provider](#generic-validation-for-any-llm-provider)
  - [Handling LLM Extraction Failures with Retries](#handling-llm-extraction-failures-with-retries)
  - [Real-world example: Invoice Data Extraction Agent](#real-world-example-invoice-data-extraction-agent)
  - [Learn more](#learn-more)
- [8. Summary](#8-summary)
  - [Core Learnings Overview](#core-learnings-overview)
  - [Pydantic Cheat Sheet](#pydantic-cheat-sheet)
  - [Best Practices Checklist](#best-practices-checklist)
  - [Resources](#resources)

---

## 1. Introduction

Pydantic brings runtime data validation to Python using type hints.

### The problem with Python

Python is dynamically typed. This means a variable can hold any type of data and can change types at any time:

```python
age = 25
age = "twenty-five"
age = ["25", 25, None]
```

Python executes this code without throwing errors.

This flexibility is helpful for quick, small scripts. But it causes serious bugs in production applications when working with external data.

### When things go wrong

Imagine building an API endpoint that receives user data:

```python
def create_user(data):
    user_id = data["id"]
    email = data["email"]
    age = data["age"]

    # Later in your business logic...
    birth_year = 2025 - age  # What if age is "25" instead of 25?
```

Your API expects clean JSON:

```json
{ "id": 1, "email": "dave@example.com", "age": 25 }
```

External clients or web forms might send malformed JSON:

```json
{ "id": 1, "email": null, "age": "unknown" }
```

Your code crashes with a `TypeError` deep inside your business logic.

### The real-world impact

In production applications, data enters from unpredictable sources:

- **API responses**: External services return unexpected schemas or missing fields
- **User input**: Web forms and mobile apps submit invalid string formats
- **Configuration**: Environment variables are always loaded as strings
- **Database records**: Legacy records contain null or unexpected fields
- **AI Models**: LLMs return unstructured text that may not match your expectations

Without validation, bugs stay hidden until production. With Pydantic, invalid data is caught immediately at the boundary of your application.

### Mental Model: The Data Bouncer

Think of Pydantic as a bouncer at the door of your application.

Without Pydantic, raw external data enters your system unchecked. It travels through your functions until it hits a line of math or string operation and crashes your program.

With Pydantic, every piece of incoming data must present its credentials at the application boundary. If the data is valid, Pydantic parses and types it cleanly. If the data is invalid, the bouncer rejects it immediately at line 1 with a detailed error report.

### Feature Comparison

| Feature                        | Plain Python Dict   | `@dataclass`           | Pydantic `BaseModel`                 |
| :----------------------------- | :------------------ | :--------------------- | :----------------------------------- |
| **Defines Data Structure**     | No (Freeform keys)  | Yes (Type annotations) | Yes (Type annotations)               |
| **Runtime Validation**         | None                | None                   | **Strict & Lax Validation**          |
| **Automatic Coercion**         | None                | None                   | **Yes** (`"25"` -> `25`)             |
| **Dictionary/JSON Conversion** | Manual `json.dumps` | Manual `asdict()`      | **Built-in** (`model_dump()`)        |
| **IDE Autocomplete**           | No (String keys)    | Yes (Attributes)       | **Yes (Attributes)**                 |
| **JSON Schema Generation**     | No                  | No                     | **Built-in** (`model_json_schema()`) |

### Static vs Runtime Validation

It is important to understand the difference between static type checking and runtime validation.

- **Static Type Checkers (mypy, IDEs)**: Read your source code before it runs. They check if your written code matches your type annotations. They cannot inspect real runtime values coming from an external API call.
- **Runtime Validation (Pydantic)**: Executes while your program is running. It inspects real incoming values (like JSON payloads or environment variables) and enforces rules live.

### What Pydantic does

Pydantic validates data at runtime. You define what your data should look like, and Pydantic ensures incoming data matches that contract:

```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    email: str
    age: int

# Valid data - works fine
user = User(id=1, email="dave@example.com", age=25)
print(user.age)  # 25

# Invalid data - fails immediately with clear error
user = User(id=1, email=None, age="unknown")
```

When validation fails, Pydantic raises a `ValidationError` with clear error messages:

```
2 validation errors for User
email
  Input should be a valid string
age
  Input should be a valid integer, unable to parse string as an integer
```

The problem is caught at the source before any business logic executes.

### Pydantic in the Python ecosystem

Pydantic is standard in modern Python development:

- **FastAPI** uses Pydantic for request and response validation
- **Django Ninja** uses Pydantic for API schemas
- **SQLModel** combines Pydantic with SQLAlchemy for database ORM models
- **OpenAI and LangChain** use Pydantic for structured LLM tool outputs

### Installation

Install Pydantic in your project using `pip` or `uv`:

```bash
pip install pydantic
```

```bash
uv add pydantic
```

### Why learn Pydantic

- **Build robust applications**: Catch data bugs at the application boundary before they reach your database or background jobs.
- **Improved developer experience**: Type hints enable instant IDE autocomplete, line error highlights, and refactoring tools.
- **Essential for AI development**: AI agents require structured outputs. Pydantic models define what the AI should return, making responses predictable and type-safe.

### Learn more

- [Official Pydantic documentation](https://docs.pydantic.dev/latest/)
- [Pydantic on GitHub](https://github.com/pydantic/pydantic)

---

## 2. Type Hints

The foundation Pydantic builds on.

### What are type hints?

Type hints specify what data type a variable, function parameter, or return value should hold:

```python
name: str = "Dave"
age: int = 30
price: float = 19.99
is_active: bool = True
```

The `: str`, `: int`, `: float`, and `: bool` annotations are type hints.

### Mental Model: Sticky Notes on Boxes

Think of Python variables as storage boxes. Type hints are like sticky notes written on the outside of each box.

When Python runs `age: int = "twenty"`, it carries the box without opening it to check inside. The sticky note says `int`, but the box contains a string `"twenty"`. Standard Python does not check if the sticky note matches the content inside.

External tools like IDEs, `mypy`, and Pydantic read the sticky notes to help you enforce safety.

### Python does not enforce type hints

Standard Python ignores type hints at runtime. They are metadata:

```python
age: int = "not a number"  # Python allows this without error
```

Python executes this code without throwing an exception.

### Benefits of type hints

1. **Documentation**: Code becomes self-explaining without needing extra docstrings for basic data types.
2. **IDE Support**: Code editors provide accurate autocomplete, syntax highlighting, and inline refactoring.
3. **Static & Runtime Tools**: Tools like `mypy` and `pydantic` use type hints to catch bugs automatically.

Without type hints:

```python
def create_user(name, email, age):
    # What types are these arguments supposed to be?
    # What data type does this function return?
    pass
```

With type hints:

```python
def create_user(name: str, email: str, age: int) -> dict:
    # Parameter types and return type are explicit
    pass
```

### IDE Autocomplete Breakdown

Without type hints, IDEs cannot inspect dynamic objects:

```python
def process_user_dict(user):
    # IDE cannot autocomplete dictionary keys.
    # Typos like user["emial"] cause runtime KeyErrors!
    return user["email"].lower()
```

With type hints and objects:

```python
class User:
    def __init__(self, name: str, email: str):
        self.name = name
        self.email = email

def process_user_object(user: User) -> str:
    # Typing 'user.' triggers autocomplete for 'name' and 'email'
    return user.email.lower()
```

### Basic primitive types

The four basic primitive types in Python:

```python
# Strings (text data)
name: str = "Alice"
message: str = "Hello, world!"

# Integers (whole numbers)
count: int = 42
user_id: int = 1001

# Floats (decimal numbers)
price: float = 29.99
temperature: float = 98.6

# Booleans (True or False)
is_active: bool = True
has_access: bool = False
```

### Container types

For collections of items, specify the container type and the item type inside square brackets `[...]`:

```python
# List of strings
tags: list[str] = ["python", "pydantic", "fastapi"]

# List of integers
quantities: list[int] = [1, 5, 3, 2]

# Dictionary with string keys and integer values
word_counts: dict[str, int] = {"error": 12, "warning": 5}

# Dictionary with string keys and string values
settings: dict[str, str] = {"theme": "dark", "language": "en"}

# Set of unique integers
unique_ids: set[int] = {101, 102, 103}

# Tuple with fixed position types
user_tuple: tuple[int, str, bool] = (1, "Alice", True)

# Variable-length tuple of integers
scores: tuple[int, ...] = (90, 85, 95, 100)
```

Starting in Python 3.9+, use built-in lowercase container names (`list`, `dict`, `set`, `tuple`). Older code uses capitalized imports from `typing` (`List`, `Dict`). Lowercase syntax is preferred.

### Union types

When a variable can hold more than one type, use the `|` pipe operator (Python 3.10+) or `Union` from `typing`:

```python
# Modern Python 3.10+ pipe syntax
value: int | float = 10.5
identifier: int | str = "USER-9921"

# Legacy Python syntax (from typing import Union)
from typing import Union
value_legacy: Union[int, float] = 10.5
```

### Optional values

When a value can be `None`, mark it as optional using `Type | None` or `Optional[Type]`:

```python
from typing import Optional

# Modern Python 3.10+ syntax (Preferred)
middle_name: str | None = None
phone_number: str | None = "+1-555-0123"

# Equivalent using Optional wrapper
legacy_middle_name: Optional[str] = None
```

Always assign `= None` as the default value when a parameter is optional.

### Literal types

Restricts a variable to specific allowed values:

```python
from typing import Literal

status: Literal["draft", "published", "archived"] = "draft"

# Valid assignments
status = "draft"      # OK
status = "published"  # OK

# Type checkers warn about invalid values
status = "pending"    # Error: "pending" is not allowed in Literal
```

Real-world examples:

```python
from typing import Literal

log_level: Literal["debug", "info", "warning", "error"] = "info"
environment: Literal["development", "staging", "production"] = "development"
http_method: Literal["GET", "POST", "PUT", "DELETE"] = "GET"
```

### Any type

The `Any` type disables type checking for a variable:

```python
from typing import Any

# Variable can hold literally any object
raw_payload: Any = {"key": "value"}
raw_payload = 100
raw_payload = [1, 2, 3]
```

Use `Any` sparingly. It removes all type safety and autocomplete benefits.

### Function type hints

Annotate parameters and return values using `->`:

```python
def format_price(amount: float, currency: str = "USD") -> str:
    return f"{currency} {amount:.2f}"

def calculate_total(prices: list[float], tax_rate: float) -> float:
    subtotal = sum(prices)
    return subtotal * (1 + tax_rate)

def get_config(key: str) -> str | None:
    config_store = {"theme": "dark"}
    return config_store.get(key)
```

If a function performs an action and returns nothing, annotate its return type as `None`:

```python
def log_message(message: str) -> None:
    print(f"[LOG]: {message}")
```

### Static type checking with MyPy

To check your type hints before running your script, use `mypy`:

1. Install `mypy`:

```bash
pip install mypy
```

2. Create a file `example.py`:

```python
def add_numbers(a: int, b: int) -> int:
    return a + b

result: int = add_numbers(10, "20")  # Error: passing string "20"
```

3. Run `mypy`:

```bash
mypy example.py
```

Output:

```text
example.py:4: error: Argument 2 to "add_numbers" has incompatible type "str"; expected "int"  [arg-type]
```

### Common type hint patterns

```python
from typing import Literal

# Required string
username: str

# Optional string (defaults to None)
bio: str | None = None

# String with a standard default value
country: str = "USA"

# Empty container initializers
items: list[str] = []
metadata: dict[str, str] = {}

# Restricted choice options
role: Literal["admin", "user", "guest"] = "user"
```

### Type hints don't validate at runtime

Python ignores type hints during execution. This code runs without raising an exception:

```python
age: int = "not a number"
prices: list[float] = "not a list"
```

Standard Python does not validate runtime data. Pydantic bridges this gap by reading your type hints and validating incoming data against them.

### Learn more

- [Python typing documentation](https://docs.python.org/3/library/typing.html)
- [Type hints cheat sheet](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html)

---

## 3. Your First Model

Create validated data structures with BaseModel.

### What is a model?

A Pydantic model is a class that inherits from `BaseModel`. It defines the structure, fields, and types of your data:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int
```

This model defines a contract: "A User must have a string `name`, a string `email`, and an integer `age`."

### Anatomy of a Pydantic Model

```python
from pydantic import BaseModel

class UserProfile(BaseModel):
    # 1. Required field: Must be provided, no default
    username: str

    # 2. Field with default value: Optional to pass when instantiating
    is_active: bool = True

    # 3. Optional field: Can be a string or None
    bio: str | None = None
```

- **Imports**: Import `BaseModel` from `pydantic`.
- **Inheritance**: Inherit your class from `BaseModel`.
- **Fields**: Define attributes with explicit type hints.

### Dataclasses vs Pydantic

Python includes a standard `@dataclass` decorator for creating data container classes:

```python
from dataclasses import dataclass

@dataclass
class UserDataclass:
    name: str
    email: str
    age: int

user = UserDataclass(name="Alice", email="alice@example.com", age="thirty")
print(user.age)  # Prints "thirty" without validation!
```

Dataclasses automatically generate `__init__()` methods, but they do not validate runtime data.

Pydantic models look similar to dataclasses, but enforce types at runtime:

```python
from pydantic import BaseModel

class UserModel(BaseModel):
    name: str
    email: str
    age: int

user = UserModel(name="Alice", email="alice@example.com", age="thirty")
# Raises ValidationError: Input should be a valid integer
```

Use Pydantic when working with external data (APIs, forms, database inputs, environment variables). Use dataclasses for simple internal objects where validation overhead is unnecessary.

### Creating instances

Pass keyword arguments to instantiate a model:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int

user = User(name="Alice", email="alice@example.com", age=30)

print(user.name)   # Alice
print(user.email)  # alice@example.com
print(user.age)    # 30
```

Access fields directly using attribute notation (`user.name`).

### Validation in action

When you pass invalid data, Pydantic raises a `ValidationError` immediately:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int

user = User(name="Alice", email="alice@example.com", age="thirty")
```

Console Error Output:

```text
ValidationError: 1 validation error for User
age
  Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='thirty', input_type=str]
```

### Catching and Inspecting ValidationError

Always handle `ValidationError` at your application boundaries:

```python
from pydantic import BaseModel, ValidationError

class User(BaseModel):
    id: int
    email: str

try:
    user = User(id="invalid_id", email="test@example.com")
except ValidationError as e:
    print("Validation failed!")
    # Print list of error dictionaries
    for error in e.errors():
        print(f"Field: {error['loc'][0]}")
        print(f"Message: {error['msg']}")
        print(f"Type: {error['type']}")
```

Output:

```text
Validation failed!
Field: id
Message: Input should be a valid integer, unable to parse string as an integer
Type: int_parsing
```

### Automatic type coercion

Pydantic uses lax type coercion by default. It automatically converts compatible types into the target type:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
    is_active: bool

# String "25" is converted to int 25
# String "true" is converted to bool True
user = User(name="Alice", age="25", is_active="true")

print(user.age)        # 25 (type: int)
print(user.is_active)  # True (type: bool)
```

Common automatic coercions:

- `"123"` -> `123` (String to int)
- `"19.99"` -> `19.99` (String to float)
- `"true"`, `"1"`, `"yes"` -> `True` (String to bool)
- `1` -> `"1"` (Int to string)

### Required vs optional fields

- **Required fields**: Fields defined without a default value. They must be passed when instantiating the model.
- **Optional fields**: Fields defined with default values or set to `None`.

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str              # Required
    email: str             # Required
    age: int | None = None # Optional (defaults to None)
    role: str = "member"   # Optional (defaults to "member")

# Valid: age and role omitted
user1 = User(name="Alice", email="alice@example.com")
print(user1.age)   # None
print(user1.role)  # member

# Valid: providing all fields
user2 = User(name="Bob", email="bob@example.com", age=28, role="admin")
print(user2.age)   # 28
print(user2.role)  # admin
```

### Converting models to dictionaries and JSON

Pydantic provides methods to serialize models back into dictionaries or JSON strings.

#### `model_dump()`

Converts a model instance into a standard Python dictionary:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int

user = User(name="Alice", email="alice@example.com", age=30)

user_dict = user.model_dump()
print(user_dict)
# Output: {'name': 'Alice', 'email': 'alice@example.com', 'age': 30}
```

#### `model_dump_json()`

Converts a model instance into a formatted JSON string:

```python
json_string = user.model_dump_json()
print(json_string)
# Output: {"name":"Alice","email":"alice@example.com","age":30}
```

### Serialization & Deserialization Reference

| Action          | Source Data    | Method / Syntax                                         | Target Output     |
| :-------------- | :------------- | :------------------------------------------------------ | :---------------- |
| **Instantiate** | Keyword args   | `User(name="Alice", age=30)`                            | Model Instance    |
| **From Dict**   | Dictionary     | `User.model_validate(data_dict)` or `User(**data_dict)` | Model Instance    |
| **From JSON**   | JSON String    | `User.model_validate_json(json_str)`                    | Model Instance    |
| **To Dict**     | Model Instance | `user.model_dump()`                                     | Python Dictionary |
| **To JSON**     | Model Instance | `user.model_dump_json()`                                | JSON String       |

### Creating models from dictionaries

Two ways to create a model instance from dictionary data:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int

data = {"name": "Alice", "email": "alice@example.com", "age": 30}

# Option 1: Unpack dictionary (Standard keyword expansion)
user1 = User(**data)

# Option 2: model_validate() (Recommended for explicit parsing)
user2 = User.model_validate(data)
```

Use `User.model_validate(data)` when receiving dictionary payloads from APIs or database drivers.

### Creating models directly from JSON strings

Use `model_validate_json()` to parse raw JSON strings directly without calling `json.loads()` first:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str
    age: int

json_data = '{"name": "Alice", "email": "alice@example.com", "age": 30}'

# Direct validation from JSON string
user = User.model_validate_json(json_data)
print(user.name)  # Alice
```

### Models as type hints

Pydantic models act as standard type annotations in functions:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    email: str

def format_welcome_email(user: User) -> str:
    # IDE provides autocomplete for user.name and user.email
    return f"To: {user.email}\nSubject: Welcome!\nHello {user.name},"

user = User(name="Alice", email="alice@example.com")
email_text = format_welcome_email(user)
print(email_text)
```

### Real-world example: Weather API Response Parser

```python
from pydantic import BaseModel, ValidationError

class WeatherResponse(BaseModel):
    city: str
    temperature: float
    humidity: int
    description: str

def parse_api_response(raw_json: str) -> WeatherResponse | None:
    try:
        return WeatherResponse.model_validate_json(raw_json)
    except ValidationError as e:
        print(f"Failed to parse weather API response: {e}")
        return None

# Incoming API payload
api_json = '{"city": "Amsterdam", "temperature": 18.5, "humidity": 75, "description": "Cloudy"}'

weather = parse_api_response(api_json)
if weather:
    print(f"City: {weather.city}")
    print(f"Temp: {weather.temperature}°C")
```

### Common mistakes

#### 1. Forgetting Type Hints

```python
# Wrong: Missing type hints on attributes
class User(BaseModel):
    name
    email

# Right: Always include explicit type hints
class User(BaseModel):
    name: str
    email: str
```

#### 2. Mutable Default Values

In plain Python classes, `default=[]` shares a single list instance across all class objects. In Pydantic, `= []` is handled safely and creates a fresh list for every new instance:

```python
from pydantic import BaseModel

class User(BaseModel):
    tags: list[str] = []  # Safe in Pydantic

user1 = User()
user2 = User()
user1.tags.append("python")

print(user1.tags)  # ['python']
print(user2.tags)  # [] (user2 is not affected)
```

### Strict mode

If you want to disable automatic type coercion and require exact data types, enable `strict=True` using `ConfigDict`:

```python
from pydantic import BaseModel, ConfigDict, ValidationError

class StrictUser(BaseModel):
    model_config = ConfigDict(strict=True)

    name: str
    age: int

# Fails in strict mode because age is passed as a string "25"
try:
    user = StrictUser(name="Alice", age="25")
except ValidationError as e:
    print("Strict validation rejected string age!")
```

`model_config` is a reserved attribute name that Pydantic looks for to configure model settings.

### Learn more

- [Models documentation](https://docs.pydantic.dev/latest/concepts/models/)

---

## 4. Validation and Fields

Control what data is acceptable using `Field` and custom validators.

### Beyond basic type checking

Validating data types is often not enough. Business rules require specific constraints:

- Email addresses must follow a valid format
- User age must be positive (e.g., between 18 and 120)
- Usernames must be between 3 and 20 characters
- Product prices cannot be negative

Pydantic provides the `Field()` function to define detailed field constraints.

### The Field function

Import `Field` from `pydantic` to assign constraints:

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(min_length=1, max_length=100)
    age: int = Field(gt=0, le=120)
    email: str

user = User(name="Alice", age=30, email="alice@example.com")
```

If `age` is set to `-5` or `name` is set to `""`, Pydantic raises a `ValidationError`.

### Field Constraints Reference

| Constraint        | Applicable Types      | Description                                 | Example                        |
| :---------------- | :-------------------- | :------------------------------------------ | :----------------------------- |
| `min_length`      | `str`, `list`, `dict` | Minimum number of characters or items       | `Field(min_length=3)`          |
| `max_length`      | `str`, `list`, `dict` | Maximum number of characters or items       | `Field(max_length=50)`         |
| `pattern`         | `str`                 | Regular expression string match             | `Field(pattern=r"^\d{5}$")`    |
| `gt`              | `int`, `float`        | Greater than                                | `Field(gt=0)`                  |
| `ge`              | `int`, `float`        | Greater than or equal to                    | `Field(ge=18)`                 |
| `lt`              | `int`, `float`        | Less than                                   | `Field(lt=100)`                |
| `le`              | `int`, `float`        | Less than or equal to                       | `Field(le=100)`                |
| `multiple_of`     | `int`, `float`        | Value must be a multiple of number          | `Field(multiple_of=5)`         |
| `default`         | Any                   | Set a static default value                  | `Field(default="active")`      |
| `default_factory` | Any                   | Callable function to generate default value | `Field(default_factory=list)`  |
| `description`     | Any                   | Text documentation for JSON Schema          | `Field(description="User ID")` |
| `alias`           | Any                   | Map incoming JSON key name                  | `Field(alias="user_id")`       |

### String constraints

Control string length and pattern matching:

```python
from pydantic import BaseModel, Field

class UserProfile(BaseModel):
    username: str = Field(min_length=3, max_length=20)
    bio: str = Field(max_length=500)
    website: str = Field(pattern=r"^https?://.*")

# Valid profile
profile = UserProfile(
    username="alice_dev",
    bio="Python developer",
    website="https://example.com"
)
```

Common string constraints:

- `min_length`: Minimum string character count
- `max_length`: Maximum string character count
- `pattern`: Regex pattern matching

### Numeric constraints

Control number boundaries:

```python
from pydantic import BaseModel, Field

class Product(BaseModel):
    name: str
    price: float = Field(gt=0)           # Must be greater than 0
    quantity: int = Field(ge=0)          # Greater than or equal to 0
    discount: float = Field(ge=0, le=1)  # Between 0.0 and 1.0
```

### Default values with Field

Assign default values alongside field validation rules:

```python
from pydantic import BaseModel, Field

class APIConfig(BaseModel):
    api_key: str
    model: str = Field(default="gpt-4")
    max_tokens: int = Field(default=1000, ge=1, le=4096)
    temperature: float = Field(default=0.7, ge=0.0, le=2.0)

# Instantiated using defaults
config = APIConfig(api_key="sk-test123")
print(config.model)       # gpt-4
print(config.max_tokens)  # 1000
```

### Dynamic Defaults with `default_factory`

Use `default_factory` when a default value must be calculated dynamically every time a new instance is created (such as current timestamps or new list instances):

```python
from datetime import datetime
from pydantic import BaseModel, Field

class LogEntry(BaseModel):
    message: str
    # Evaluated dynamically for every instance
    timestamp: datetime = Field(default_factory=datetime.now)
    tags: list[str] = Field(default_factory=list)

log1 = LogEntry(message="System started")
log2 = LogEntry(message="User logged in")

# Each log gets its own unique timestamp and list
print(log1.timestamp)
print(log2.timestamp)
```

Do not write `default=datetime.now()`. That evaluates `datetime.now()` once when the module loads, freezing the timestamp for all future models. Always use `default_factory=datetime.now`.

### Field Aliases

External APIs often use camelCase (`userId`, `createdAt`), while Python uses snake_case (`user_id`, `created_at`). Use `alias` and `populate_by_name` to handle conversion:

```python
from pydantic import BaseModel, ConfigDict, Field

class UserResponse(BaseModel):
    model_config = ConfigDict(populate_by_name=True)

    user_id: int = Field(alias="userId")
    first_name: str = Field(alias="firstName")

# Incoming external JSON payload with camelCase
incoming_data = {"userId": 101, "firstName": "Alice"}

# Validates using camelCase alias
user = UserResponse.model_validate(incoming_data)
print(user.user_id)     # 101
print(user.first_name)  # Alice

# Internal Python keyword instantiation still works due to populate_by_name=True
user2 = UserResponse(user_id=102, first_name="Bob")
```

### Field descriptions

Add human-readable descriptions for documentation and schema generation:

```python
from pydantic import BaseModel, Field

class Order(BaseModel):
    order_id: str = Field(description="Unique UUID order identifier")
    total: float = Field(gt=0, description="Total order amount in USD")
```

### Custom validators

When built-in constraints are insufficient, write custom validators using `@field_validator` or `@model_validator`.

#### `@field_validator` (Single Field Validation)

Validate or transform a specific field:

```python
from pydantic import BaseModel, field_validator

class User(BaseModel):
    username: str

    @field_validator("username")
    def validate_username(cls, value: str) -> str:
        if " " in value:
            raise ValueError("Username cannot contain spaces")
        return value.lower()  # Normalize input to lowercase

user = User(username="AliceSmith")
print(user.username)  # alicesmith
```

Custom validators receive `cls` (the model class) and `value` (the field value). Return the cleaned value or raise `ValueError`.

#### `@model_validator` (Cross-Field Validation)

Use `@model_validator(mode="after")` to validate dependencies between multiple fields:

```python
from pydantic import BaseModel, model_validator

class SignupForm(BaseModel):
    password: str
    confirm_password: str

    @model_validator(mode="after")
    def check_passwords_match(self) -> "SignupForm":
        if self.password != self.confirm_password:
            raise ValueError("Passwords do not match")
        return self

# Raises ValidationError because passwords differ
form = SignupForm(password="secret123", confirm_password="different_pass")
```

### Specialized Pydantic Types

Pydantic includes built-in specialized types for standard data formats:

```python
from pydantic import BaseModel, EmailStr, HttpUrl

class UserContact(BaseModel):
    email: EmailStr  # Validates email format automatically
    website: HttpUrl # Validates URL structure (requires http/https scheme)

contact = UserContact(
    email="alice@example.com",
    website="https://example.com"
)
```

Note: `EmailStr` requires installing the `email-validator` package (`pip install email-validator`).

### Real-world example: Payment Form Validator

```python
from pydantic import BaseModel, Field, EmailStr

class PaymentForm(BaseModel):
    email: EmailStr
    card_number: str = Field(min_length=16, max_length=16, pattern=r"^\d{16}$")
    expiry_month: int = Field(ge=1, le=12)
    expiry_year: int = Field(ge=2025, le=2035)
    cvv: str = Field(pattern=r"^\d{3,4}$")
    amount: float = Field(gt=0)

payment = PaymentForm(
    email="customer@example.com",
    card_number="1234567890123456",
    expiry_month=12,
    expiry_year=2026,
    cvv="888",
    amount=149.99
)
print(f"Processing ${payment.amount} for {payment.email}")
```

### JSON Schema generation

Pydantic automatically generates standard JSON Schema from your models using `model_json_schema()`:

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(min_length=1, description="Full name")
    age: int = Field(ge=0, description="Age in years")

print(User.model_json_schema())
```

Frameworks like FastAPI use `model_json_schema()` to generate OpenAPI documentation automatically.

### Learn more

- [Fields documentation](https://docs.pydantic.dev/latest/concepts/fields/)
- [Validators documentation](https://docs.pydantic.dev/latest/concepts/validators/)

---

## 5. Nested Models

Handle complex and hierarchical data structures.

### Real-world data is nested

Production data is rarely flat. Orders contain items, user profiles contain addresses, and invoices contain line item breakdown summaries.

### Mental Model: Building Blocks

Think of Pydantic models as custom LEGO building blocks. Once you define a smaller building block (like `Address` or `OrderItem`), you can use it as a field type inside larger building blocks (like `User` or `Order`).

### Models inside models

Define smaller models and use them as field types in container models:

```python
from pydantic import BaseModel

class OrderItem(BaseModel):
    product_id: str
    name: str
    quantity: int
    price: float

class Order(BaseModel):
    order_id: str
    item: OrderItem  # Nested model

order = Order(
    order_id="ORD-001",
    item=OrderItem(
        product_id="P100",
        name="Wireless Mouse",
        quantity=2,
        price=29.99
    )
)

print(order.item.name)  # Wireless Mouse
```

### Creating from nested dictionaries

When you pass nested dictionaries to `model_validate()`, Pydantic parses and validates every level recursively:

```python
from pydantic import BaseModel

class OrderItem(BaseModel):
    product_id: str
    name: str
    quantity: int
    price: float

class Order(BaseModel):
    order_id: str
    item: OrderItem

# Nested dictionary from API payload
data = {
    "order_id": "ORD-001",
    "item": {
        "product_id": "P100",
        "name": "Wireless Mouse",
        "quantity": 2,
        "price": 29.99
    }
}

order = Order.model_validate(data)
print(type(order.item))  # <class 'OrderItem'>
print(order.item.price)  # 29.99
```

Pydantic automatically converts the nested dictionary into an `OrderItem` model instance.

### Lists of models

Handle collections of nested objects using `list[Model]`:

```python
from pydantic import BaseModel

class OrderItem(BaseModel):
    product_id: str
    name: str
    quantity: int
    price: float

class Order(BaseModel):
    order_id: str
    customer_email: str
    items: list[OrderItem]  # List of nested models

order_data = {
    "order_id": "ORD-500",
    "customer_email": "customer@example.com",
    "items": [
        {"product_id": "P1", "name": "Keyboard", "quantity": 1, "price": 89.99},
        {"product_id": "P2", "name": "Monitor", "quantity": 2, "price": 199.99}
    ]
}

order = Order.model_validate(order_data)

for item in order.items:
    print(f"Item: {item.name} | Total: ${item.quantity * item.price}")
```

### Optional nested models

Make nested models optional using `Model | None = None`:

```python
from pydantic import BaseModel

class Discount(BaseModel):
    code: str
    percent: float

class Order(BaseModel):
    order_id: str
    total: float
    discount: Discount | None = None

# Order without discount
order1 = Order(order_id="ORD-01", total=50.00)
print(order1.discount)  # None

# Order with discount
order2 = Order(
    order_id="ORD-02",
    total=50.00,
    discount={"code": "SUMMER20", "percent": 20.0}
)
print(order2.discount.code)  # SUMMER20
```

### Deep nesting

Models can be nested to any depth:

```python
from pydantic import BaseModel

class Address(BaseModel):
    street: str
    city: str
    country: str

class Customer(BaseModel):
    name: str
    email: str
    address: Address

class OrderItem(BaseModel):
    name: str
    price: float

class Order(BaseModel):
    order_id: str
    customer: Customer
    items: list[OrderItem]

data = {
    "order_id": "ORD-999",
    "customer": {
        "name": "Alice",
        "email": "alice@example.com",
        "address": {
            "street": "123 Main St",
            "city": "Amsterdam",
            "country": "Netherlands"
        }
    },
    "items": [
        {"name": "Laptop Stand", "price": 49.99}
    ]
}

order = Order.model_validate(data)
print(order.customer.address.city)  # Amsterdam
```

### Exporting nested models

Calling `model_dump()` converts the entire nested model tree back into standard nested dictionaries:

```python
dict_data = order.model_dump()
print(dict_data["customer"]["address"]["city"])  # Amsterdam
```

### Selective Export (`include` and `exclude`)

Filter specific fields during serialization using `include` or `exclude`:

```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    username: str
    password_hash: str

user = User(id=1, username="alice", password_hash="secret_hash_value")

# Exclude sensitive fields from output dict
public_data = user.model_dump(exclude={"password_hash"})
print(public_data)  # {'id': 1, 'username': 'alice'}
```

### Self-referencing models

To create recursive structures like tree nodes or comment threads, import `annotations` from `__future__`:

```python
from __future__ import annotations
from pydantic import BaseModel

class Comment(BaseModel):
    author: str
    text: str
    replies: list[Comment] = []

comment = Comment(
    author="Alice",
    text="Great tutorial!",
    replies=[
        Comment(author="Bob", text="Agreed!")
    ]
)
print(comment.replies[0].author)  # Bob
```

### Learn more

- [Nested models documentation](https://docs.pydantic.dev/latest/concepts/models/#nested-models)

---

## 6. Pydantic Settings

Type-safe application configuration from environment variables.

### The problem with environment variables

In standard Python, `os.environ` loads environment variables as raw strings:

```python
import os

api_key = os.getenv("API_KEY")                 # str | None
max_connections = os.getenv("MAX_CONNECTIONS") # Loaded as str "100", not int 100!
debug_mode = os.getenv("DEBUG")                # Loaded as str "True", not bool True!
```

Manual configuration handling requires writing repetitive code to:

- Check if mandatory environment variables are set
- Cast string values to `int`, `float`, or `bool`
- Handle fallback default values
- Mask secret tokens in log files

`pydantic-settings` automates environment variable parsing into validated Python objects.

### Installation

`pydantic-settings` is a separate package:

```bash
pip install pydantic-settings
```

```bash
uv add pydantic-settings
```

### Your first settings class

Inherit from `BaseSettings` instead of `BaseModel`:

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    api_key: str
    max_connections: int = 100
    debug: bool = False

# Automatically reads from environment variables
settings = Settings()

print(settings.api_key)         # Reads API_KEY environment variable
print(settings.max_connections) # Reads MAX_CONNECTIONS or defaults to 100
```

Set environment variables in your terminal shell:

```bash
export API_KEY="sk-prod-99201"
export MAX_CONNECTIONS="250"
export DEBUG="true"
```

When `Settings()` is instantiated, Pydantic reads environment variables matching field names in uppercase.

### How field mapping works

| Settings Field    | Default Environment Variable |
| :---------------- | :--------------------------- |
| `api_key`         | `API_KEY`                    |
| `max_connections` | `MAX_CONNECTIONS`            |
| `database_url`    | `DATABASE_URL`               |

### Automatic type conversion

Pydantic Settings converts string environment variables into target Python types:

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    port: int                 # "8080" -> 8080
    debug: bool               # "true" -> True
    rate_limit: float         # "1.5" -> 1.5
    allowed_hosts: list[str]  # "localhost,127.0.0.1" -> ["localhost", "127.0.0.1"]
```

Accepted boolean values in environment variables:

- `True`: `"true"`, `"1"`, `"yes"`, `"on"`
- `False`: `"false"`, `"0"`, `"no"`, `"off"`

### Loading from .env files

Store local configuration variables in a `.env` file in your project root:

```text
# .env file content
API_KEY=sk-local-key-123
DATABASE_URL=postgresql://user:pass@localhost:5432/appdb
DEBUG=true
MAX_CONNECTIONS=50
```

Configure `SettingsConfigDict` to load the `.env` file automatically:

```python
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env", env_file_encoding="utf-8")

    api_key: str
    database_url: str
    debug: bool = False
    max_connections: int = 100

settings = Settings()
print(settings.api_key)  # sk-local-key-123
```

Environment variable lookup priority:

1. Environment variables set directly in the OS shell (Highest priority)
2. Variables loaded from `.env` file
3. Default values defined in the `BaseSettings` class (Lowest priority)

### Environment variable prefix

Prevent configuration name collisions with other tools by adding an `env_prefix`:

```python
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_prefix="APP_")

    api_key: str  # Reads APP_API_KEY
    port: int = 8000 # Reads APP_PORT
```

### Handling secrets securely with `SecretStr`

Printing plain strings can expose secret API keys or passwords in log files. Use `SecretStr` to hide sensitive data:

```python
from pydantic import SecretStr
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    api_key: SecretStr

settings = Settings(api_key="secret_api_token_123")

# SecretStr masks string output when printed or logged
print(settings.api_key)  # Output: **********

# Retrieve the actual plain-text secret when making HTTP calls
raw_key = settings.api_key.get_secret_value()
print(raw_key)  # Output: secret_api_token_123
```

### Real-world example: Production Application Settings

```python
from pydantic import SecretStr, Field
from pydantic_settings import BaseSettings, SettingsConfigDict

class AppSettings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env", env_prefix="APP_")

    # Application
    env: str = Field(default="development")
    debug: bool = False

    # Server Configuration
    host: str = "0.0.0.0"
    port: int = Field(default=8000, ge=1024, le=65535)

    # Database & API Credentials
    database_url: SecretStr
    openai_api_key: SecretStr

    @property
    def is_production(self) -> bool:
        return self.env.lower() == "production"

# Instantiate settings
settings = AppSettings(
    APP_DATABASE_URL="postgresql://user:pass@db:5432/prod",
    APP_OPENAI_API_KEY="sk-proj-secret-key"
)

print(f"Running on port {settings.port} | Production: {settings.is_production}")
```

### Singleton settings instance pattern

Load settings once and reuse the instance using `@lru_cache`:

```python
from functools import lru_cache
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    app_name: str = "My Application"
    admin_email: str = "admin@example.com"

@lru_cache
def get_settings() -> Settings:
    # Loaded once and cached in memory
    return Settings()

# Use across multiple modules
settings = get_settings()
```

### Learn more

- [Pydantic Settings documentation](https://docs.pydantic.dev/latest/concepts/pydantic_settings/)

---

## 7. Structured LLM Output

Extract type-safe, validated responses from AI language models.

### The problem with LLM responses

Large Language Models (LLMs) return unstructured text responses:

```text
The product is a MacBook Pro laptop costing $1999.00. It is currently in stock.
```

To use LLM responses in Python applications, you need structured data:

```json
{
  "product": "MacBook Pro",
  "price": 1999.0,
  "in_stock": true
}
```

Parsing raw text with regular expressions is fragile. Language models can vary their text formatting unexpectedly.

### Mental Model: The Mold / Stencil

Think of a Pydantic model as a rigid mold or stencil. Unstructured text generated by an LLM is poured into the mold. Pydantic shapes and validates the raw text, guaranteeing that the final output matches your defined Python data structure.

### OpenAI Integration with Pydantic

The official OpenAI SDK supports Pydantic models directly for structured outputs using `beta.chat.completions.parse()` or `responses.parse()`:

```python
from openai import OpenAI
from pydantic import BaseModel, Field

# 1. Define target extraction schema
class ProductExtraction(BaseModel):
    name: str = Field(description="Name of the product")
    price: float = Field(description="Price in USD")
    category: str = Field(description="Product category")
    in_stock: bool = Field(description="Availability status")

# 2. Instantiate client
client = OpenAI()

# 3. Request parsed completion
response = client.beta.chat.completions.parse(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "Extract product details from text."},
        {"role": "user", "content": "The MacBook Pro is priced at $1999.00 in Electronics. Available now."}
    ],
    response_format=ProductExtraction,
)

# 4. Access validated Pydantic model directly
product: ProductExtraction = response.choices[0].message.parsed

print(product.name)      # MacBook Pro
print(product.price)     # 1999.0
print(product.in_stock)  # True
```

### Adding Field Descriptions for LLM Context

LLMs inspect Pydantic field `description` attributes to understand what value to extract for each attribute:

```python
from pydantic import BaseModel, Field

class UserLead(BaseModel):
    full_name: str = Field(description="First and last name of the customer")
    email: str | None = Field(description="Email address if explicitly mentioned in text")
    company_size: int = Field(description="Number of employees at customer company")
```

### Enforcing Choices using `Literal`

Restrict LLM output choices to predefined values:

```python
from typing import Literal
from pydantic import BaseModel, Field

class CustomerSentiment(BaseModel):
    sentiment: Literal["positive", "negative", "neutral"]
    urgency: Literal["low", "medium", "high"]
    summary: str = Field(description="Brief 1-sentence summary of customer feedback")
```

The AI model is constrained to pick only from the listed string options.

### Generic Validation for Any LLM Provider

If using LLM providers without native SDK Pydantic support (such as Anthropic, Ollama, or Google Gemini), prompt the model to return JSON, and validate the output string using `model_validate_json()`:

```python
import json
from pydantic import BaseModel, ValidationError

class ActionItem(BaseModel):
    task: str
    assignee: str
    priority: int

# Simulated JSON string response returned from LLM
raw_llm_response = '{"task": "Update documentation", "assignee": "Alice", "priority": 1}'

try:
    action_item = ActionItem.model_validate_json(raw_llm_response)
    print(f"Task: {action_item.task} | Assignee: {action_item.assignee}")
except ValidationError as e:
    print(f"LLM returned invalid JSON structure: {e}")
```

### Handling LLM Extraction Failures with Retries

When validation fails, send the validation error message back to the LLM so it can correct its mistake:

```python
from pydantic import BaseModel, Field, ValidationError

class TicketCategory(BaseModel):
    category_id: int = Field(ge=100, le=999)
    label: str

def process_llm_json(raw_json_text: str):
    try:
        return TicketCategory.model_validate_json(raw_json_text)
    except ValidationError as e:
        # Pass error description back into prompt for retry loop
        retry_prompt = f"Your previous JSON was invalid:\n{e}\nPlease correct the JSON."
        return retry_prompt
```

### Real-world example: Invoice Data Extraction Agent

```python
from typing import Literal
from pydantic import BaseModel, Field

class LineItem(BaseModel):
    description: str
    quantity: int = Field(ge=1)
    unit_price: float = Field(ge=0.0)

class InvoiceData(BaseModel):
    invoice_id: str = Field(description="Invoice identifier number")
    vendor: str = Field(description="Company issuing the invoice")
    items: list[LineItem]
    total_amount: float = Field(gt=0.0)
    status: Literal["paid", "pending", "overdue"]

# Sample unstructured document text
document_text = """
INVOICE #INV-2025-88
Vendor: Data Lumina Services
Items:
- Python Training Course (Quantity: 2) @ $250.00 each
- API Consulting (Quantity: 1) @ $500.00 each
Total: $1000.00
Payment Status: Paid
"""
```

### Learn more

- [OpenAI Structured Outputs Guide](https://platform.openai.com/docs/guides/structured-outputs)
- [Anthropic Structured Outputs Guide](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)

---

## 8. Summary

Key learnings, patterns, and best practices.

### Core Learnings Overview

1. **Chapter 1: Introduction**: Python's dynamic typing causes runtime bugs when dealing with external data. Pydantic validates incoming data at runtime and catches errors at the application boundary.
2. **Chapter 2: Type Hints**: Python type hints (`str`, `int`, `list[str]`, `str | None`) document expected types. Standard Python ignores them, but Pydantic uses them for enforcement.
3. **Chapter 3: Your First Model**: Subclass `BaseModel` to define data models. Use `model_dump()` to export dictionaries, `model_dump_json()` for JSON strings, and `model_validate()` to parse incoming data.
4. **Chapter 4: Validation and Fields**: Apply constraints using `Field()` (`min_length`, `gt`, `pattern`). Add custom validation rules using `@field_validator` and `@model_validator`.
5. **Chapter 5: Nested Models**: Build complex data structures by nesting models inside other models or using `list[Model]`.
6. **Chapter 6: Pydantic Settings**: Manage environment variables safely using `BaseSettings` and `.env` files. Hide sensitive tokens using `SecretStr`.
7. **Chapter 7: Structured LLM Output**: Convert unstructured LLM text into type-safe Python data models using SDK response parsing or `model_validate_json()`.

### Pydantic Cheat Sheet

| Task                     | Syntax Example                                     |
| :----------------------- | :------------------------------------------------- |
| **Define Model**         | `class User(BaseModel): name: str`                 |
| **Field Constraints**    | `age: int = Field(ge=18, le=100)`                  |
| **Default Factory**      | `tags: list[str] = Field(default_factory=list)`    |
| **Parse Dictionary**     | `user = User.model_validate(data_dict)`            |
| **Parse JSON String**    | `user = User.model_validate_json(json_str)`        |
| **Export Dictionary**    | `data = user.model_dump()`                         |
| **Export JSON String**   | `json_str = user.model_dump_json()`                |
| **Exclude Secret Field** | `user.model_dump(exclude={'password'})`            |
| **Catch Error**          | `except ValidationError as e: print(e.errors())`   |
| **Custom Validator**     | `@field_validator("name")`                         |
| **Base Settings**        | `class Settings(BaseSettings): api_key: SecretStr` |

### Best Practices Checklist

- **Validate at Boundaries**: Instantiated Pydantic models at entry points (API endpoints, CLI inputs, DB reads, LLM responses).
- **Use `SecretStr` for Sensitive Data**: Prevent passwords and API keys from leaking into log files.
- **Use `default_factory` for Dynamic Objects**: Never assign mutable defaults like `default=datetime.now()`. Use `default_factory=datetime.now`.
- **Catch `ValidationError`**: Always wrap external data parsing in `try ... except ValidationError` blocks to return clean user error responses.
- **Annotate Field Descriptions for LLMs**: When passing models to AI models, write clear field `description` parameters to guide extraction accuracy.

### Resources

- [Official Pydantic Documentation](https://docs.pydantic.dev/latest/)
- [Pydantic Settings Guide](https://docs.pydantic.dev/latest/concepts/pydantic_settings/)
- [Python for AI Course](https://python.datalumina.com)
