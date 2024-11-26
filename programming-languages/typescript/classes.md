In TypeScript, **classes** provide a way to define object templates with properties and methods. They enable object-oriented programming (OOP) features like inheritance, encapsulation, and polymorphism. Classes in TypeScript are similar to ES6 classes but include type annotations and additional features.

---

### **Basic Class**
```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person("Rehan", 24);
person.greet(); // Output: Hello, my name is Rehan and I am 24 years old.
```

---

### **Access Modifiers**
- **`public`**: Accessible from anywhere (default).
- **`private`**: Accessible only within the class.
- **`protected`**: Accessible within the class and subclasses.

```typescript
class BankAccount {
  public accountNumber: string;
  private balance: number;

  constructor(accountNumber: string, balance: number) {
    this.accountNumber = accountNumber;
    this.balance = balance;
  }

  public getBalance(): number {
    return this.balance; // Can access private property within the class.
  }

  private deductFees(): void {
    this.balance -= 10; // Deduct fees (only accessible internally).
  }
}

const account = new BankAccount("12345", 1000);
console.log(account.getBalance()); // Output: 1000
// account.deductFees(); // Error: 'deductFees' is private.
```

---

### **Inheritance**
TypeScript supports single inheritance using the `extends` keyword.

```typescript
class Animal {
  constructor(public name: string) {}

  speak(): void {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  speak(): void {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Buddy");
dog.speak(); // Output: Buddy barks.
```

---

### **Abstract Classes**
Abstract classes cannot be instantiated and are meant to be subclassed. They can have both implemented and abstract methods.

```typescript
abstract class Shape {
  abstract calculateArea(): number; // Must be implemented by subclasses.

  display(): void {
    console.log("Displaying the shape.");
  }
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  calculateArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

const circle = new Circle(10);
console.log(circle.calculateArea()); // Output: 314.159...
circle.display(); // Output: Displaying the shape.
```

---

### **Getters and Setters**
Use **get** and **set** to create computed properties.

```typescript
class Rectangle {
  constructor(private _width: number, private _height: number) {}

  get area(): number {
    return this._width * this._height;
  }

  set width(value: number) {
    if (value > 0) this._width = value;
    else throw new Error("Width must be positive.");
  }

  set height(value: number) {
    if (value > 0) this._height = value;
    else throw new Error("Height must be positive.");
  }
}

const rect = new Rectangle(10, 20);
console.log(rect.area); // Output: 200
rect.width = 15;
console.log(rect.area); // Output: 300
```

---

### **Static Members**
Static members belong to the class, not an instance.

```typescript
class MathUtils {
  static PI = 3.14159;

  static calculateCircumference(radius: number): number {
    return 2 * this.PI * radius;
  }
}

console.log(MathUtils.PI); // Output: 3.14159
console.log(MathUtils.calculateCircumference(10)); // Output: 62.8318
```

---

### **Readonly Properties**
A `readonly` property can only be initialized during declaration or in the constructor.

```typescript
class Book {
  readonly title: string;

  constructor(title: string) {
    this.title = title;
  }
}

const book = new Book("TypeScript Basics");
console.log(book.title); // Output: TypeScript Basics
// book.title = "Advanced TypeScript"; // Error: Cannot assign to 'title' because it is a read-only property.
```

---

### **Optional Properties**
Properties can be marked optional using `?`.

```typescript
class User {
  constructor(public name: string, public email?: string) {}
}

const user1 = new User("Rehan");
console.log(user1.email); // Output: undefined
```

---

### **Interfaces with Classes**
Classes can implement interfaces to ensure specific structure and behavior.

```typescript
interface Logger {
  log(message: string): void;
}

class ConsoleLogger implements Logger {
  log(message: string): void {
    console.log(`Log: ${message}`);
  }
}

const logger = new ConsoleLogger();
logger.log("Hello, TypeScript!"); // Output: Log: Hello, TypeScript!
```

TypeScript classes provide a robust way to implement and manage OOP principles in your code while leveraging strong typing.
