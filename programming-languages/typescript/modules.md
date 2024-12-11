# Modules in typescript

modules in ts = modules in js (es6 modules, files modules)

2 types of modules:
1. external modules (commonly used in code)
2. ambient modules (contains only type definitions, no other declarations can be done)

## Admbient modules (*.d.ts)

```typescript
export type sumArgs = {
  firstNum: number,
  secondNum: number
}

const foo = bar; // error
```

### **TypeScript Modules in Detail**

Modules in TypeScript are used to encapsulate and organize code into reusable pieces. They allow you to structure your application logically, manage dependencies, and control the visibility of variables, classes, and functions.

---

### **Types of Modules in TypeScript**

1. **Internal Modules (Deprecated)**
   - Known as **"namespaces"** in TypeScript.
   - Used for organizing code within a single file.
   - Mostly replaced by ES modules and avoided in modern TypeScript.

   ```typescript
   namespace MyNamespace {
       export const greet = () => "Hello!";
   }

   console.log(MyNamespace.greet()); // Output: "Hello!"
   ```

2. **External Modules (Preferred)**
   - Use the `import`/`export` syntax from ES6.
   - Encapsulate code in separate files.
   - Enable better maintainability and reuse.

   **File: mathUtils.ts**
   ```typescript
   export function add(a: number, b: number): number {
       return a + b;
   }

   export const PI = 3.14;
   ```

   **File: app.ts**
   ```typescript
   import { add, PI } from './mathUtils';

   console.log(add(2, 3)); // Output: 5
   console.log(PI);        // Output: 3.14
   ```

---

### **Export Types**

1. **Named Exports**
   - Allows multiple exports from a file.
   - Import specific items by their names.

   ```typescript
   export const a = 1;
   export const b = 2;
   ```

   ```typescript
   import { a, b } from './module';
   ```

2. **Default Exports**
   - Allows a single default export per file.
   - Common for exporting a primary class, function, or object.

   ```typescript
   export default function greet() {
       return "Hello, World!";
   }
   ```

   ```typescript
   import greet from './module';
   console.log(greet()); // Output: Hello, World!
   ```

---

### **Import Syntax**

1. **Named Import**
   ```typescript
   import { add, subtract } from './mathUtils';
   ```

2. **Wildcard Import**
   ```typescript
   import * as MathUtils from './mathUtils';

   console.log(MathUtils.add(1, 2));
   ```

3. **Default Import**
   ```typescript
   import myDefault from './defaultExport';
   ```

4. **Side-effect Import**
   ```typescript
   import './polyfills'; // Import a module for its side effects
   ```

---

### **Ambient Modules**

Ambient modules are a way to define the structure of third-party libraries or modules that don’t have TypeScript definitions. They help TypeScript understand the types and exports of such modules.

#### **Declaring Ambient Modules**
Ambient modules are declared using the `declare module` syntax. They are typically found in `.d.ts` files.

```typescript
// File: ambient-modules.d.ts
declare module "some-library" {
    export function someFunction(a: number): string;
}
```

#### **Using Ambient Modules**
You can import and use the module as if it had TypeScript support:

```typescript
import { someFunction } from "some-library";

console.log(someFunction(42)); // Assumes correct typing
```

---

### **Module Resolution**

TypeScript follows specific rules to resolve module paths:

1. **Relative Paths**
   - Start with `./` or `../`.
   - Example: `import { add } from './mathUtils';`

2. **Non-relative Paths**
   - Typically refer to modules installed via `npm` or defined in `node_modules`.
   - Example: `import express from 'express';`

3. **Custom Paths**
   - Can be configured in `tsconfig.json` using `paths` and `baseUrl`.

   ```json
   {
       "compilerOptions": {
           "baseUrl": "./src",
           "paths": {
               "@utils/*": ["utils/*"]
           }
       }
   }
   ```

   ```typescript
   import { helper } from '@utils/helper';
   ```

---

### **Key Concepts of TypeScript Modules**

1. **ES Modules Compatibility**
   - TypeScript's module system aligns with the ES6 module specification.

2. **Module Scopes**
   - Variables, functions, and classes in a module are local to that module by default.

3. **Tree-shaking**
   - Modern bundlers like Webpack or Rollup remove unused code from modules during the build process.

4. **Dynamic Imports**
   - Enables loading modules on demand.

   ```typescript
   async function loadUtils() {
       const { add } = await import('./mathUtils');
       console.log(add(2, 3));
   }
   ```

---

### **Best Practices**

1. **Use ES Modules**
   - Stick to `import`/`export` syntax for better compatibility and cleaner code.

2. **Keep Modules Small**
   - Avoid creating large modules; split them into logical units.

3. **Consistent Exports**
   - Use either default or named exports but maintain consistency across the codebase.

4. **Leverage TypeScript Declarations**
   - For third-party libraries without types, use `@types` packages or write custom declarations.

5. **Use Linting and Formatters**
   - Tools like ESLint and Prettier help maintain consistent module structure and formatting.

---

If you'd like specific examples or help with a module system, let me know!
