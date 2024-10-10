# **Built-in Modules in Python**

Python comes with a rich set of built-in modules that provide various functionalities without requiring external installations. These modules offer solutions for common tasks, from mathematical operations to file handling and network communication.

Here are some of the most commonly used built-in modules:

**Core Modules:**

- **`os`:** Provides functions for interacting with the operating system, such as file and directory operations.
- **`sys`:** Accesses system-specific parameters and functions, like command-line arguments and version information.
- **`math`:** Offers mathematical functions, including trigonometric, logarithmic, and exponential operations.
- **`random`:** Generates random numbers and performs random selections.
- **`datetime`:** Provides classes for working with dates and times.
- **`json`:** Encodes and decodes JSON data.
- **`pickle`:** Serializes and deserializes Python objects.
- **`urllib`:** Handles URL-related operations, like fetching web pages and making HTTP requests.
- **`re`:** Provides regular expression matching and substitution.
- **`time`:** Provides functions for working with time and dates.
- **`collections`:** Offers specialized container data types, like namedtuples, defaultdict, and OrderedDict.
- **`itertools`:** Provides tools for creating iterators, generating combinations, permutations, and more.

**Standard Library Modules:**

- **`email`:** Handles email processing and sending.
- **`xml`:** Provides tools for working with XML data.
- **`sqlite3`:** A lightweight SQL database engine.
- **`csv`:** Reads and writes CSV files.
- **`tarfile`:** Handles tar archives.
- **`zipfile`:** Handles ZIP archives.

**Additional Modules:**

- **`tkinter`:** A GUI toolkit for creating desktop applications.
- **`unittest`:** A unit testing framework.
- **`doctest`:** A tool for finding bugs in doctest tests embedded in your source code.

**Using Built-in Modules:**

To use a built-in module, import it at the beginning of your Python script:

**Python**

```python
import math

result = math.sqrt(25)
print(result)  # Output: 5.0
```

You can also import specific functions from a module:

**Python**

```python
from math import sqrt

result = sqrt(25)
print(result)  # Output: 5.0
```

By leveraging these built-in modules, you can write more efficient and concise Python code, without the need for external dependencies.