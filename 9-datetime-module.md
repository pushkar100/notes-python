# Python's `datetime` Module: The Complete Beginner's Guide

- [1. Introduction: What is the `datetime` Module?](#1-introduction-what-is-the-datetime-module)
- [2. Working with Calendar Dates: `datetime.date`](#2-working-with-calendar-dates-datetimedate)
- [3. Date Arithmetic & Durations: `datetime.timedelta`](#3-date-arithmetic-durations-datetimetimedelta)
- [4. Working with Clock Times: `datetime.time`](#4-working-with-clock-times-datetimetime)
- [5. Combining Dates & Times: `datetime.datetime`](#5-combining-dates-times-datetimedatetime)
- [6. Timezones: Naive vs. Aware Datetimes](#6-timezones-naive-vs-aware-datetimes)
- [7. Working with Timezones Using `pytz`](#7-working-with-timezones-using-pytz)
- [8. Formatting and Parsing Dates: `strftime` and `strptime`](#8-formatting-and-parsing-dates-strftime-and-strptime)
- [9. Popular Real-World Use Cases (Bonus Topics)](#9-popular-real-world-use-cases-bonus-topics)
- [10. Quick Reference & Summary](#10-quick-reference-summary)

Dealing with dates and times in programming can feel confusing at first. Between leap years, different calendar formats, timezones, and hours/minutes/seconds math, keeping track of time manually would be a nightmare.

Python solves this with its built-in **`datetime` module**. It provides intuitive, reliable tools to store, calculate, convert, and format dates and times in your programs.

Best of all, **`datetime` is built right into Python**, so you don't need to install anything extra with `pip` to get started.

## 1. Introduction: What is the `datetime` Module?

The `datetime` module supplies classes for manipulating dates and times. While the module has several components, the four most important building blocks you will use every day are:

1. **`date`**: Represents a calendar date (year, month, day) without any time of day.
2. **`time`**: Represents a time of day (hour, minute, second, microsecond) independent of any particular day.
3. **`datetime`**: Combines both a date and a time into one single object.
4. **`timedelta`**: Represents a duration of time (the difference between two dates or times) used for addition and subtraction.

To start using the module, import it at the top of your Python file or Jupyter Notebook:

```python
import datetime
```

---

## 2. Working with Calendar Dates: `datetime.date`

When you only care about calendar dates (like a birthday, an anniversary, or an invoice due date), use `datetime.date`.

### Creating a Specific Date (`datetime.date`)

You create a date by passing three numbers: `year`, `month`, and `day`.

```python
import datetime

# Create a date for September 8, 2026
my_date = datetime.date(2026, 9, 8)
print(my_date)
```

**Output:**

```text
2026-09-08
```

### Common Newbie Gotchas with `datetime.date`

When creating dates, beginners often run into two very common errors:

#### Gotcha 1: Leading Zeros in Month or Day Numbers

In Python, numbers written with a leading zero (like `09` or `08`) are treated as octal numbers and trigger a `SyntaxError`:

```python
# ❌ INCORRECT:
datetime.date(2026, 09, 8)
```

**Output:**

```text
SyntaxError: leading zeros in decimal integer literals are not permitted; use an 0o prefix for octal integers
```

**Fix:** Always use plain integers without leading zeros, such as `9` instead of `09`:

```python
# ✅ CORRECT:
datetime.date(2026, 9, 8)
```

#### Gotcha 2: Passing Strings Instead of Integers

`datetime.date()` expects integers, not string text. If you pass quotes, Python throws a `TypeError`:

```python
# ❌ INCORRECT:
datetime.date('2026', '9', '8')
```

**Output:**

```text
TypeError: 'str' object cannot be interpreted as an integer
```

**Fix:** Pass bare numbers: `datetime.date(2026, 9, 8)`.

### Getting Today's Date (`datetime.date.today()`)

To find out what today's date is according to your computer's local clock, use `.today()`:

```python
import datetime

today = datetime.date.today()
print(today)
```

**Output:**

```text
2026-09-09
```

### Extracting Year, Month, and Day

You can inspect the individual components of any `date` object using its attributes:

```python
import datetime

today = datetime.date.today()

print("Year: ", today.year)
print("Month:", today.month)
print("Day:  ", today.day)
```

**Output:**

```text
Year:  2026
Month: 9
Day:   9
```

### Finding the Day of the Week

Python provides two methods to check which day of the week a date falls on:

- **`.weekday()`**: Counts days from **0 to 6** (where Monday = 0, Sunday = 6).
- **`.isoweekday()`**: Follows the international ISO standard from **1 to 7** (where Monday = 1, Sunday = 7).

```python
import datetime

today = datetime.date(2026, 9, 9)  # This is a Wednesday

print("weekday():   ", today.weekday())     # Monday is 0, so Wednesday is 2
print("isoweekday():", today.isoweekday())  # Monday is 1, so Wednesday is 3
```

**Output:**

```text
weekday():    2
isoweekday(): 3
```

Here is a quick cheat sheet:

- Monday: `weekday() = 0`, `isoweekday() = 1`
- Tuesday: `weekday() = 1`, `isoweekday() = 2`
- Wednesday: `weekday() = 2`, `isoweekday() = 3`
- Thursday: `weekday() = 3`, `isoweekday() = 4`
- Friday: `weekday() = 4`, `isoweekday() = 5`
- Saturday: `weekday() = 5`, `isoweekday() = 6`
- Sunday: `weekday() = 6`, `isoweekday() = 7`

---

## 3. Date Arithmetic & Durations: `datetime.timedelta`

How do you find what the date will be 7 days from now? Or how many days are left until your birthday?

You cannot simply write `date + 7` because Python doesn't know whether `7` means 7 seconds, 7 hours, or 7 days. That is where **`datetime.timedelta`** comes in. A `timedelta` represents a span of time.

### Creating a `timedelta`

You can create a time difference using parameters like `days`, `hours`, `minutes`, `seconds`, `weeks`, and `microseconds`:

```python
import datetime

tdelta = datetime.timedelta(days=7)
print(tdelta)
```

**Output:**

```text
7 days, 0:00:00
```

### Adding and Subtracting Dates with `timedelta`

You can add or subtract a `timedelta` to or from a `date` object:

```python
import datetime

today = datetime.date(2026, 9, 9)
tdelta = datetime.timedelta(days=7)

# What was the date exactly 1 week ago?
one_week_ago = today - tdelta
print("1 week ago was:", one_week_ago)

# What will the date be 1 week from now?
one_week_later = today + tdelta
print("1 week later is:", one_week_later)
```

**Output:**

```text
1 week ago was: 2026-09-02
1 week later is: 2026-09-16
```

### Subtracting Two Dates to Get a `timedelta`

When you subtract one `date` from another `date`, the result is automatically a `timedelta` object:

```python
import datetime

today = datetime.date(2026, 9, 9)
bday = datetime.date(2026, 9, 14)

till_bday = bday - today
print(till_bday)
print("Type:", type(till_bday))
```

**Output:**

```text
5 days, 0:00:00
Type: <class 'datetime.timedelta'>
```

### Inspecting `timedelta` Attributes (`.days` and `.total_seconds()`)

A `timedelta` object gives you convenient attributes and methods to work with the duration:

- **`.days`**: Returns the integer number of full days.
- **`.total_seconds()`**: Converts the entire duration into seconds as a floating-point number.

```python
import datetime

today = datetime.date(2026, 9, 9)
bday = datetime.date(2026, 9, 14)

till_bday = bday - today

print(f"Days remaining: {till_bday.days}")
print(f"Total seconds remaining: {till_bday.total_seconds()}")
```

**Output:**

```text
Days remaining: 5
Total seconds remaining: 432000.0
```

---

## 4. Working with Clock Times: `datetime.time`

If you only need to store or represent a time of day without caring about what day, month, or year it is, use `datetime.time`.

### Creating a Time Object

`datetime.time(hour, minute, second, microsecond)`:

- `hour`: 0 to 23 (24-hour clock format)
- `minute`: 0 to 59 (defaults to 0)
- `second`: 0 to 59 (defaults to 0)
- `microsecond`: 0 to 999999 (defaults to 0)

```python
import datetime

# 9:32 AM and 40 seconds
time_of_day = datetime.time(9, 32, 40)
print(time_of_day)
```

**Output:**

```text
09:32:40
```

### Accessing Time Components

Just like dates, you can access each piece of the time individually:

```python
import datetime

time_of_day = datetime.time(9, 32, 40, 500)

print("Hour:       ", time_of_day.hour)
print("Minute:     ", time_of_day.minute)
print("Second:     ", time_of_day.second)
print("Microsecond:", time_of_day.microsecond)
```

**Output:**

```text
Hour:        9
Minute:      32
Second:      40
Microsecond: 500
```

> Note: `datetime.time` objects represent a pure time on a clock, so you cannot directly add a `timedelta` to a pure `time` object. For time calculations involving calendar days and clock times together, use `datetime.datetime`.

---

## 5. Combining Dates & Times: `datetime.datetime`

Most real-world applications (like database records, log files, user logins, and order timestamps) need both the calendar date AND the time of day.

The `datetime.datetime` class combines all features of `date` and `time` into one powerful object.

### Creating a `datetime.datetime` Object

Pass `year`, `month`, `day`, followed optionally by `hour`, `minute`, `second`, and `microsecond`:

```python
import datetime

# May 10, 2026 at 09:40:05 and 10,000 microseconds
dt = datetime.datetime(2026, 5, 10, 9, 40, 5, 10000)
print(dt)
```

**Output:**

```text
2026-05-10 09:40:05.010000
```

### Splitting into `date` and `time`

If you have a `datetime` object, you can easily pull out just the date part or just the time part using `.date()` and `.time()`:

```python
import datetime

dt = datetime.datetime(2026, 5, 10, 9, 40, 5, 10000)

print("Date part:", dt.date())
print("Time part:", dt.time())
```

**Output:**

```text
Date part: 2026-05-10
Time part: 09:40:05.010000
```

### Accessing Individual Attributes

You have access to all date and time attributes on the combined object:

```python
import datetime

dt = datetime.datetime(2026, 5, 10, 9, 40, 5, 10000)

print(f"Date fields: year={dt.year}, month={dt.month}, day={dt.day}")
print(f"Day of week: weekday={dt.weekday()}, isoweekday={dt.isoweekday()}")
print(f"Time fields: hour={dt.hour}, min={dt.minute}, sec={dt.second}, microsec={dt.microsecond}")
```

**Output:**

```text
Date fields: year=2026, month=5, day=10
Day of week: weekday=6, isoweekday=7
Time fields: hour=9, min=40, sec=5, microsec=10000
```

### Doing Math with `datetime` and `timedelta`

Just like with `date`, you can perform math on full `datetime` objects using `timedelta`:

```python
import datetime

current_moment = datetime.datetime(2026, 9, 9, 12, 0, 0)

# Add 7 days
seven_days_later = current_moment + datetime.timedelta(days=7)
print("7 days later:", seven_days_later)

# Add 7 hours
seven_hours_later = current_moment + datetime.timedelta(hours=7)
print("7 hours later:", seven_hours_later)

# Difference between two datetime moments
diff = seven_days_later - current_moment
print("Difference:", diff)
```

**Output:**

```text
7 days later: 2026-09-16 12:00:00
7 hours later: 2026-09-09 19:00:00
Difference: 7 days, 0:00:00
```

---

## 6. Timezones: Naive vs. Aware Datetimes

One of the most critical concepts to understand in date and time programming is the difference between **Naive** and **Aware** datetime objects:

- **Naive Datetime**: Contains a date and time, but has **NO timezone information attached**. It does not know if it represents New York time, London time, Tokyo time, or UTC. It's just a number on a wall clock.
- **Aware Datetime**: Contains explicit timezone information. It knows its exact offset from Universal Coordinated Time (UTC) and can be safely converted to any timezone in the world.

### Current Time: `today()`, `now()`, and `utcnow()`

There are three ways beginners often try to get the current date and time:

```python
import datetime

dt_today = datetime.datetime.today()
dt_now = datetime.datetime.now()
dt_utcnow = datetime.datetime.utcnow()

print("today: ", dt_today)
print("now:   ", dt_now)
print("utcnow:", dt_utcnow)
```

**Output:**

```text
today:  2026-09-09 00:39:19.748494
now:    2026-09-09 00:39:19.748521
utcnow: 2026-09-08 19:09:19.748602
```

### Important Warning: `utcnow()` is Deprecated!

In modern Python, running `datetime.datetime.utcnow()` prints a deprecation warning:

```text
DeprecationWarning: datetime.datetime.utcnow() is deprecated and scheduled for removal in a future version.
Use timezone-aware objects to represent datetimes in UTC: datetime.datetime.now(datetime.UTC).
```

**Why was it deprecated?** Because `utcnow()` returns a **naive** datetime! Even though the numbers reflect UTC time, the object has no timezone attached, making it very easy to accidentally mix local and UTC times in calculations.

### The Modern Way: UTC Aware Datetime

Python now has built-in UTC timezone support via `datetime.timezone.utc`. You pass this into `datetime.datetime.now()`:

```python
import datetime

# Create a timezone-aware UTC datetime
dt_utc = datetime.datetime.now(datetime.timezone.utc)
print(dt_utc)
```

**Output:**

```text
2026-09-08 19:10:39.965975+00:00
```

Notice the `+00:00` at the end! That offset indicates that this object is timezone-aware and set to UTC (+0 hours offset).

---

## 7. Working with Timezones Using `pytz`

While standard Python includes basic UTC offsets, third-party libraries like `pytz` have long been used to manage the world's full database of named timezones (including complex Daylight Saving Time rules).

If you are using `pytz` (installable via `pip install pytz`), here is how to work with it:

### Viewing Available Timezones

`pytz.all_timezones` is a list containing hundreds of standard IANA timezone names:

```python
import pytz

# Print the first 5 available timezones
print(pytz.all_timezones[:5])
```

**Output:**

```text
['Africa/Abidjan', 'Africa/Accra', 'Africa/Addis_Ababa', 'Africa/Algiers', 'Africa/Asmara']
```

### Getting Current Time in UTC with `pytz`

```python
import datetime
import pytz

dt_utc_now = datetime.datetime.now(tz=pytz.UTC)
print(dt_utc_now)
```

**Output:**

```text
2026-09-08 19:28:08.531184+00:00
```

### Converting From One Timezone to Another (`astimezone`)

Once you have a timezone-aware datetime, you can convert it to any other timezone in the world with `.astimezone()`:

```python
import datetime
import pytz

# Current time in UTC
dt_utc_now = datetime.datetime.now(tz=pytz.UTC)

# Convert UTC to US Eastern time
eastern_tz = pytz.timezone('US/Eastern')
dt_eastern = dt_utc_now.astimezone(eastern_tz)

print("UTC:       ", dt_utc_now)
print("US Eastern:", dt_eastern)
```

**Output:**

```text
UTC:        2026-09-08 19:28:08.531184+00:00
US Eastern: 2026-09-08 15:28:08.531184-04:00
```

### Localizing a Naive Datetime (`localize`)

If you have a naive datetime (one that was created without timezone information) and you know which timezone it belongs to, use the timezone's `.localize()` method to attach that timezone:

```python
import datetime
import pytz

# Start with a naive local time
naive_dt = datetime.datetime.now()
print("Naive:    ", naive_dt)

# Localize it to US Eastern
eastern_tz = pytz.timezone('US/Eastern')
localized_dt = eastern_tz.localize(naive_dt)

print("Localized:", localized_dt)
```

**Output:**

```text
Naive:     2026-09-09 00:56:28.753672
Localized: 2026-09-09 00:56:28.753672-04:00
```

---

## 8. Formatting and Parsing Dates: `strftime` and `strptime`

Dates in code need to be displayed to humans as pretty text strings (formatting), and strings received from web forms or API requests need to be turned back into Python `datetime` objects (parsing).

Here is a simple mnemonic to never mix them up:

- **`strftime`**: **str**ing **f**ormat time (Datetime ➡️ String)
- **`strptime`**: **str**ing **p**arse time (String ➡️ Datetime)

### 1. ISO 8601 Format (`.isoformat()`)

The international standard for exchanging date and time text across the internet (like in REST APIs) is ISO 8601:

```python
import datetime
import pytz

dt = datetime.datetime.now(tz=pytz.UTC)
print(dt.isoformat())
```

**Output:**

```text
2026-09-08T19:28:08.531184+00:00
```

### 2. Formatting Datetime to String: `strftime`

Use `.strftime()` with format directives (placeholders) to build custom date text:

```python
import datetime

dt = datetime.datetime(2026, 9, 8, 19, 28, 8)

# Format as "September 08, 2026"
formatted_str = dt.strftime('%B %d, %Y')
print(formatted_str)
```

**Output:**

```text
September 08, 2026
```

Common format directives:

- `%Y`: Year with century (e.g., `2026`)
- `%y`: Year without century (e.g., `26`)
- `%B`: Full month name (e.g., `September`)
- `%b`: Abbreviated month name (e.g., `Sep`)
- `%m`: Month as zero-padded number (`01` to `12`)
- `%d`: Day of the month zero-padded (`01` to `31`)
- `%H`: Hour in 24-hour format (`00` to `23`)
- `%I`: Hour in 12-hour format (`01` to `12`)
- `%p`: AM or PM designation
- `%M`: Minute (`00` to `59`)
- `%S`: Second (`00` to `59`)
- `%A`: Full weekday name (e.g., `Wednesday`)
- `%a`: Abbreviated weekday name (e.g., `Wed`)

Another example combining several directives:

```python
import datetime

dt = datetime.datetime(2026, 9, 8, 14, 30, 0)
print(dt.strftime("%A, %B %d, %Y at %I:%M %p"))
```

**Output:**

```text
Tuesday, September 08, 2026 at 02:30 PM
```

### 3. Parsing String into Datetime: `strptime`

When you receive a date string from user input or a file, use `datetime.datetime.strptime(string, format)` to convert it into a real `datetime` object:

```python
import datetime

date_time_str = 'September 08, 2026'

# The format pattern must match the input string pattern exactly
date_from_string = datetime.datetime.strptime(date_time_str, '%B %d, %Y')
print("Parsed datetime object:", date_from_string)
print("Object type:           ", type(date_from_string))
```

**Output:**

```text
Parsed datetime object: 2026-09-08 00:00:00
Object type:            <class 'datetime.datetime'>
```

Once parsed, you can perform any date arithmetic, access `.year` and `.month`, or reformat it however you like!

---

## 9. Popular Real-World Use Cases (Bonus Topics)

Beyond the fundamentals, here are practical, real-world patterns you will encounter when building web apps, scripts, and automation pipelines.

### Use Case 1: The Modern Standard Library `zoneinfo` (Python 3.9+)

Starting with Python 3.9, Python introduced `zoneinfo` into its standard library! That means **you no longer need `pytz`** to work with named timezones (like `'America/New_York'` or `'Asia/Kolkata'`).

```python
from datetime import datetime
from zoneinfo import ZoneInfo

# Get current time in Tokyo
tokyo_time = datetime.now(ZoneInfo("Asia/Tokyo"))
print("Tokyo time:   ", tokyo_time)

# Convert to New York time
ny_time = tokyo_time.astimezone(ZoneInfo("America/New_York"))
print("New York time:", ny_time)
```

**Output:**

```text
Tokyo time:    2026-09-09 04:30:15.123456+09:00
New York time: 2026-09-08 15:30:15.123456-04:00
```

### Use Case 2: Working with Unix Timestamps (Epoch Time)

Computers and databases frequently store time as a single integer or float: the number of seconds that have passed since January 1, 1970 (called the Unix Epoch).

#### Converting a `datetime` to a Unix timestamp (`.timestamp()`):

```python
import datetime

now = datetime.datetime.now()
epoch_timestamp = now.timestamp()
print("Unix Timestamp:", epoch_timestamp)
```

**Output:**

```text
Unix Timestamp: 1788915600.0
```

#### Converting a Unix timestamp back into a `datetime` (`fromtimestamp`):

```python
import datetime

timestamp = 1788915600.0
dt = datetime.datetime.fromtimestamp(timestamp)
print("Datetime from timestamp:", dt)
```

**Output:**

```text
Datetime from timestamp: 2026-09-09 01:00:00
```

### Use Case 3: Comparing Dates (Past, Future & Expiration Checks)

You can directly compare `date` and `datetime` objects using standard comparison operators (`<`, `<=`, `>`, `>=`, `==`):

```python
import datetime

today = datetime.date.today()
subscription_expiry = datetime.date(2026, 12, 31)

if today > subscription_expiry:
    print("Your subscription has expired! Please renew.")
else:
    days_left = (subscription_expiry - today).days
    print(f"Subscription active! You have {days_left} days remaining.")
```

**Output:**

```text
Subscription active! You have 113 days remaining.
```

### Use Case 4: Calculating Someone's Exact Age from Birthday

A common task in user profile systems is calculating age in full years:

```python
import datetime

def calculate_age(birth_date):
    today = datetime.date.today()
    # Subtract 1 if the birthday hasn't occurred yet this calendar year
    has_birthday_occurred = (today.month, today.day) >= (birth_date.month, birth_date.day)
    age = today.year - birth_date.year - (not has_birthday_occurred)
    return age

birthday = datetime.date(2000, 5, 15)
print(f"Age: {calculate_age(birthday)} years old")
```

**Output:**

```text
Age: 26 years old
```

### Use Case 5: Iterating Through a Range of Dates (Date Loops)

In data analysis, automation, or web scraping, you often need to loop day-by-day between a start date and an end date:

```python
import datetime

start_date = datetime.date(2026, 9, 1)
end_date = datetime.date(2026, 9, 5)
one_day = datetime.timedelta(days=1)

current_date = start_date
while current_date <= end_date:
    print(f"Processing data for: {current_date}")
    current_date += one_day
```

**Output:**

```text
Processing data for: 2026-09-01
Processing data for: 2026-09-02
Processing data for: 2026-09-03
Processing data for: 2026-09-04
Processing data for: 2026-09-05
```

---

## 10. Quick Reference & Summary

Here is a quick recap of the core datetime tools and their functions:

- **`datetime.date(YYYY, M, D)`**: Stores only the calendar date. Remember: no leading zeros like `09` and no string quotes!
- **`datetime.date.today()`**: Gets today's local date.
- **`datetime.time(h, m, s, ms)`**: Stores only the time of day.
- **`datetime.datetime(YYYY, M, D, h, m, s)`**: Combines date and time into one object.
- **`datetime.timedelta(days=..., hours=...)`**: Represents a duration. Used for date math (`date + timedelta`, `date1 - date2`).
- **`datetime.datetime.now(datetime.timezone.utc)`**: The modern, safe way to get the current UTC time with timezone awareness.
- **`dt.strftime('%B %d, %Y')`**: Converts a datetime object into a formatted string (**f**ormat).
- **`datetime.datetime.strptime(str, format)`**: Parses a date string into a datetime object (**p**arse).
- **`zoneinfo.ZoneInfo("Region/City")`**: Python 3.9+'s built-in way to handle IANA timezones without needing extra packages.
