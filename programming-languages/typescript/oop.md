TypeScript supports the core **object-oriented programming (OOP)** principles, enhancing JavaScript's prototype-based system with class-based constructs. These principles include **Encapsulation**, **Inheritance**, **Polymorphism**, and **Abstraction**. Let's explore these concepts with examples.

---

## **1. Encapsulation**
Encapsulation restricts access to certain parts of an object and allows selective exposure of properties or methods.

### Example: Encapsulation in TypeScript
```typescript
class User {
    private password: string; // Private property, inaccessible outside the class
    public username: string; // Public property, accessible anywhere

    constructor(username: string, password: string) {
        this.username = username;
        this.password = password;
    }

    // Getter to expose password securely
    getPasswordHint(): string {
        return this.password[0] + '****';
    }
}

const user = new User("Rehan", "secret123");
console.log(user.username); // Rehan
console.log(user.getPasswordHint()); // s****
console.log(user.password); // Error: Property 'password' is private
```

**Modifiers in TypeScript:**
- `public`: Accessible anywhere (default).
- `private`: Accessible only within the class.
- `protected`: Accessible within the class and derived classes.
- `readonly`: Property that can be assigned only during initialization.

---

## **2. Inheritance**
Inheritance allows a class (child) to inherit properties and methods from another class (parent).

### Example: Inheritance in TypeScript
```typescript
class Animal {
    protected species: string;

    constructor(species: string) {
        this.species = species;
    }

    sound() {
        console.log(`${this.species} makes a sound.`);
    }
}

class Dog extends Animal {
    constructor() {
        super("Dog");
    }

    sound() {
        console.log("Dog barks!");
    }
}

const animal = new Animal("Generic Animal");
animal.sound(); // Generic Animal makes a sound.

const dog = new Dog();
dog.sound(); // Dog barks!
```

**Key Points:**
- Use `extends` for inheritance.
- Call the parent class constructor with `super()` in the derived class constructor.

---

## **3. Polymorphism**
Polymorphism allows methods in a class hierarchy to have different implementations based on the calling object.

### Example: Method Overriding
```typescript
class Shape {
    area(): number {
        return 0;
    }
}

class Circle extends Shape {
    radius: number;

    constructor(radius: number) {
        super();
        this.radius = radius;
    }

    area(): number {
        return Math.PI * this.radius * this.radius;
    }
}

class Rectangle extends Shape {
    width: number;
    height: number;

    constructor(width: number, height: number) {
        super();
        this.width = width;
        this.height = height;
    }

    area(): number {
        return this.width * this.height;
    }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(4, 6)];
shapes.forEach((shape) => {
    console.log(`Area: ${shape.area()}`);
});
// Output:
// Area: 78.53981633974483
// Area: 24
```

---

## **4. Abstraction**
Abstraction allows defining a class with methods that are meant to be implemented by derived classes. TypeScript supports abstraction through **abstract classes** and **interfaces**.

### Example: Abstract Classes
```typescript
abstract class Vehicle {
    abstract start(): void; // Abstract method, must be implemented by subclasses
    abstract stop(): void;

    describe(): void {
        console.log("This is a vehicle.");
    }
}

class Car extends Vehicle {
    start(): void {
        console.log("Car starts with a key.");
    }

    stop(): void {
        console.log("Car stops.");
    }
}

const myCar = new Car();
myCar.describe(); // This is a vehicle.
myCar.start(); // Car starts with a key.
myCar.stop(); // Car stops.
```

---

## **5. Interfaces**
Interfaces provide a way to define the structure of an object and enforce the implementation of methods in a class.

### Example: Interfaces
```typescript
interface Flyable {
    fly(): void;
}

interface Swimable {
    swim(): void;
}

class Duck implements Flyable, Swimable {
    fly(): void {
        console.log("Duck flies!");
    }

    swim(): void {
        console.log("Duck swims!");
    }
}

const duck = new Duck();
duck.fly(); // Duck flies!
duck.swim(); // Duck swims!
```

**Key Differences Between Abstract Classes and Interfaces:**
- Abstract classes can have implementation for some methods, while interfaces cannot.
- A class can implement multiple interfaces but can extend only one class.

---

## **6. Static Members**
Static members belong to the class rather than an instance.

### Example: Static Members
```typescript
class Utility {
    static PI: number = 3.14159;

    static calculateCircumference(radius: number): number {
        return 2 * Utility.PI * radius;
    }
}

console.log(Utility.PI); // 3.14159
console.log(Utility.calculateCircumference(5)); // 31.4159
```

---

## **7. Getters and Setters**
Getters and setters allow controlled access to properties.

### Example: Getters and Setters
```typescript
class Person {
    private _age: number;

    constructor(age: number) {
        this._age = age;
    }

    get age(): number {
        return this._age;
    }

    set age(value: number) {
        if (value < 0) {
            throw new Error("Age cannot be negative.");
        }
        this._age = value;
    }
}

const person = new Person(24);
console.log(person.age); // 24
person.age = 30;
console.log(person.age); // 30
```

---

## **8. Composition (as an OOP Concept)**
Composition allows building classes using other classes or objects as building blocks.

### Example: Composition
```typescript
class Engine {
    start() {
        console.log("Engine started.");
    }
}

class Car {
    private engine: Engine;

    constructor(engine: Engine) {
        this.engine = engine;
    }

    drive() {
        this.engine.start();
        console.log("Car is driving.");
    }
}

const engine = new Engine();
const car = new Car(engine);
car.drive();
// Output:
// Engine started.
// Car is driving.
```

---

## **Conclusion**
TypeScript enhances JavaScript's OOP capabilities by providing strong typing, access modifiers, abstract classes, interfaces, and more. It makes code more predictable and maintainable, especially in large-scale applications.
