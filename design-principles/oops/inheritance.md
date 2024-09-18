# Inheritance
> allows a new class to acquire the properties and behaviors of an existing class. 
- It helps in code reusability and establishes a relationship between classes. 

## Key Concepts of Inheritance:

### 1. **Purpose**:
   - The main objective of inheritance is to promote `code reusability`.
   - It also provides a mechanism for establishing **hierarchical relationships** between classes.

### 2. **Types of Inheritance**:
---
i. **Single Inheritance**: A class inherits from one parent class.
````java
// Parent class
class Animal {
    // Method in the parent class
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// Child class inherits from Animal
class Dog extends Animal {
    // Additional method in the child class
    public void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating an object of Dog class
        Dog dog = new Dog();
        
        // Calling method from parent class
        dog.eat();  // Outputs: This animal eats food.
        
        // Calling method from child class
        dog.bark(); // Outputs: The dog barks.
    }
}
````

---
ii. **Multilevel Inheritance**: A class inherits from a class that also inherits from another class, forming a chain.
```java
// Parent class
class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// Intermediate child class
class Mammal extends Animal {
    public void sleep() {
        System.out.println("This mammal sleeps.");
    }
}

// Child class inherits from Mammal, which also inherits from Animal
class Dog extends Mammal {
    public void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        
        // Inherited from Animal class
        dog.eat();  // Outputs: This animal eats food.
        
        // Inherited from Mammal class
        dog.sleep(); // Outputs: This mammal sleeps.
        
        // Method defined in Dog class
        dog.bark();  // Outputs: The dog barks.
    }
}
```

---
iii. **Hierarchical Inheritance**: Multiple classes inherit from the same parent class.
```java
// Parent class
class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// First child class
class Dog extends Animal {
    public void bark() {
        System.out.println("The dog barks.");
    }
}

// Second child class
class Cat extends Animal {
    public void meow() {
        System.out.println("The cat meows.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Cat cat = new Cat();
        
        dog.eat();  // Outputs: This animal eats food.
        dog.bark(); // Outputs: The dog barks.
        
        cat.eat();  // Outputs: This animal eats food.
        cat.meow(); // Outputs: The cat meows.
    }
}
```


iv. **Multiple Inheritance** (not supported directly in Java with classes): A class inherits from multiple parent classes. Java allows this using interfaces.

### 3. **Advantages of Inheritance**:
   - **Code Reusability**: Allows the reuse of code from an existing class without rewriting it.
   - **Extensibility**: Enables developers to extend or add new functionality to an existing class.
   - **Maintenance**: Makes updating or modifying code easier. Changes to the parent class can automatically affect child classes.
   - **Polymorphism**: Inheritance facilitates polymorphism, allowing objects of different subclasses to be treated as objects of the superclass.

### Example of Method Overriding in Inheritance

Method overriding occurs when a child class provides a specific implementation of a method already defined in its parent class. The method in the child class must have the same signature as in the parent class.

```java
// Parent class
class Animal {
    public void sound() {
        System.out.println("This animal makes a sound.");
    }
}

// Child class overrides the sound method
class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal();
        animal.sound();  // Outputs: This animal makes a sound.
        
        Dog dog = new Dog();
        dog.sound();     // Outputs: The dog barks.
    }
}
```

### `super` Keyword in Java
The `super` keyword is used to refer to the parent class's methods or constructors. It is often used when a subclass wants to call a method or constructor from its parent class.

```java
class Animal {
    public void sound() {
        System.out.println("This animal makes a sound.");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        // Call the parent class method using super
        super.sound();
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();  // Outputs: This animal makes a sound.
                      //           The dog barks.
    }
}
```