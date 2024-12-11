Generics in TypeScript allow you to write reusable and flexible components that can work with a variety of data types while maintaining type safety. They enable you to create types or functions that accept type parameters, ensuring type constraints at compile time.

---

### **Why Use Generics?**
Generics are useful when:
- You want to work with multiple data types in a type-safe way.
- You want to avoid `any` type for better type safety.
- You want to reuse code for different types.

---

### **Generic Syntax**
Generics use a type parameter (commonly denoted by `T`, `U`, `V`, etc.), which acts as a placeholder for a type that will be specified when the generic is used.

#### Example:
```typescript
function identity<T>(value: T): T {
  return value;
}

// Usage
const result1 = identity<number>(42);  // T is number
const result2 = identity<string>("hello"); // T is string
const result3 = identity<boolean>(true);  // T is boolean
```

---

### **Generic Functions**
You can use generics in functions to create type-safe and reusable logic.

#### Example:
```typescript
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge({ name: "Alice" }, { age: 25 });
// inferred type: { name: string; age: number }
console.log(merged); // Output: { name: 'Alice', age: 25 }
```

---

### **Generic Interfaces**
You can define generic interfaces to describe the shape of data that can work with multiple types.

#### Example:
```typescript
interface KeyValuePair<K, V> {
  key: K;
  value: V;
}

const pair: KeyValuePair<string, number> = { key: "age", value: 25 };
```

---

### **Generic Classes**
Generics can be used in classes to create type-safe implementations for various types.

#### Example:
```typescript
class DataStorage<T> {
  private data: T[] = [];

  addItem(item: T): void {
    this.data.push(item);
  }

  removeItem(item: T): void {
    this.data = this.data.filter((data) => data !== item);
  }

  getItems(): T[] {
    return [...this.data];
  }
}

const stringStorage = new DataStorage<string>();
stringStorage.addItem("hello");
stringStorage.addItem("world");
stringStorage.removeItem("hello");
console.log(stringStorage.getItems()); // Output: ['world']
```

---

### **Generic Constraints**
You can constrain a generic type to ensure it satisfies certain conditions.

#### Using `extends` Keyword:
```typescript
function printLength<T extends { length: number }>(item: T): void {
  console.log(item.length);
}

printLength("hello"); // Output: 5
printLength([1, 2, 3]); // Output: 3
// printLength(42); // Error: Type 'number' does not have a 'length' property
```

#### Keyof Constraint:
```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person = { name: "Alice", age: 25 };
console.log(getProperty(person, "name")); // Output: "Alice"
// console.log(getProperty(person, "address")); // Error: 'address' does not exist in type
```

---

### **Generic Default Types**
You can provide a default type for a generic parameter.

#### Example:
```typescript
interface ApiResponse<T = string> {
  status: number;
  data: T;
}

const response: ApiResponse<number> = { status: 200, data: 123 };
const defaultResponse: ApiResponse = { status: 200, data: "OK" };
```

---

### **Generic Utility Types**
TypeScript provides several built-in utility types based on generics, such as:

1. **`Partial<T>`**: Makes all properties of `T` optional.
2. **`Readonly<T>`**: Makes all properties of `T` readonly.
3. **`Record<K, T>`**: Constructs an object type with keys of type `K` and values of type `T`.
4. **`Pick<T, K>`**: Creates a type by picking a set of properties `K` from `T`.
5. **`Omit<T, K>`**: Creates a type by omitting a set of properties `K` from `T`.

---

### **Advantages of Generics**
1. **Reusability**: Code can work with a variety of types.
2. **Type Safety**: Ensures the type correctness at compile time.
3. **Flexibility**: You can design components to work with multiple data types.
4. **Code Clarity**: Makes the code more expressive and less prone to runtime errors.

---

### **Use Cases**
1. **Reusable Components**:
   - Generic lists, tables, or data structures.
2. **Type-safe APIs**:
   - Define return types for API calls dynamically.
3. **Dynamic Behavior**:
   - Classes or functions that adapt based on input types.

Generics are a cornerstone of TypeScript, enhancing its power by making it easier to write reusable, type-safe, and expressive code.
