# error handling in Python:

**1. Exceptions:**

- Exceptions are objects that represent errors that occur during program execution.
- When an error occurs, an exception is raised, which can be handled using `try` and `except` blocks.

**Example:**

```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
    print("Result:", result)
except ValueError:
    print("Invalid input. Please enter a    number.")
except ZeroDivisionError:
    print("Cannot divide by zero.")
```

**2. Common Built-in Exceptions:**

- `ValueError`: Raised when a built-in operation or function receives an argument of an inappropriate type.
- `TypeError`: Raised when an operation or function is applied to an object of an inappropriate type.
- `NameError`: Raised when a variable or function is referenced that does not exist.
- `IndexError`: Raised when an index is out of range for a list or tuple.
- `KeyError`: Raised when a key is not found in a dictionary.
- `ZeroDivisionError`: Raised when division or modulo operation is performed on a zero divisor.

**3. Custom Exceptions:**

- You can create custom exceptions by defining new classes that inherit from `Exception`.

**Python**

```python
class MyCustomError(Exception):
    pass

try:
    raise MyCustomError("This is a custom error")
except MyCustomError as e:
    print("Caught a custom error:", e)
```

**4. `finally` Block:**

- The `finally` block is executed regardless of whether an exception is raised or not. It's often used for cleanup tasks like closing files or database connections.

**Python**

```python
try:
    file = open("myfile.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found.")
finally:
    if file:
        file.close()
```

**5. Raising Exceptions:**

- You can raise exceptions using the `raise` keyword.

**Python**

```python
if age < 18:
    raise ValueError("You must be at least 18 years old.")
```

**6. Best Practices:**

- Use specific exceptions to provide meaningful error messages.
- Handle exceptions gracefully to prevent unexpected program termination.
- Consider using logging to record exceptions for debugging purposes.
- Avoid using `except:` without specifying a specific exception type, as it can catch unexpected errors.

By effectively handling exceptions in your Python code, you can make your programs more robust and resilient to errors.