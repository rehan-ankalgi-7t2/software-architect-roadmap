Object-Oriented Programming (OOP) in Dart

Dart follows the principles of Object-Oriented Programming (OOP), which include:

1. Encapsulation – Data hiding using classes and private members.


2. Inheritance – Reusing and extending classes.


3. Polymorphism – Using overridden methods for flexibility.


4. Abstraction – Hiding implementation details using abstract classes and interfaces.




---

1. Classes & Objects

In Dart, a class is a blueprint for creating objects.

Defining a Class & Creating Objects

class Car {
  String brand = "Toyota";
  int speed = 100;

  void showDetails() {
    print("Brand: $brand, Speed: $speed km/h");
  }
}

void main() {
  Car myCar = Car(); // Creating an object
  myCar.showDetails(); // Brand: Toyota, Speed: 100 km/h
}


---

2. Constructors in Dart

A constructor is a special function used to initialize an object.

Default Constructor

class Person {
  String name;
  int age;

  Person() {
    name = "John Doe";
    age = 25;
    print("Person Created: $name, Age: $age");
  }
}

void main() {
  Person p1 = Person(); // Calls the constructor
}

Parameterized Constructor

class Employee {
  String name;
  int salary;

  Employee(this.name, this.salary); // Constructor with parameters

  void show() {
    print("Employee: $name, Salary: $salary");
  }
}

void main() {
  Employee emp = Employee("Alice", 50000);
  emp.show();
}

Named Constructor

class Laptop {
  String brand;
  int price;

  Laptop(this.brand, this.price);

  // Named Constructor
  Laptop.discounted(String brand) {
    this.brand = brand;
    this.price = 30000; // Fixed discount price
  }
}

void main() {
  Laptop laptop1 = Laptop("HP", 50000);
  Laptop laptop2 = Laptop.discounted("Dell");

  print("${laptop1.brand}: ${laptop1.price}"); // HP: 50000
  print("${laptop2.brand}: ${laptop2.price}"); // Dell: 30000
}


---

3. Encapsulation (Private Members & Getters/Setters)

Encapsulation is data hiding using private fields (prefix _) and exposing them through getters and setters.

class BankAccount {
  String _accountNumber; // Private variable
  double _balance;

  BankAccount(this._accountNumber, this._balance);

  // Getter
  double get balance => _balance;

  // Setter
  set deposit(double amount) {
    _balance += amount;
  }

  void withdraw(double amount) {
    if (amount <= _balance) {
      _balance -= amount;
    } else {
      print("Insufficient balance");
    }
  }
}

void main() {
  BankAccount acc = BankAccount("123456789", 5000);
  acc.deposit = 2000; // Using setter
  acc.withdraw(1000);
  print("Balance: ${acc.balance}"); // Using getter
}


---

4. Inheritance (Extending Classes)

Inheritance allows a class to extend another class and reuse its properties and methods.

class Animal {
  String name;
  Animal(this.name);

  void makeSound() {
    print("$name makes a sound");
  }
}

// Child class extending Animal
class Dog extends Animal {
  Dog(String name) : super(name);

  void bark() {
    print("$name barks");
  }
}

void main() {
  Dog myDog = Dog("Buddy");
  myDog.makeSound(); // Buddy makes a sound
  myDog.bark();      // Buddy barks
}

Overriding Parent Class Methods

class Vehicle {
  void start() {
    print("Vehicle is starting...");
  }
}

class Car extends Vehicle {
  @override
  void start() {
    print("Car is starting...");
  }
}

void main() {
  Car myCar = Car();
  myCar.start(); // Car is starting...
}


---

5. Polymorphism (Method Overriding & Method Overloading)

Polymorphism allows overriding methods and using the same method name with different implementations.

Method Overriding

class Shape {
  void draw() {
    print("Drawing a shape");
  }
}

class Circle extends Shape {
  @override
  void draw() {
    print("Drawing a Circle");
  }
}

void main() {
  Shape s = Circle();
  s.draw(); // Drawing a Circle
}

Method Overloading (Optional Parameters for Overloading)

Dart doesn’t support traditional method overloading, but we can achieve similar behavior using optional parameters.

class Calculator {
  void add(int a, int b, [int? c]) {
    if (c != null) {
      print("Sum: ${a + b + c}");
    } else {
      print("Sum: ${a + b}");
    }
  }
}

void main() {
  Calculator calc = Calculator();
  calc.add(5, 10);      // Sum: 15
  calc.add(5, 10, 20);  // Sum: 35
}


---

6. Abstraction (Abstract Classes & Interfaces)

Abstraction is achieved using abstract classes and interfaces.

Abstract Classes

An abstract class cannot be instantiated and is meant to be inherited by other classes.

abstract class Animal {
  void makeSound(); // Abstract method (no implementation)
}

class Cat extends Animal {
  @override
  void makeSound() {
    print("Meow Meow");
  }
}

void main() {
  Cat myCat = Cat();
  myCat.makeSound(); // Meow Meow
}

Interfaces (Implicit in Dart)

Dart doesn’t have a special keyword for interfaces. Any class with unimplemented methods acts as an interface.

abstract class Printable {
  void printData();
}

class Book implements Printable {
  @override
  void printData() {
    print("Printing book details...");
  }
}

void main() {
  Book myBook = Book();
  myBook.printData(); // Printing book details...
}


---

7. Mixins (Multiple Inheritance Alternative)

Mixins allow code reuse without class inheritance.

mixin Fly {
  void fly() {
    print("I can fly!");
  }
}

class Bird with Fly {}

void main() {
  Bird sparrow = Bird();
  sparrow.fly(); // I can fly!
}


---

8. Static Members

Static variables and methods belong to the class, not an instance.

class MathUtil {
  static const double pi = 3.14159;

  static double square(double num) {
    return num * num;
  }
}

void main() {
  print(MathUtil.pi); // 3.14159
  print(MathUtil.square(4)); // 16
}


---

Conclusion

Encapsulation → Use private fields & getters/setters

Inheritance → extends keyword for class inheritance

Polymorphism → Method overriding using @override

Abstraction → Use abstract class

Interfaces → Use implements keyword

Mixins → Use mixin for code reuse


Would you like practice exercises for OOP concepts?

