## **Dictionaries in Python**

**Dictionaries** in Python are unordered collections of key-value pairs. They provide a flexible and efficient way to store and retrieve data.

**Key Points:**

- **Keys:** Must be unique and immutable (e.g., strings, numbers, tuples).
- **Values:** Can be of any data type.
- **Unordered:** The order of elements in a dictionary is not guaranteed.
- **Mutable:** You can add, remove, or modify elements in a dictionary.

**Creating a Dictionary:**

**Python**

```python
my_dict = {'name': 'Alice', 'age': 30, 'city': 'New York'}
```

**Accessing Values:**

**Python**

```python
name = my_dict['name']  # Output: Alice
```

**Adding or Modifying Elements:**

**Python**

```python
my_dict['country'] = 'USA'  # Add a new key-value pair
my_dict['age'] = 31  # Modify an existing value
```

**Removing Elements:**

**Python**

```python
del my_dict['city']  # Remove a key-value pair
```

**Checking for Key Existence:**

**Python**

```python
if 'country' in my_dict:
    print(my_dict['country'])
else:
    print('Country key not found.')
```

**Iterating Through a Dictionary:**

**Python**

```python
for key, value in my_dict.items():
    print(key, value)
```

**Common Dictionary Methods:**

- `keys()`: Returns a view of the dictionary's keys.
- `values()`: Returns a view of the dictionary's values.
- `items()`: Returns a view of the dictionary's key-value pairs.
- `get(key, default=None)`: Returns the value for the specified key, or a default value if the key doesn't exist.
- `update(other_dict)`: Merges another dictionary into the current one.
- `pop(key, default=None)`: Removes the specified key and returns its value, or a default value if the key doesn't exist.

**Example:**

**Python**

```python
student = {'name': 'Bob', 'grades': {'math': 90, 'science': 85}}
print(student['grades']['math'])  # Output: 90
```

Dictionaries are a powerful tool in Python for organizing and managing data efficiently. By understanding their key features and methods, you can effectively use them in your programming tasks.