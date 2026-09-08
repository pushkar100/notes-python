# Python's `os` Module: The Complete Beginner's Guide

- [1. Getting Started with the `os` Module](#1-getting-started-with-the-os-module)
- [2. Knowing Where You Are: Current Working Directory](#2-knowing-where-you-are-current-working-directory)
- [3. Viewing Folder Contents (`os.listdir`)](#3-viewing-folder-contents-oslistdir)
- [4. Creating and Deleting Folders](#4-creating-and-deleting-folders)
- [5. Renaming Files and Folders (`os.rename`)](#5-renaming-files-and-folders-osrename)
- [6. Inspecting File and Folder Information (`os.stat`)](#6-inspecting-file-and-folder-information-osstat)
- [7. Exploring Directory Trees with `os.walk`](#7-exploring-directory-trees-with-oswalk)
- [8. Working with Environment Variables (`os.environ`)](#8-working-with-environment-variables-osenviron)
- [9. Mastering File Paths with `os.path`](#9-mastering-file-paths-with-ospath)
- [10. Popular Additional Use Cases of the `os` Module](#10-popular-additional-use-cases-of-the-os-module)
- [11. Quick Reference Cheatsheet](#11-quick-reference-cheatsheet)

When you use your computer, you do things like click on folders, create new directories, check file sizes, rename files, or move documents around.

The built-in Python **`os` module** is your code's way of doing all those exact same everyday computer tasks automatically. Think of it as a remote control that lets your Python script communicate directly with your computer's Operating System (Windows, macOS, or Linux).

Best of all, you don't need to install anything using `pip` because the `os` module comes pre-installed with standard Python!

## 1. Getting Started with the `os` Module

To start using the module, all you need to do is import it at the top of your Python file or Jupyter Notebook:

```python
import os
```

Once imported, you have access to dozens of functions designed to interact with your file system, files, directories, and system environment.

---

## 2. Knowing Where You Are: Current Working Directory

Whenever your Python script runs, it is always "standing" in a specific folder on your computer. This location is called the **Current Working Directory (CWD)**.

### Checking Where You Are (`os.getcwd`)

To ask Python "Where am I right now?", use `os.getcwd()` (which stands for **get** **c**urrent **w**orking **d**irectory):

```python
import os

current_dir = os.getcwd()
print(current_dir)
```

**Example Output:**

```text
/Users/pushkar/Desktop/RESTApi
```

### Changing Your Location (`os.chdir`)

If you want your script to move to another folder (just like double-clicking a folder in your file explorer), use `os.chdir()` (stands for **ch**ange **dir**ectory):

```python
import os

# Move to the Desktop folder
os.chdir('/Users/pushkar/Desktop')

# Verify our new location
print(os.getcwd())
```

**Example Output:**

```text
/Users/pushkar/Desktop
```

---

## 3. Viewing Folder Contents (`os.listdir`)

To see what files and folders live inside a directory, use `os.listdir()`.

### Listing the Current Directory

If you don't pass any argument inside the parentheses, it lists everything in your current working directory:

```python
import os

items = os.listdir()
print(items)
```

**Example Output:**

```text
['learning-os', 'Resume', 'numpy', 'RESTApi', 'Interview.md', 'practice', 'requirements.txt']
```

### Listing a Specific Directory

You can also pass a folder name or full path to peek inside another folder without moving to it:

```python
import os

numpy_files = os.listdir('numpy')
print(numpy_files)
```

**Example Output:**

```text
['requirements.txt', 'numpy.ipynb', '.venv', 'numpy.md']
```

---

## 4. Creating and Deleting Folders

The `os` module gives you tools to create folders and delete them when they are no longer needed.

### Creating a Single Folder (`os.mkdir`)

Use `os.mkdir()` (**m**a**k**e **dir**ectory) to create one new folder:

```python
import os

os.mkdir('learning-os')
print(os.listdir('learning-os'))
```

**Example Output:**

```text
[]
```

### Deleting a Single Empty Folder (`os.rmdir`)

Use `os.rmdir()` (**r**e**m**ove **dir**ectory) to delete a folder:

```python
import os

os.rmdir('learning-os')
```

> **Note for Beginners:** `os.rmdir()` only works on **empty** folders! This protects you from accidentally wiping out valuable files.

### Creating Deep / Nested Folders at Once (`os.makedirs`)

What if you want to create a folder inside another folder that doesn't exist yet (like `nested/new-folder`)? `os.mkdir()` will fail if the parent folder doesn't exist, but `os.makedirs()` will create all intermediate parent folders automatically:

```python
import os

os.makedirs('nested/new-folder')
print(os.listdir('nested'))
```

**Example Output:**

```text
['new-folder']
```

### Deleting Deep Empty Folders (`os.removedirs`)

Similarly, `os.removedirs()` deletes child folders and cleans up empty parent folders along the path:

```python
import os

os.removedirs('nested/new-folder')
```

---

## 5. Renaming Files and Folders (`os.rename`)

To rename a file or a folder, use `os.rename(source, destination)`.

```python
import os

# Create a folder called 'testing'
os.mkdir('testing')

# Rename 'testing' to 'new-testing'
os.rename('testing', 'new-testing')

print('new-testing' in os.listdir())
```

**Example Output:**

```text
True
```

---

## 6. Inspecting File and Folder Information (`os.stat`)

Every file and folder on your operating system holds metadata—like its size, permissions, and when it was last modified. You can view this using `os.stat()`.

### Getting the Stat Object

```python
import os

info = os.stat('new-testing')
print(info)
```

**Example Output:**

```text
os.stat_result(st_mode=16877, st_ino=22412450, st_dev=16777229, st_nlink=2, st_uid=501, st_gid=20, st_size=64, st_atime=1788890991, st_mtime=1788890991, st_ctime=1788891005)
```

### Reading the File/Folder Size (`st_size`)

```python
import os

size_in_bytes = os.stat('new-testing').st_size
print(f"Size: {size_in_bytes} bytes")
```

**Example Output:**

```text
Size: 64 bytes
```

### Reading Human-Readable Modification Times (`st_mtime`)

The attribute `st_mtime` gives the modification time as a raw computer timestamp (seconds since January 1, 1970). We can convert it into human-friendly date and time using Python's `datetime` module:

```python
import os
from datetime import datetime

mod_timestamp = os.stat('new-testing').st_mtime
human_readable_time = datetime.fromtimestamp(mod_timestamp)

print(f"Last modified: {human_readable_time}")
```

**Example Output:**

```text
Last modified: 2026-09-08 23:39:51.770517
```

---

## 7. Exploring Directory Trees with `os.walk`

If you have a folder structure with lots of nested folders, subfolders, and files, checking each folder manually is tedious.

`os.walk()` acts like an automatic explorer that visits every single corner of a directory tree from top to bottom. For each folder it visits, it gives you 3 things:

1. `dirpath`: The current folder path.
2. `dirnames`: A list of subdirectories inside this folder.
3. `dirfiles`: A list of files inside this folder.

```python
import os

for dirpath, dirnames, dirfiles in os.walk(os.getcwd()):
    print(f"Directory path: {dirpath}")
    print(f"Sub-Directory names: {dirnames}")
    print(f"Directory files: {dirfiles}\n")
```

**Example Output:**

```text
Directory path: /Users/pushkar/Desktop/my_project
Sub-Directory names: ['app', 'tests']
Directory files: ['README.md', 'requirements.txt']

Directory path: /Users/pushkar/Desktop/my_project/app
Sub-Directory names: []
Directory files: ['__init__.py', 'main.py']

Directory path: /Users/pushkar/Desktop/my_project/tests
Sub-Directory names: []
Directory files: ['test_app.py']
```

---

## 8. Working with Environment Variables (`os.environ`)

Environment variables are system-wide key-value pairs stored by your operating system. They are often used to store user profile paths, system configurations, and sensitive credentials like API keys without hardcoding them into scripts.

### Reading an Environment Variable (`os.environ.get`)

To safely read an environment variable, use `os.environ.get('VARIABLE_NAME')`:

```python
import os

home_folder = os.environ.get('HOME')
print(home_folder)
```

**Example Output:**

```text
/Users/pushkar
```

Using `.get()` is recommended because if the variable doesn't exist, Python will cleanly return `None` rather than crashing with an error.

---

## 9. Mastering File Paths with `os.path`

Path handling is one of the most common sources of bugs for beginners. Different operating systems use different slashes (Windows uses `\`, while macOS and Linux use `/`). The `os.path` submodule takes care of this cross-platform compatibility automatically.

### Why String Concatenation (`+`) Is a Bad Idea

If you try to stitch paths together with strings using `+`, it is very easy to miss a slash:

```python
import os

# Accidentally forgetting the slash:
path_to_new_file = os.environ.get('HOME') + 'new-file.txt'
print(path_to_new_file)
```

**Output (Buggy!):**

```text
/Users/pushkarnew-file.txt
```

### Joining Paths Correctly (`os.path.join`)

`os.path.join()` inserts the correct slashes automatically depending on whether your script is running on Windows, macOS, or Linux:

```python
import os

path_to_new_file = os.path.join(os.environ.get('HOME'), 'new-file.txt')
print(path_to_new_file)
```

**Output (Correct!):**

```text
/Users/pushkar/new-file.txt
```

### Extracting File and Folder Names

Given a path like `/some/temp/folder/my_file.txt`:

1. **`os.path.basename()`**: Extracts just the final file name.
2. **`os.path.dirname()`**: Extracts just the folder directory path.
3. **`os.path.split()`**: Gives you both as a tuple `(dirname, basename)`.

```python
import os

full_path = '/some/temp/folder/my_file.txt'

print("Base name:", os.path.basename(full_path))
print("Directory name:", os.path.dirname(full_path))
print("Split into both:", os.path.split(full_path))
```

**Example Output:**

```text
Base name: my_file.txt
Directory name: /some/temp/folder
Split into both: ('/some/temp/folder', 'my_file.txt')
```

### Splitting File Name and Extension (`os.path.splitext`)

When you want to know what type of file you're dealing with (e.g. `.txt`, `.csv`, `.pdf`), `os.path.splitext()` separates the file path from its extension:

```python
import os

file_path = '/Users/pushkar/Desktop/RESTApi/requirements.txt'
root, extension = os.path.splitext(file_path)

print("Root path:", root)
print("File extension:", extension)
```

**Example Output:**

```text
Root path: /Users/pushkar/Desktop/RESTApi/requirements
File extension: .txt
```

### Checking Existence: Files vs. Folders

Before opening or deleting a file, it's good practice to verify that it actually exists:

```python
import os

# Check if anything (file or folder) exists
print(os.path.exists('/Users/pushkar/Desktop/RESTApi'))
print(os.path.exists('/some/fake/folder'))

# Check if it specifically is a file
print(os.path.isfile('/Users/pushkar/Desktop/RESTApi/requirements.txt'))

# Check if it specifically is a directory (folder)
print(os.path.isdir('/Users/pushkar/Desktop/RESTApi'))
```

**Example Output:**

```text
True
False
True
True
```

### Exploring What Else `os.path` Can Do (`dir(os.path)`)

You can inspect all available functions inside `os.path` at any time using Python's built-in `dir()` function:

```python
import os

print(dir(os.path))
```

**Example Output:**

```text
['abspath', 'basename', 'commonpath', 'dirname', 'exists', 'getatime', 'getctime', 'getmtime', 'getsize', 'isabs', 'isdir', 'isfile', 'islink', 'join', 'realpath', 'relpath', 'split', 'splitext', ...]
```

---

## 10. Popular Additional Use Cases of the `os` Module

While the notebook covered the fundamentals of navigating folders and inspecting paths, here are several other widely used functions from the `os` module that every Python developer should know:

### 1. Deleting Files (`os.remove`)

We learned that `os.rmdir()` only deletes empty directories. To delete an actual file, use `os.remove()` (or its alias `os.unlink()`):

```python
import os

# Create a sample file
with open('temp_demo.txt', 'w') as f:
    f.write('Temporary data')

# Check that it exists
print("File exists before delete:", os.path.exists('temp_demo.txt'))

# Delete the file
os.remove('temp_demo.txt')

print("File exists after delete:", os.path.exists('temp_demo.txt'))
```

**Example Output:**

```text
File exists before delete: True
File exists after delete: False
```

### 2. Setting and Managing Environment Variables (`os.environ` & `os.getenv`)

You can also create or update environment variables for your script's current running session:

```python
import os

# Set a custom environment variable
os.environ['DATABASE_PORT'] = '5432'

# Retrieve it with os.getenv (allows setting a fallback default if not found)
port = os.getenv('DATABASE_PORT', '8000')
api_key = os.getenv('SECRET_API_KEY', 'default_mock_key')

print(f"Database port: {port}")
print(f"API key: {api_key}")
```

**Example Output:**

```text
Database port: 5432
API key: default_mock_key
```

### 3. Detecting Operating System Type (`os.name`)

If you want your code to act differently depending on whether it runs on Windows or a Unix-like system (macOS / Linux):

```python
import os

print(f"OS type: {os.name}")

if os.name == 'posix':
    print("Running on macOS or Linux!")
elif os.name == 'nt':
    print("Running on Windows!")
```

**Example Output (on macOS):**

```text
OS type: posix
Running on macOS or Linux!
```

### 4. Getting Full Absolute Paths (`os.path.abspath`)

If you have a relative path like `requirements.txt` or `.` (current folder), `os.path.abspath()` resolves it to the full absolute path from root:

```python
import os

abs_path = os.path.abspath('requirements.txt')
print(abs_path)
```

**Example Output:**

```text
/Users/pushkar/Desktop/RESTApi/requirements.txt
```

### 5. Getting File Size Directly (`os.path.getsize`)

Instead of calling `os.stat('filename').st_size`, you can use the convenient shortcut `os.path.getsize()`:

```python
import os

size = os.path.getsize('requirements.txt')
print(f"Size of requirements.txt: {size} bytes")
```

**Example Output:**

```text
Size of requirements.txt: 249 bytes
```

### 6. Executing System Commands (`os.system`)

You can run terminal / command line commands right from Python:

```python
import os

# Run a simple echo command in the terminal
return_code = os.system("echo 'Hello from the terminal!'")
print(f"Command finished with return code: {return_code}")
```

**Example Output:**

```text
Hello from the terminal!
Command finished with return code: 0
```

> **Tip:** For advanced command execution and capturing terminal output, Python's modern `subprocess` module is recommended, but `os.system()` remains popular for quick commands.

---

## 11. Quick Reference Cheatsheet

Here is a quick summary list of the most common `os` operations:

- **Get current folder**: `os.getcwd()`
- **Change folder**: `os.chdir('/path/to/folder')`
- **List contents**: `os.listdir('.')`
- **Create one folder**: `os.mkdir('data')`
- **Create nested folders**: `os.makedirs('data/raw/csv')`
- **Delete empty folder**: `os.rmdir('data')`
- **Delete empty folder tree**: `os.removedirs('data/raw/csv')`
- **Delete a file**: `os.remove('sample.txt')`
- **Rename file or folder**: `os.rename('old.txt', 'new.txt')`
- **File/folder stats**: `os.stat('data.csv').st_size`
- **Traverse directory tree**: `for root, dirs, files in os.walk('.'):`
- **Read environment variable**: `os.environ.get('HOME')`
- **Join path safely**: `os.path.join('folder', 'file.txt')`
- **Get file name**: `os.path.basename('/a/b/c.txt')` (gives `'c.txt'`)
- **Get folder path**: `os.path.dirname('/a/b/c.txt')` (gives `'/a/b'`)
- **Split path & name**: `os.path.split('/a/b/c.txt')` (gives `('/a/b', 'c.txt')`)
- **Split extension**: `os.path.splitext('pic.jpg')` (gives `('pic', '.jpg')`)
- **Check if path exists**: `os.path.exists('file.txt')`
- **Check if path is file**: `os.path.isfile('file.txt')`
- **Check if path is folder**: `os.path.isdir('my_folder')`
