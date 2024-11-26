TypeScript is a **strongly typed superset of JavaScript** that compiles to plain JavaScript. It provides static typing, interfaces, classes, and advanced tooling to catch errors early and write robust, scalable applications. Here’s a detailed guide to all major TypeScript concepts.

---

## **1. Type Annotations**
TypeScript allows you to explicitly specify types for variables, function parameters, and return values.

### Basic Types
```typescript
let isDone: boolean = true;
let age: number = 24;
let name: string = "Rehan";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["Hello", 42]; // Tuple

let anything: any = "Can be anything"; // Avoid if possible
let unknownType: unknown = "Can be anything but safer than `any`"; 
let nothing: void = undefined; // Typically used for functions with no return value
let notAssigned: undefined = undefined;
let nullValue: null = null;
```

---

## **2. Functions**
### With Types
```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

### Optional and Default Parameters
```typescript
function greet(name: string, salutation: string = "Hello"): string {
  return `${salutation}, ${name}`;
}
```

### Rest Parameters
```typescript
function sum(...nums: number[]): number {
  return nums.reduce((acc, num) => acc + num, 0);
}
```

---

## **3. Interfaces**
Interfaces define the shape of objects.

```typescript
interface Person {
  name: string;
  age: number;
  greet(): void;
}

const person: Person = {
  name: "Rehan",
  age: 24,
  greet() {
    console.log("Hello!");
  },
};
```

---

## **4. Classes**
Classes in TypeScript follow OOP principles and include additional features like access modifiers.

### Syntax
```typescript
class Person {
  constructor(public name: string, private age: number) {}

  greet(): string {
    return `Hello, my name is ${this.name}`;
  }
}
```

---

## **5. Inheritance**
TypeScript supports inheritance with the `extends` keyword.

```typescript
class Employee extends Person {
  constructor(name: string, age: number, public role: string) {
    super(name, age);
  }

  getRole(): string {
    return this.role;
  }
}
```

---

## **6. Type System**

### **Union Types**
```typescript
let value: number | string;
value = 42; 
value = "hello"; 
```

### **Intersection Types**
```typescript
interface A {
  a: number;
}

interface B {
  b: string;
}

type AB = A & B;

const ab: AB = { a: 1, b: "hello" };
```

### **Type Aliases**
```typescript
type ID = string | number;
let userId: ID = "abc123";
```

---

## **7. Enums**
Enums allow you to define a set of named constants.

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let color: Color = Color.Green;
```

---

## **8. Generics**
Generics make components reusable while maintaining strong typing.

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("Hello");
```

### Generic Constraints
```typescript
function logLength<T extends { length: number }>(arg: T): void {
  console.log(arg.length);
}

logLength([1, 2, 3]);
```

---

## **9. Advanced Types**
### **Type Guards**
```typescript
function isString(value: any): value is string {
  return typeof value === "string";
}
```

### **Nullable Types**
```typescript
let nullable: string | null = null;
```

### **Type Casting**
```typescript
let value: any = "TypeScript";
let length = (value as string).length;
```

---

## **10. Modules**
Modules allow you to organize code into reusable pieces.

### Export and Import
```typescript
// utils.ts
export const greet = (name: string) => `Hello, ${name}`;

// main.ts
import { greet } from "./utils";
console.log(greet("Rehan"));
```

---

## **11. Namespaces**
Used for grouping code logically.

```typescript
namespace Utils {
  export function greet(name: string) {
    return `Hello, ${name}`;
  }
}

Utils.greet("Rehan");
```

---

## **12. Decorators**
A special feature in TypeScript for meta-programming, commonly used in frameworks like Angular.

```typescript
function Log(target: any, propertyName: string | Symbol): void {
  console.log(`${String(propertyName)} was accessed.`);
}

class MyClass {
  @Log
  myMethod() {
    console.log("Doing something...");
  }
}
```

---

## **13. Utility Types**
TypeScript provides built-in types to manipulate other types.

### **Partial**
Makes all properties optional.
```typescript
interface User {
  name: string;
  age: number;
}

let user: Partial<User> = {};
```

### **Readonly**
Makes all properties read-only.
```typescript
let user: Readonly<User> = { name: "Rehan", age: 24 };
// user.age = 25; // Error
```

### **Pick & Omit**
```typescript
type PickedUser = Pick<User, "name">;
type OmittedUser = Omit<User, "age">;
```

---

## **14. Type Narrowing**
TypeScript narrows types dynamically based on conditions.

```typescript
function narrow(value: number | string) {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}
```

---

## **15. Async/Await with TypeScript**
Asynchronous code with strong type checking.
```typescript
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/user/${id}`);
  return await response.json();
}
```

---

## **16. Type Assertion**
TypeScript allows you to override inferred types.
```typescript
let value: any = "hello";
let strLength: number = (value as string).length;
```

---

## **17. Configuration**
TypeScript is configured using a `tsconfig.json` file.

### Example
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "strict": true,
    "outDir": "./dist"
  }
}
```

---

TypeScript is a powerful tool for writing scalable and maintainable JavaScript applications. Mastering its features will enable you to build robust, production-grade applications efficiently!
