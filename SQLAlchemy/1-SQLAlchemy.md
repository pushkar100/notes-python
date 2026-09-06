# SQLAlchemy Master Tutorial: From Beginner to Pro

_A progressive, step-by-step guide to mastering databases in Python with SQLAlchemy 2.0._

- [Introduction: What is SQLAlchemy?](#introduction-what-is-sqlalchemy)
  - [Core vs. ORM: The Two Layers](#core-vs-orm-the-two-layers)
- [1. Setup & The Engine (Connecting to the Database)](#1-setup-the-engine-connecting-to-the-database)
  - [Installation](#installation)
  - [What is the Engine?](#what-is-the-engine)
  - [Creating Your First Engine](#creating-your-first-engine)
- [2. Running Raw SQL (Core Basics)](#2-running-raw-sql-core-basics)
  - [The Connection Context (`with engine.connect()`)](#the-connection-context-with-engineconnect)
  - [Connection Styles: Alternatives to `with engine.connect()`](#connection-styles-alternatives-to-with-engineconnect)
- [3. SQLAlchemy Core: Tables, Schemas & Queries](#3-sqlalchemy-core-tables-schemas-queries)
  - [The Core Building Blocks](#the-core-building-blocks)
  - [Common Data Types Reference](#common-data-types-reference)
  - [Table & Column Constraints Reference](#table-column-constraints-reference)
  - [Creating Tables in the Database](#creating-tables-in-the-database)
  - [Core CRUD: Building Queries (Functions vs. Table Methods)](#core-crud-building-queries-functions-vs-table-methods)
  - [Complete Core CRUD Example](#complete-core-crud-example)
  - [Working with Query Results (`Result` Object)](#working-with-query-results-result-object)
  - [Core Relationships & JOINs](#core-relationships-joins)
  - [Summary: Chainable `select()` Methods](#summary-chainable-select-methods)
- [4. SQLAlchemy ORM: Defining Models](#4-sqlalchemy-orm-defining-models)
  - [The ORM Mental Model](#the-orm-mental-model)
  - [Style A: Classic ORM Syntax (`Column` & `sessionmaker`)](#style-a-classic-orm-syntax-column-sessionmaker)
  - [Style B: Modern 2.0 ORM Syntax (`Mapped` & `mappedcolumn`)](#style-b-modern-20-orm-syntax-mapped-mapped_column)
  - [Quick Comparison: Core vs. Classic ORM vs. Modern 2.0](#quick-comparison-core-vs-classic-orm-vs-modern-20)
- [5. Working with ORM Data (CRUD & Relationships)](#5-working-with-orm-data-crud-relationships)
  - [Basic CRUD with a Single Model](#basic-crud-with-a-single-model)
  - [Managing Related Data](#managing-related-data)
  - [Eager Loading (`selectinload`) to Prevent Slow Queries](#eager-loading-selectinload-to-prevent-slow-queries)
- [6. SQLAlchemy with Pandas DataFrames](#6-sqlalchemy-with-pandas-dataframes)
  - [Writing DataFrames to SQL (`df.tosql`)](#writing-dataframes-to-sql-dfto_sql)
  - [Reading SQL Data into DataFrames (`pd.readsql`)](#reading-sql-data-into-dataframes-pdread_sql)
- [7. Web Integration: Flask-SQLAlchemy Example](#7-web-integration-flask-sqlalchemy-example)
  - [Complete Minimal Flask REST API](#complete-minimal-flask-rest-api)
- [Summary & Quick Cheat Sheet](#summary-quick-cheat-sheet)

---

## Introduction: What is SQLAlchemy?

**SQLAlchemy** is Python's leading database library. Instead of writing messy, hard-coded SQL strings throughout your project, SQLAlchemy lets you interact with relational databases using clean, standard Python code.

### Core vs. ORM: The Two Layers

SQLAlchemy is divided into two layers:

1. **SQLAlchemy Core:** The foundational layer. It manages database connections, handles transactions, and builds SQL queries using Python expressions.
2. **SQLAlchemy ORM (Object-Relational Mapper):** Built on top of Core. It lets you define database tables as standard Python classes, and table rows as Python objects.

```text
+---------------------------------------------------+
|                  SQLAlchemy ORM                   |
|     (Classes, Objects, Sessions, Relationships)   |
+---------------------------------------------------+
|                 SQLAlchemy Core                   |
|  (Schema, Table, Column, Engine, Connection Pool) |
+---------------------------------------------------+
|               Database Driver (DBAPI)             |
|          (sqlite3, psycopg2, pymysql, etc.)       |
+---------------------------------------------------+
|                 Relational Database               |
|          (SQLite, PostgreSQL, MySQL, etc.)        |
+---------------------------------------------------+
```

---

## 1. Setup & The Engine (Connecting to the Database)

### Installation

Install or upgrade to SQLAlchemy 2.x:

```bash
pip install -U SQLAlchemy
```

Verify your installation:

```python
import sqlalchemy
print(sqlalchemy.__version__)  # Should output 2.x.x
```

### What is the Engine?

The **Engine** is the starting point of every SQLAlchemy application. Think of it as the **central power station** connecting your Python script to your actual database file or server.

```text
+-----------------------------------------------------------------------+
|                         Your Python Application                       |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                                ENGINE                                 |
|                                                                       |
|  +------------------------+      +---------------------------------+  |
|  |        Dialect         |      |         Connection Pool         |  |
|  | (Translates SQL syntax |      |   (Reuses active connections    |  |
|  |  e.g., SQLite vs Postgres)    |    to keep your app fast)       |  |
|  +------------------------+      +---------------------------------+  |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                        Database Driver (DBAPI)                        |
|                     (sqlite3, psycopg2, pymysql)                      |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                          Physical Database                            |
|                     (SQLite file, PostgreSQL, MySQL)                  |
+-----------------------------------------------------------------------+
```

The Engine handles three tasks automatically in the background:

- **Dialect:** Different databases have slightly different SQL rules. The Dialect translates generic SQLAlchemy code into the exact flavor your database understands (SQLite, PostgreSQL, MySQL, etc.).
- **Connection Pool:** Opening a new database connection every time is slow. The pool keeps a few open connections ready to be reused, making your app significantly faster.
- **DBAPI Driver:** Talks to Python's low-level database driver (e.g., the built-in `sqlite3` module).

> **Important Note on "Lazy Connection":** Creating an engine with `create_engine()` does **not** connect to the database immediately. It waits until you actually execute your first query.

### Creating Your First Engine

```python
from sqlalchemy import create_engine

# Connect to a local SQLite database file named 'my_database.db'
# echo=True prints all generated SQL queries to the terminal (great for learning!)
engine = create_engine("sqlite:///my_database.db", echo=True)
```

---

## 2. Running Raw SQL (Core Basics)

Before defining classes or tables, you can run raw SQL queries directly through your engine.

### The Connection Context (`with engine.connect()`)

To run queries, ask the engine for a connection using `engine.connect()`. Wrapping it in a Python `with` block guarantees the connection is automatically closed when you finish:

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///my_database.db", echo=True)

# Open a connection and execute SQL
with engine.connect() as conn:
    # 1. Create a table
    conn.execute(text("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)"))

    # 2. Insert rows
    conn.execute(text("INSERT INTO users (name, age) VALUES ('Alice', 25)"))
    conn.execute(text("INSERT INTO users (name, age) VALUES ('Bob', 30)"))

    # 3. Save changes (commit)
    conn.commit()

    # 4. Query data
    result = conn.execute(text("SELECT * FROM users"))
    for row in result:
        print(f"ID: {row.id}, Name: {row.name}, Age: {row.age}")
```

#### Key Methods Explained

- **`text("...")`**: Safely wraps raw SQL text into an executable SQLAlchemy clause. In SQLAlchemy 2.0, raw SQL strings must always be wrapped in `text()`.
- **`conn.execute(...)`**: Sends the SQL command to the database and returns the result.
- **`conn.commit()`**: Permanently saves data changes (`INSERT`, `UPDATE`, `DELETE`) to disk.
- **`for row in result:`**: Loops through matching database rows.

### Connection Styles: Alternatives to `with engine.connect()`

#### Style 1: Automatic Commits (`with engine.begin()`)

If you don't want to write `conn.commit()` manually every time, use `engine.begin()`. It opens a connection, starts a transaction, and **commits automatically** when the block finishes without errors:

```python
with engine.begin() as conn:
    conn.execute(text("INSERT INTO users (name, age) VALUES ('Charlie', 35)"))
    # No conn.commit() needed!
```

#### Style 2: Manual Connection (`connect()` & `close()`)

Without the `with` statement, you must close the connection manually in a `try...finally` block:

```python
conn = engine.connect()
try:
    conn.execute(text("INSERT INTO users (name, age) VALUES ('David', 28)"))
    conn.commit()
finally:
    conn.close()  # Always close to prevent connection leaks!
```

#### Style 3: Using `Session` for Raw SQL

You can also use SQLAlchemy ORM's `Session` object as a direct drop-in replacement for `engine.connect()`:

```python
from sqlalchemy.orm import Session

with Session(engine) as session:
    session.execute(text("INSERT INTO users (name, age) VALUES ('Eve', 22)"))
    session.commit()
```

---

## 3. SQLAlchemy Core: Tables, Schemas & Queries

Writing raw SQL strings works, but it is easy to make typo mistakes and doesn't take advantage of Python's safety. **SQLAlchemy Core** allows you to define database tables as Python objects.

### The Core Building Blocks

- **`MetaData`**: A catalog/registry that holds all table definitions for your database.
- **`Table`**: Represents a physical database table bound to a `MetaData` catalog.
- **`Column`**: Represents a field in a table, specifying name, data type, and constraints.

```text
+-------------------------------------------------------------------------+
|                               MetaData                                  |
|         (Central catalog holding all table schema definitions)          |
|                                                                         |
|   +-----------------------------------------------------------------+   |
|   |                       Table ('people')                          |   |
|   |   +------------------------+--------------------------------+   |   |
|   |   | Column('id')           | Integer, primary_key=True      |   |   |
|   |   +------------------------+--------------------------------+   |   |
|   |   | Column('name')         | String(50), nullable=False     |   |   |
|   |   +------------------------+--------------------------------+   |   |
|   |   | Column('age')          | Integer                        |   |   |
|   |   +------------------------+--------------------------------+   |   |
|   +-----------------------------------------------------------------+   |
+-------------------------------------------------------------------------+
                                     |
                          meta.create_all(engine)
                                     v
+-------------------------------------------------------------------------+
|                                ENGINE                                   |
|       (Executes "CREATE TABLE IF NOT EXISTS people..." on DB)          |
+-------------------------------------------------------------------------+
```

### Common Data Types Reference

| Data Type           | SQL Type        | Description & Example                                                        |
| :------------------ | :-------------- | :--------------------------------------------------------------------------- |
| **`Integer`**       | `INTEGER`       | Whole numbers: `Column('age', Integer)`                                      |
| **`BigInteger`**    | `BIGINT`        | Large numbers (64-bit): `Column('views', BigInteger)`                        |
| **`String(n)`**     | `VARCHAR(n)`    | Text with character limit: `Column('name', String(50))`                      |
| **`Text`**          | `TEXT`          | Unlimited text (articles, comments): `Column('bio', Text)`                   |
| **`Float`**         | `FLOAT`         | Decimals: `Column('score', Float)`                                           |
| **`Numeric(p, s)`** | `DECIMAL(p, s)` | Exact precision (currency): `Column('price', Numeric(10, 2))`                |
| **`Boolean`**       | `BOOLEAN`       | True/False flags: `Column('is_active', Boolean)`                             |
| **`DateTime`**      | `DATETIME`      | Date and time (Python `datetime.datetime`): `Column('created_at', DateTime)` |

### Table & Column Constraints Reference

| Constraint / Option       | Description                                                 | Example                                              |
| :------------------------ | :---------------------------------------------------------- | :--------------------------------------------------- |
| **`primary_key=True`**    | Unique row identifier (auto-increments integers in SQLite). | `Column('id', Integer, primary_key=True)`            |
| **`nullable=False`**      | Column cannot be empty (`NOT NULL`).                        | `Column('name', String(50), nullable=False)`         |
| **`unique=True`**         | All values in this column must be unique.                   | `Column('email', String(100), unique=True)`          |
| **`default=value`**       | Default value set on Python side if omitted during insert.  | `Column('status', String(20), default='active')`     |
| **`ForeignKey('t.col')`** | Links to a column in another table.                         | `Column('user_id', Integer, ForeignKey('users.id'))` |

### Creating Tables in the Database

```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String

engine = create_engine("sqlite:///mydatabase.db", echo=True)

# 1. Create MetaData registry
meta = MetaData()

# 2. Define the Table structure
people = Table(
    "people",
    meta,
    Column("id", Integer, primary_key=True),
    Column("name", String(50), nullable=False),
    Column("age", Integer)
)

# 3. Create table in the database if it doesn't already exist
meta.create_all(engine)
```

#### Output Breakdown of `meta.create_all(engine)`

With `echo=True`, SQLAlchemy inspects the database first and then creates missing tables:

```sql
BEGIN (implicit)
PRAGMA main.table_info("people")  -- Checks if table already exists
CREATE TABLE people (
    id INTEGER NOT NULL,
    name VARCHAR(50) NOT NULL,
    age INTEGER,
    PRIMARY KEY (id)
)
COMMIT
```

_Note: `meta.create_all()` is safe to run repeatedly; it never overwrites or alters existing tables._

---

### Core CRUD: Building Queries (Functions vs. Table Methods)

In SQLAlchemy Core, queries can be written in two equivalent styles:

1. **Function Import Style:** `select(people)`
2. **Table Method Style:** `people.select()`

Both styles produce the exact same SQL queries!

#### 1. Create (Insert)

```python
from sqlalchemy import insert

# Function Import Style:
stmt = insert(people).values(name="Alice", age=25)

# Table Method Style:
stmt = people.insert().values(name="Alice", age=25)
```

#### 2. Read (Select)

```python
from sqlalchemy import select

# Function Import Style:
stmt = select(people).where(people.c.age > 20)

# Table Method Style:
stmt = people.select().where(people.c.age > 20)
```

> **What is `.c`?** The `.c` attribute stands for **columns**. It lets you access table columns as Python attributes: `people.c.name` or `people.c.age`.

#### 3. Update

```python
from sqlalchemy import update

# Function Import Style:
stmt = update(people).where(people.c.name == "Alice").values(age=26)

# Table Method Style:
stmt = people.update().where(people.c.name == "Alice").values(age=26)
```

#### 4. Delete

```python
from sqlalchemy import delete

# Function Import Style:
stmt = delete(people).where(people.c.name == "Alice")

# Table Method Style:
stmt = people.delete().where(people.c.name == "Alice")
```

#### 5. Combining Multiple `.where()` Conditions

```python
from sqlalchemy import or_, and_, select

# AND logic: Chain multiple .where() calls
stmt1 = select(people).where(people.c.age >= 20).where(people.c.name == "Alice")

# AND logic: Separate conditions with commas
stmt2 = select(people).where(people.c.age >= 20, people.c.name == "Alice")

# OR logic: Use the or_() helper
stmt3 = select(people).where(or_(people.c.age < 18, people.c.age > 65))
```

---

### Complete Core CRUD Example

Here is a full, runnable script executing all four CRUD operations with Core:

```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, insert, select, update, delete

engine = create_engine("sqlite:///mydatabase.db", echo=True)
meta = MetaData()

people = Table(
    "people",
    meta,
    Column("id", Integer, primary_key=True),
    Column("name", String(50), nullable=False),
    Column("age", Integer)
)
meta.create_all(engine)

with engine.connect() as conn:
    # 1. CREATE: Insert single and multiple rows
    conn.execute(insert(people).values(name="Alice", age=25))
    conn.execute(insert(people), [
        {"name": "Bob", "age": 30},
        {"name": "Charlie", "age": 35}
    ])
    conn.commit()

    # 2. READ: Query data
    result = conn.execute(select(people).where(people.c.age >= 25))
    for row in result:
        print(f"ID: {row.id}, Name: {row.name}, Age: {row.age}")

    # 3. UPDATE: Modify row
    conn.execute(update(people).where(people.c.name == "Alice").values(age=26))
    conn.commit()

    # 4. DELETE: Remove row
    conn.execute(delete(people).where(people.c.name == "Charlie"))
    conn.commit()
```

---

### Working with Query Results (`Result` Object)

When you execute a query (`result = conn.execute(...)`), SQLAlchemy returns a **`Result`** object.

#### 1. Looping Through Rows

The simplest, most memory-efficient way to read data is looping directly over `result`:

```python
result = conn.execute(select(people))
for row in result:
    print(f"{row.name} is {row.age} years old")
```

#### 2. Three Ways to Access Values on a Row

```python
row = conn.execute(select(people)).first()

# Method A: Attribute / Dot Access (Recommended)
print(row.name)  # 'Alice'

# Method B: Index Access
print(row[1])    # 'Alice'

# Method C: Key / Mapping Access
print(row._mapping["name"])  # 'Alice'
```

#### 3. Fetching Methods Reference

| Method                     | What It Returns           | When to Use                                                     |
| :------------------------- | :------------------------ | :-------------------------------------------------------------- |
| **`result.all()`**         | List of all matching rows | Fetch everything into memory.                                   |
| **`result.first()`**       | First row, or `None`      | Fetch one row safely without crashing if empty.                 |
| **`result.one()`**         | Exactly one row           | Expect exactly 1 row; raises error if 0 or >1 rows.             |
| **`result.one_or_none()`** | One row, or `None`        | Unique query that might not exist yet; raises error if >1 rows. |
| **`result.fetchmany(n)`**  | List of `n` rows          | Process large datasets in batches.                              |

#### 4. Converting Rows to Dictionaries

```python
# Single row to dict:
row_dict = row._asdict()  # {'id': 1, 'name': 'Alice', 'age': 25}

# All rows to a list of dicts:
result = conn.execute(select(people))
all_dict = [dict(r._mapping) for r in result]
```

> **⚠️ Beginner Gotcha: `Result` is a One-Time Stream!**
> Once you iterate over `result` or call `.all()`, the stream is empty. Calling `result.all()` a second time returns an empty list `[]`.

---

### Core Relationships & JOINs

#### Defining Tables with `ForeignKey`

```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, ForeignKey

engine = create_engine("sqlite:///mydatabase.db", echo=True)
meta = MetaData()

# Parent Table
users = Table(
    "users",
    meta,
    Column("id", Integer, primary_key=True),
    Column("name", String(50), nullable=False)
)

# Child Table (user_id points to users.id)
addresses = Table(
    "addresses",
    meta,
    Column("id", Integer, primary_key=True),
    Column("email", String(100), nullable=False),
    Column("user_id", Integer, ForeignKey("users.id"))
)

meta.create_all(engine)
```

#### Sample Dataset

```python
with engine.connect() as conn:
    conn.execute(insert(users), [
        {"id": 1, "name": "Alice"},
        {"id": 2, "name": "Bob"},
        {"id": 3, "name": "Charlie"}  # Charlie has no email address
    ])
    conn.execute(insert(addresses), [
        {"email": "alice@work.com", "user_id": 1},
        {"email": "alice@home.org", "user_id": 1},
        {"email": "bob@example.com", "user_id": 2}
    ])
    conn.commit()
```

#### 1. Inner Join (`users.join(addresses)`)

Returns only rows with matches in **both** tables (Charlie is omitted):

```python
stmt = select(users.c.name, addresses.c.email).select_from(users.join(addresses))
with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(f"{row.name} | {row.email}")
```

```text
Output:
Alice | alice@work.com
Alice | alice@home.org
Bob | bob@example.com
```

#### 2. Left Outer Join (`users.outerjoin(addresses)`)

Returns **all** rows from the left table (`users`), even if they have no matching record in `addresses` (Charlie is included with `None`):

```python
stmt = select(users.c.name, addresses.c.email).select_from(users.outerjoin(addresses))
with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(f"{row.name} | {row.email}")
```

```text
Output:
Alice | alice@work.com
Alice | alice@home.org
Bob | bob@example.com
Charlie | None
```

#### 3. Aggregation & `GROUP BY`

Summarizes data across groups using SQL functions like `func.count()`:

```python
from sqlalchemy import func

stmt = (
    select(users.c.name, func.count(addresses.c.id).label("total_emails"))
    .select_from(users.outerjoin(addresses))
    .group_by(users.c.id, users.c.name)
)

with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(f"{row.name} has {row.total_emails} email(s)")
```

```text
Output:
Alice has 2 email(s)
Bob has 1 email(s)
Charlie has 0 email(s)
```

#### ⚠️ Common `GROUP BY` Gotchas

1. **Un-aggregated Columns Must Be in `GROUP BY`:** Any column in `select(...)` not wrapped in an aggregate function (like `func.count()`) must be listed in `.group_by(...)`. Failing to do so causes database errors in PostgreSQL and MySQL.
2. **Use `.having()` for Aggregate Conditions (Not `.where()`):**
   - `.where()` filters rows **before** grouping.
   - `.having()` filters groups **after** aggregation: `.having(func.count(addresses.c.id) > 1)`.
3. **Always Label Aggregates with `.label("name")`:** This allows clean attribute access on result rows (`row.total_emails`).

---

### Summary: Chainable `select()` Methods

| Method                  | SQL Keyword     | What It Does                                  | Example                               |
| :---------------------- | :-------------- | :-------------------------------------------- | :------------------------------------ |
| **`.where(*conds)`**    | `WHERE`         | Filters rows matching criteria.               | `.where(users.c.age >= 18)`           |
| **`.select_from(obj)`** | `FROM` / `JOIN` | Specifies the query source or join construct. | `.select_from(users.join(addresses))` |
| **`.order_by(*cols)`**  | `ORDER BY`      | Sorts rows (use `.desc()` for descending).    | `.order_by(users.c.age.desc())`       |
| **`.group_by(*cols)`**  | `GROUP BY`      | Groups rows for aggregate calculations.       | `.group_by(users.c.name)`             |
| **`.having(*conds)`**   | `HAVING`        | Filters aggregate results after `GROUP BY`.   | `.having(func.count() > 1)`           |
| **`.limit(n)`**         | `LIMIT n`       | Restricts results to `n` rows.                | `.limit(10)`                          |
| **`.offset(n)`**        | `OFFSET n`      | Skips first `n` rows (used for pagination).   | `.limit(10).offset(20)`               |
| **`.distinct()`**       | `DISTINCT`      | Removes duplicate rows from output.           | `select(users.c.name).distinct()`     |

---

## 4. SQLAlchemy ORM: Defining Models

The **ORM (Object-Relational Mapper)** allows you to treat database tables as standard Python classes and individual rows as Python objects.

### The ORM Mental Model

| Python ORM Concept                             | Database Equivalent                           |
| :--------------------------------------------- | :-------------------------------------------- |
| **Python Class** (`class User`)                | **Database Table** (`users` table)            |
| **Class Attributes** (`name`, `age`)           | **Table Columns** (`name VARCHAR`, `age INT`) |
| **Object Instance** (`u = User(name='Alice')`) | **Single Table Row**                          |

---

### Style A: Classic ORM Syntax (`Column` & `sessionmaker`)

In older codebases and tutorials, models use `Column()` directly and sessions are built with `sessionmaker`:

```python
from sqlalchemy import create_engine, Column, Integer, String, ForeignKey
from sqlalchemy.orm import declarative_base, relationship, sessionmaker

engine = create_engine("sqlite:///classic.db", echo=True)
Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    name = Column(String(50), nullable=False)

    # Relationship: Connects User to Address objects in Python
    addresses = relationship("Address", back_populates="user")

class Address(Base):
    __tablename__ = "addresses"

    id = Column(Integer, primary_key=True)
    email = Column(String(100), nullable=False)
    user_id = Column(Integer, ForeignKey("users.id"))

    # Relationship: Connects Address back to User
    user = relationship("User", back_populates="addresses")

Base.metadata.create_all(engine)

# Session factory pattern
Session = sessionmaker(bind=engine)
session = Session()

# Add a user with addresses
new_user = User(name="Alice")
new_user.addresses = [Address(email="alice@work.com")]
session.add(new_user)
session.commit()
session.close()
```

---

### Style B: Modern 2.0 ORM Syntax (`Mapped` & `mapped_column`)

In modern SQLAlchemy 2.0, models use **Python type hints** for better IDE autocompletion and safety:

```python
from typing import List
from sqlalchemy import create_engine, String, ForeignKey
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship

engine = create_engine("sqlite:///modern.db", echo=True)

# 1. Base class
class Base(DeclarativeBase):
    pass

# 2. User Model
class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(50), nullable=False)

    # 1-to-Many Relationship
    addresses: Mapped[List["Address"]] = relationship(
        back_populates="user",
        cascade="all, delete-orphan"
    )

    def __repr__(self):
        return f"<User(id={self.id}, name='{self.name}')>"

# 3. Address Model
class Address(Base):
    __tablename__ = "addresses"

    id: Mapped[int] = mapped_column(primary_key=True)
    email: Mapped[str] = mapped_column(String(100), nullable=False)
    user_id: Mapped[int] = mapped_column(ForeignKey("users.id"))

    # Many-to-1 Relationship
    user: Mapped["User"] = relationship(back_populates="addresses")

    def __repr__(self):
        return f"<Address(id={self.id}, email='{self.email}')>"

# 4. Create tables
Base.metadata.create_all(engine)
```

---

### Quick Comparison: Core vs. Classic ORM vs. Modern 2.0

| Feature               | SQLAlchemy Core                  | Classic ORM (1.x Style)                          | Modern ORM (2.0 Style)                                   |
| :-------------------- | :------------------------------- | :----------------------------------------------- | :------------------------------------------------------- |
| **Catalog Registry**  | `meta = MetaData()`              | `Base = declarative_base()`                      | `class Base(DeclarativeBase): pass`                      |
| **Model Setup**       | `Table('users', meta, ...)`      | `class User(Base): __tablename__ = 'users'`      | `class User(Base): __tablename__ = 'users'`              |
| **Column Definition** | `Column('name', String(50))`     | `name = Column(String(50))`                      | `name: Mapped[str] = mapped_column(String(50))`          |
| **Type Hints**        | None                             | None                                             | Full Python Type Hints (`Mapped[str]`)                   |
| **Relationships**     | Manual SQL JOINs                 | `addresses = relationship(...)`                  | `addresses: Mapped[List['Address']] = relationship(...)` |
| **Session Usage**     | `with engine.connect() as conn:` | `Session = sessionmaker(...)`<br>`s = Session()` | `with Session(engine) as session:`                       |

---

## 5. Working with ORM Data (CRUD & Relationships)

To interact with ORM models, use a **`Session`**. The `Session` acts as an in-memory workspace that tracks your changes and commits them together.

### Basic CRUD with a Single Model

```python
from sqlalchemy.orm import Session
from sqlalchemy import select

# CREATE (Insert)
with Session(engine) as session:
    user1 = User(name="Alice")
    user2 = User(name="Bob")
    session.add_all([user1, user2])
    session.commit()

# READ (Query with scalars())
with Session(engine) as session:
    # All users
    all_users = session.scalars(select(User)).all()

    # Filter by condition
    alice = session.scalars(select(User).where(User.name == "Alice")).first()

    # Sort users
    sorted_users = session.scalars(select(User).order_by(User.name.desc())).all()

# UPDATE (Modify in memory, then commit)
with Session(engine) as session:
    user = session.scalars(select(User).where(User.name == "Alice")).first()
    if user:
        user.name = "Alicia"
        session.commit()  # SQLAlchemy detects the change automatically!

# DELETE (Remove object)
with Session(engine) as session:
    user = session.scalars(select(User).where(User.name == "Bob")).first()
    if user:
        session.delete(user)
        session.commit()
```

> **What is `session.scalars()`?**
> In SQLAlchemy 2.0, `session.execute(select(User))` returns row tuples containing objects `(User, )`. Calling `session.scalars(...)` unwraps the tuple and gives you direct access to the `User` object itself!

---

### Managing Related Data

#### 1. Creating Related Objects

Attach child objects directly to parent relationship lists:

```python
with Session(engine) as session:
    user = User(
        name="Alice",
        addresses=[
            Address(email="alice@work.com"),
            Address(email="alice@home.org")
        ]
    )
    session.add(user)
    session.commit()  # Saves User and both Address records automatically!
```

#### 2. Reading Associated Data (Relationship Navigation)

Navigate between parent and child without writing any SQL joins:

```python
with Session(engine) as session:
    user = session.scalars(select(User).where(User.name == "Alice")).first()

    # Parent -> Children: Access user's addresses
    for addr in user.addresses:
        print(f"Email: {addr.email}")

    # Child -> Parent: Access an address's owner
    address = session.scalars(select(Address).where(Address.email == "alice@work.com")).first()
    print(f"Belongs to: {address.user.name}")
```

#### 3. Querying Across Relationships with `.join()` and `.any()`

```python
with Session(engine) as session:
    # Join models and filter by child property
    stmt1 = select(User).join(User.addresses).where(Address.email.like("%@work.com"))
    work_users = session.scalars(stmt1).all()

    # Filter parent using .any() on relationship
    stmt2 = select(User).where(User.addresses.any(Address.email == "alice@home.org"))
    alice = session.scalars(stmt2).first()
```

#### 4. Deleting & Cascade Deletion

Because `cascade="all, delete-orphan"` is set on `User.addresses`:

```python
with Session(engine) as session:
    user = session.scalars(select(User).where(User.name == "Alice")).first()

    # Deleting Alice automatically deletes all her associated addresses from the database!
    session.delete(user)
    session.commit()
```

---

### Eager Loading (`selectinload`) to Prevent Slow Queries

By default, SQLAlchemy uses **lazy loading**—it queries related addresses only when you access `user.addresses`. If you loop through 50 users, this causes **51 separate database queries** (the notorious "N+1 Problem").

Use `selectinload` to fetch all users and their addresses in **2 efficient queries**:

```python
from sqlalchemy.orm import selectinload

with Session(engine) as session:
    # Eagerly load users AND their addresses in one go
    stmt = select(User).options(selectinload(User.addresses))
    users = session.scalars(stmt).all()

    for u in users:
        print(f"{u.name}: {[a.email for a in u.addresses]}")
```

---

## 6. SQLAlchemy with Pandas DataFrames

SQLAlchemy integrates seamlessly with Pandas for data analysis pipelines.

### Writing DataFrames to SQL (`df.to_sql`)

```python
import pandas as pd
from sqlalchemy import create_engine, String, Integer

engine = create_engine("sqlite:///analytics.db", echo=True)

df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 35],
    "email": ["alice@example.com", "bob@example.com", "charlie@example.com"]
})

# Write DataFrame to a database table named 'users'
df.to_sql(
    name="users",
    con=engine,
    if_exists="replace",  # Options: 'fail', 'replace', or 'append'
    index=False,          # Do not write row numbers as a column
    dtype={"name": String(50), "age": Integer, "email": String(100)}
)
```

#### `df.to_sql` Parameters Summary

| Parameter         | Description                                                                                                                           |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **`name`**        | Target table name.                                                                                                                    |
| **`con`**         | SQLAlchemy `engine` or connection.                                                                                                    |
| **`if_exists`**   | **`'fail'`**: Error if table exists.<br>**`'replace'`**: Drop and recreate table.<br>**`'append'`**: Insert rows into existing table. |
| **`index=False`** | Prevents saving DataFrame index numbers as a column.                                                                                  |
| **`chunksize=n`** | Inserts data in batches of `n` rows for large datasets.                                                                               |
| **`dtype={...}`** | Optional dictionary specifying explicit SQLAlchemy column types.                                                                      |

### Reading SQL Data into DataFrames (`pd.read_sql`)

```python
# 1. Read from raw SQL query string:
df_query = pd.read_sql_query("SELECT name, age FROM users WHERE age >= 30", con=engine)

# 2. Read an entire database table:
df_table = pd.read_sql_table("users", con=engine)
```

---

## 7. Web Integration: Flask-SQLAlchemy Example

In web frameworks like Flask, the **`Flask-SQLAlchemy`** extension manages session lifecycles per web request automatically.

### Complete Minimal Flask REST API

```python
from flask import Flask, jsonify, request
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///app.db"
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False

# Initialize extension
db = SQLAlchemy(app)

# Define Model
class User(db.Model):
    __tablename__ = "users"

    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    email = db.Column(db.String(100), unique=True, nullable=False)

    def to_dict(self):
        return {"id": self.id, "name": self.name, "email": self.email}

# Create tables in app context
with app.app_context():
    db.create_all()

# --- API ROUTES ---

# GET all users
@app.route("/users", methods=["GET"])
def get_users():
    users = User.query.all()
    return jsonify([u.to_dict() for u in users]), 200

# POST create user
@app.route("/users", methods=["POST"])
def create_user():
    data = request.get_json()
    new_user = User(name=data["name"], email=data["email"])
    db.session.add(new_user)
    db.session.commit()
    return jsonify(new_user.to_dict()), 201

# GET single user by ID (or 404)
@app.route("/users/<int:user_id>", methods=["GET"])
def get_user(user_id):
    user = db.get_or_404(User, user_id)
    return jsonify(user.to_dict()), 200

# DELETE user
@app.route("/users/<int:user_id>", methods=["DELETE"])
def delete_user(user_id):
    user = db.get_or_404(User, user_id)
    db.session.delete(user)
    db.session.commit()
    return jsonify({"message": f"User {user_id} deleted"}), 200

if __name__ == "__main__":
    app.run(debug=True)
```

#### Why Flask-SQLAlchemy is Convenient

- **`db.Model`**: Replaces the need to define a separate `Base = declarative_base()`.
- **`db.session`**: Automatically scoped to the current HTTP request, opening and closing connections cleanly without manual connection leaks.
- **`db.get_or_404()`**: Automatically returns an HTTP 404 response if the ID doesn't exist.

---

## Summary & Quick Cheat Sheet

| Task                    | SQLAlchemy Core                                 | SQLAlchemy ORM (2.0)                            |
| :---------------------- | :---------------------------------------------- | :---------------------------------------------- |
| **Connect to Database** | `engine = create_engine("sqlite:///db.sqlite")` | `engine = create_engine("sqlite:///db.sqlite")` |
| **Manage Scope**        | `with engine.connect() as conn:`                | `with Session(engine) as session:`              |
| **Define Table**        | `Table("users", meta, Column(...))`             | `class User(Base): ...`                         |
| **Create Tables**       | `meta.create_all(engine)`                       | `Base.metadata.create_all(engine)`              |
| **Insert Data**         | `conn.execute(insert(users).values(...))`       | `session.add(User(...))`                        |
| **Query Data**          | `conn.execute(select(users))`                   | `session.scalars(select(User))`                 |
| **Commit Changes**      | `conn.commit()`                                 | `session.commit()`                              |
| **Relationships**       | `ForeignKey("users.id")` + explicit `JOIN`      | `relationship(..., back_populates=...)`         |
