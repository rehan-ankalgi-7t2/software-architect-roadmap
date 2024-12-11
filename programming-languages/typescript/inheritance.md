Inheritance is a mechanism by which one class or object can acquire properties and methods of another. In JavaScript and TypeScript, inheritance can be achieved through various patterns. Here’s an overview of the available inheritance patterns:

---

### **1. Prototypal Inheritance (JavaScript Specific)**
JavaScript is a prototype-based language, and inheritance is achieved through objects linking to other objects via the prototype chain.

**Example:**
```javascript
const parent = {
    greet() {
        console.log("Hello from parent!");
    }
};

const child = Object.create(parent); // child inherits from parent
child.greet(); // Output: Hello from parent!
```

**Key Points:**
- Achieved using `Object.create()` or directly manipulating the prototype chain.
- Used when you want objects to inherit from other objects.
- Flexible and allows dynamic extension of objects.

---

### **2. Class-Based Inheritance (ES6 and TypeScript)**
Class-based inheritance mimics traditional object-oriented programming (OOP) paradigms.

**Example (JavaScript):**
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // Output: Rex barks.
```

**Example (TypeScript):**
```typescript
class Animal {
    constructor(public name: string) {}
    speak(): void {
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    speak(): void {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // Output: Rex barks.
```

**Key Points:**
- Syntax is similar to OOP languages like Java or C++.
- Enables method overriding and constructor inheritance.

---

### **3. Multiple Inheritance Using Mixins (JavaScript and TypeScript)**
JavaScript and TypeScript don’t support multiple inheritance directly, but it can be simulated using mixins.

**Example (TypeScript):**
```typescript
type Constructor<T = {}> = new (...args: any[]) => T;

function CanFly<TBase extends Constructor>(Base: TBase) {
    return class extends Base {
        fly() {
            console.log("I can fly!");
        }
    };
}

function CanSwim<TBase extends Constructor>(Base: TBase) {
    return class extends Base {
        swim() {
            console.log("I can swim!");
        }
    };
}

class Animal {}
class Bird extends CanFly(CanSwim(Animal)) {}

const bird = new Bird();
bird.fly(); // Output: I can fly!
bird.swim(); // Output: I can swim!
```

**Key Points:**
- Mixins combine properties and methods from multiple sources.
- Provides flexibility but can complicate the inheritance hierarchy.

---

### **4. Functional Inheritance (JavaScript Specific)**
Inheritance is achieved by creating factory functions and attaching additional methods.

**Example:**
```javascript
function Animal(name) {
    const obj = { name };
    obj.speak = function() {
        console.log(`${name} makes a noise.`);
    };
    return obj;
}

function Dog(name) {
    const dog = Animal(name);
    dog.speak = function() {
        console.log(`${name} barks.`);
    };
    return dog;
}

const rex = Dog("Rex");
rex.speak(); // Output: Rex barks.
```

**Key Points:**
- No classes or prototypes are used.
- Good for simpler scenarios but lacks the robustness of class-based or prototypal inheritance.

---

### **5. Hybrid Inheritance**
Combines class-based and prototypal inheritance to take advantage of both paradigms.

**Example (JavaScript):**
```javascript
function Animal(name) {
    this.name = name;
}
Animal.prototype.speak = function() {
    console.log(`${this.name} makes a noise.`);
};

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // Output: Rex barks.
```

**Key Points:**
- Combines flexibility of prototypes with clarity of classes.
- Often seen in libraries/frameworks like React.

---

### **6. Interface-Based Inheritance (TypeScript Only)**
TypeScript allows you to define the structure of a class using `interface`.

**Example:**
```typescript
interface Animal {
    name: string;
    speak(): void;
}

class Dog implements Animal {
    constructor(public name: string) {}
    speak(): void {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Rex");
dog.speak(); // Output: Rex barks.
```

**Key Points:**
- Interfaces enforce structure but don’t implement logic.
- Useful for ensuring consistency in codebases.

---

### **7. Delegation-Based Inheritance (JavaScript Specific)**
Objects delegate behavior to other objects without a direct hierarchical relationship.

**Example:**
```javascript
const animal = {
    speak() {
        console.log("Animal makes a noise.");
    }
};

const dog = {
    __proto__: animal,
    speak() {
        console.log("Dog barks.");
    }
};

dog.speak(); // Output: Dog barks.
```

**Key Points:**
- Achieved through `__proto__` or `Object.setPrototypeOf()`.
- Provides dynamic inheritance and avoids deep hierarchies.

---

### **Comparison of Patterns**

| Pattern                     | Flexibility    | Complexity | Use Case                                     |
|-----------------------------|----------------|------------|----------------------------------------------|
| **Prototypal Inheritance**  | High           | Medium     | Dynamic behavior, prototype chaining         |
| **Class-Based Inheritance** | Moderate       | Low        | OOP-style programming, easier to read        |
| **Mixins**                  | High           | Medium     | Combining features from multiple sources     |
| **Functional Inheritance**  | Moderate       | Low        | Simpler scenarios, avoiding prototype chaining |
| **Interface-Based**         | Moderate       | Low        | Type safety and enforcing structure (TypeScript) |
| **Hybrid**                  | Moderate       | Medium     | Combining clarity of classes and flexibility of prototypes |

---

### **Best Practices**
1. Use **class-based inheritance** for simplicity and maintainability.
2. Use **prototypal inheritance** or **mixins** for dynamic behavior or combining traits.
3. Prefer **interfaces** in TypeScript to define structure and ensure type safety.
4. Avoid deep inheritance hierarchies—favor composition over inheritance when possible.
