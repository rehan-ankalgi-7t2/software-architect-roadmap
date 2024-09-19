# Polymorphism

Polymorphism is a core concept of object-oriented programming (OOP) that allows one object to take multiple forms. In Java, polymorphism enables methods to perform different tasks based on the object that calls them. Polymorphism is primarily achieved in Java in two ways:

1. **Compile-time polymorphism (Method Overloading)**
2. **Run-time polymorphism (Method Overriding)**

Let's discuss both in detail with examples.

---

### 1. **Compile-time Polymorphism (Method Overloading)**

**Method overloading** allows multiple methods in a class to have the same name but different parameter lists (i.e., number or types of parameters). The method to be called is determined at compile time based on the method signature.

#### Example:

```java
class Calculator {
    // Method to add two integers
    public int add(int a, int b) {
        return a + b;
    }

    // Overloaded method to add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Overloaded method to add two double values
    public double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        // Calling the method with two integers
        System.out.println(calc.add(10, 20)); // Output: 30
        
        // Calling the method with three integers
        System.out.println(calc.add(10, 20, 30)); // Output: 60
        
        // Calling the method with two double values
        System.out.println(calc.add(10.5, 20.5)); // Output: 31.0
    }
}
```

In this example, the `add()` method is overloaded, and Java selects the appropriate method based on the number and types of arguments at compile time.

---

### 2. **Run-time Polymorphism (Method Overriding)**

**Method overriding** occurs when a subclass provides a specific implementation of a method that is already defined in its superclass. This is also known as **dynamic polymorphism** because the method to be called is determined at runtime based on the object type.

#### Example:

```java
class Animal {
    // Overridden method
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // Dog's specific implementation of sound()
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    // Cat's specific implementation of sound()
    @Override
    public void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        // Polymorphism at work
        Animal myAnimal = new Animal();  // Animal reference and object
        Animal myDog = new Dog();        // Animal reference, but Dog object
        Animal myCat = new Cat();        // Animal reference, but Cat object
        
        myAnimal.sound();  // Output: Animal makes a sound
        myDog.sound();     // Output: Dog barks
        myCat.sound();     // Output: Cat meows
    }
}
```

In this example, the `sound()` method is overridden in both the `Dog` and `Cat` classes. Although the reference type is `Animal`, the actual method that is called depends on the runtime object (`Dog` or `Cat`). This demonstrates runtime polymorphism.

---

### Key Points:

- **Method Overloading** (Compile-time polymorphism):
  - Same method name but different parameter lists.
  - Resolved during compilation.
  - Can be applied in the same class or between parent-child classes.

- **Method Overriding** (Run-time polymorphism):
  - Same method name and parameter list in both the superclass and subclass.
  - Resolved at runtime based on the actual object.
  - Requires an inheritance relationship.

### Benefits of Polymorphism:

1. **Code Reusability**: It allows you to use the same method for different types of objects, reducing code duplication.
2. **Flexibility**: You can write more generic and flexible code that can work with objects of different classes, enhancing maintainability.
3. **Scalability**: You can add new functionality easily by extending classes without modifying existing code.

Polymorphism is a powerful concept in Java that helps in building flexible, scalable, and maintainable systems.