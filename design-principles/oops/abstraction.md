# Abstraction 🤫
![](https://media.licdn.com/dms/image/v2/C4E12AQGUlVop8QEQVg/article-cover_image-shrink_423_752/article-cover_image-shrink_423_752/0/1520122194088?e=1732147200&v=beta&t=XzMNaw58UXyNjg-Yylg4_MHRK88dsz5l6T7d-Tm7gRw)

> Showing essential data / details and hiding other information
- users should not worry about the inner detials and working of the class

## Key Components of Abstraction
1. Interface
2. Implementation

### Implementation using Interface
- **Interface:** Refers to the way sections of code communicate with one another, typically done through methods
- **Implementation:** the implementation of these methods (how these are coded) should be hidden
- if classes are entangled, it creates a `Ripple Effect` where one change causes many more changes
- creating interfaces for classes interaction, ensures that each peice can be developed individually

### Implementation using Abstract classes
- **Abstract classes**: These are classes that cannot be instantiated on their own. 
- They contain abstract methods, which are method signatures without implementations. 
- Subclasses that inherit the abstract class must provide implementations for these abstract methods.

> **Abstraction allows a a program to develop incrementally and prevents it from being entagled and complex**

### Types of Abstraction
1. Data Abstraction
2. Process Abstraction

## Benefits of Abstraction:
1. **Reduces complexity**: By hiding the unnecessary details, abstraction makes the program easier to understand and use.
2. **Increases code reusability**: Abstract methods and classes allow developers to create a general framework that can be reused and extended without modifying the existing code.
3. **Improves maintainability**: Abstraction decouples the interface from the implementation, allowing developers to change how something is done without altering how it is used.

## Example
````Python
from abc import ABC, abstractmethod

# Abstract base class
class Animal(ABC):
    
    @abstractmethod
    def make_sound(self):
        pass
    
    def move(self):
        print("This animal can move.")

# Subclass providing implementation
class Dog(Animal):
    
    def make_sound(self):
        print("Bark")

# Subclass providing implementation
class Cat(Animal):
    
    def make_sound(self):
        print("Meow")

# Instantiate objects
dog = Dog()
dog.make_sound()  # Outputs: Bark
dog.move()        # Outputs: This animal can move.

cat = Cat()
cat.make_sound()  # Outputs: Meow
cat.move()        # Outputs: This animal can move.
````
- `Abstract class Animal`: The class defines the make_sound() method as an abstract method, meaning every subclass must implement this method.
- `Concrete classes (Dog and Cat)`: These classes provide their own specific implementations of the make_sound() method.

## Levels of Abstraction:
Abstraction operates on two levels:

- **High-level abstraction**: This refers to providing a general overview without getting into the details. It defines "what" the object will do, not "how" it will do it.
- **Low-level abstraction**: This deals with the detailed implementation of functionalities, focusing on "how" things will be done.

## Practical Uses:

- **APIs**: When developers use APIs, they are interacting with abstracted services. They don't need to understand how the server processes their requests; they only need to know how to send a request and handle the response.

- **Database Systems**: When using an SQL query to fetch data, users don't need to know how the data is stored on disk; they simply issue queries to retrieve what they need.