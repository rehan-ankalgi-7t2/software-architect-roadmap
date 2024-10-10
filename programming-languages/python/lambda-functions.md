# **Lambda Functions in Python**

Lambda functions, also known as anonymous functions, are a concise way to define small, unnamed functions in Python. They are often used for simple tasks that don't require a full function definition.

**Syntax:**

**Python**

`lambda arguments: expression`

- `arguments`: A comma-separated list of arguments.
- `expression`: The expression to be evaluated.

**Example:**

**Python**

```python
double = lambda x: x * 2
result = double(5)
print(result)  # Output: 10
```

In this example, `lambda x: x * 2` defines a lambda function that takes an argument `x` and returns its double.

**Common Use Cases:**

- **Sorting lists:**
    
    **Python**
    
    ```python
    numbers = [3, 1, 4, 1, 5, 9]
    numbers.sort(key=lambda x: x % 2)
    print(numbers)  # Output: [1, 1, 5, 9, 3, 4]
    ```
    
- **Filtering lists:**
    
    **Python**
    
    ```python
    numbers = [1, 2, 3, 4, 5]
    even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
    print(even_numbers)  # Output: [2, 4]
    ```
    
- **Mapping values:**
    
    **Python**
    
    ```python
    numbers = [1, 2, 3, 4, 5]
    squared_numbers = list(map(lambda x: x * x, numbers))
    print(squared_numbers)  # Output: [1, 4, 9, 16, 25]
    ```
    

**Key Points:**

- Lambda functions are expressions, not statements.
- They can have multiple arguments but can only return a single expression.
- They are often used for short, one-line functions.
- They can be assigned to variables or passed as arguments to other functions.

**When to Use Lambda Functions:**

- For simple, one-line functions that are used only once.
- As arguments to functions that expect functions as input (e.g., `map`, `filter`, `sorted`).
- To create anonymous functions on the fly.

While lambda functions can be concise and useful, it's important to use them judiciously. If a function becomes complex or is used multiple times, it's often better to define a named function for readability and maintainability.