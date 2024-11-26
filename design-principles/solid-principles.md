The SOLID principles are a set of design guidelines that aim to make software designs more maintainable, scalable, and robust. These principles help developers write clean, modular, and reusable code. Here's a breakdown of each principle:

---

### **1. Single Responsibility Principle (SRP)**

**Definition:**
A class should have only one reason to change. In other words, a class should only have one responsibility.

**Purpose:**
This principle ensures that a class is focused on a single task or functionality, making it easier to understand and modify.

**Example (JavaScript/TypeScript):**
```typescript
// Violates SRP
class Invoice {
  calculateTotal() {
    // Calculate total
  }
  printInvoice() {
    // Print the invoice
  }
}

// Follows SRP
class Invoice {
  calculateTotal() {
    // Calculate total
  }
}

class InvoicePrinter {
  printInvoice(invoice: Invoice) {
    // Print the invoice
  }
}
```

---

### **2. Open/Closed Principle (OCP)**

**Definition:**
Software entities (classes, modules, functions) should be open for extension but closed for modification.

**Purpose:**
Encourages adding new functionality by extending the existing code rather than modifying it, minimizing the risk of introducing bugs.

**Example (JavaScript/TypeScript):**
```typescript
// Violates OCP
class Discount {
  calculate(price: number, type: string) {
    if (type === 'percentage') {
      return price * 0.9;
    } else if (type === 'fixed') {
      return price - 10;
    }
  }
}

// Follows OCP
interface Discount {
  calculate(price: number): number;
}

class PercentageDiscount implements Discount {
  calculate(price: number): number {
    return price * 0.9;
  }
}

class FixedDiscount implements Discount {
  calculate(price: number): number {
    return price - 10;
  }
}
```

---

### **3. Liskov Substitution Principle (LSP)**

**Definition:**
Subtypes must be substitutable for their base types without altering the correctness of the program.

**Purpose:**
Ensures that derived classes can be used interchangeably with their base classes without unexpected behavior.

**Example (JavaScript/TypeScript):**
```typescript
// Violates LSP
class Bird {
  fly() {
    console.log('Flying');
  }
}

class Penguin extends Bird {
  fly() {
    throw new Error("Penguins can't fly");
  }
}

// Follows LSP
class Bird {
  makeSound() {
    console.log('Chirp');
  }
}

class FlyingBird extends Bird {
  fly() {
    console.log('Flying');
  }
}

class Penguin extends Bird {
  swim() {
    console.log('Swimming');
  }
}
```

---

### **4. Interface Segregation Principle (ISP)**

**Definition:**
A class should not be forced to implement interfaces it does not use. Instead, create smaller, more specific interfaces.

**Purpose:**
Prevents bloated interfaces and ensures that classes only implement methods relevant to them.

**Example (JavaScript/TypeScript):**
```typescript
// Violates ISP
interface Animal {
  fly(): void;
  swim(): void;
}

class Dog implements Animal {
  fly() {
    throw new Error("Dogs can't fly");
  }
  swim() {
    console.log('Swimming');
  }
}

// Follows ISP
interface Swimmer {
  swim(): void;
}

interface Flyer {
  fly(): void;
}

class Dog implements Swimmer {
  swim() {
    console.log('Swimming');
  }
}
```

---

### **5. Dependency Inversion Principle (DIP)**

**Definition:**
High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

**Purpose:**
Reduces coupling between high-level and low-level modules, promoting flexibility.

**Example (JavaScript/TypeScript):**
```typescript
// Violates DIP
class MySQLDatabase {
  connect() {
    console.log('Connected to MySQL');
  }
}

class Application {
  db: MySQLDatabase;

  constructor() {
    this.db = new MySQLDatabase();
  }

  start() {
    this.db.connect();
  }
}

// Follows DIP
interface Database {
  connect(): void;
}

class MySQLDatabase implements Database {
  connect() {
    console.log('Connected to MySQL');
  }
}

class Application {
  db: Database;

  constructor(db: Database) {
    this.db = db;
  }

  start() {
    this.db.connect();
  }
}

// Usage
const mySQL = new MySQLDatabase();
const app = new Application(mySQL);
app.start();
```

---

### **Summary of Benefits**
1. **SRP**: Makes classes smaller and easier to understand.
2. **OCP**: Encourages adding features without breaking existing functionality.
3. **LSP**: Ensures derived classes maintain compatibility.
4. **ISP**: Prevents unnecessary dependencies in interfaces.
5. **DIP**: Promotes loose coupling and flexibility.

These principles collectively lead to more modular, testable, and maintainable software systems.
