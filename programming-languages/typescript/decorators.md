In TypeScript, **decorators** are a special feature that allows you to add metadata or modify classes, methods, properties, or parameters. They are part of TypeScript's experimental features and align closely with ES decorators (a proposed JavaScript feature). Decorators are commonly used in frameworks like **Angular** or **NestJS**.

---

## **What are Decorators?**
Decorators are special functions prefixed with `@` that are applied to a **class**, **method**, **property**, or **parameter** to augment or modify their behavior.

### **Enabling Decorators**
To use decorators in TypeScript, you need to enable the experimental feature in the `tsconfig.json` file:
```json
{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
```

---

## **Types of Decorators**
TypeScript supports the following types of decorators:

### 1. **Class Decorators**
Class decorators are applied to a class and can modify or extend its behavior.

**Example:**
```typescript
function LogClass(constructor: Function) {
    console.log(`Class Decorator Called for: ${constructor.name}`);
}

@LogClass
class ExampleClass {
    constructor() {
        console.log("Instance Created");
    }
}

// Output:
// Class Decorator Called for: ExampleClass
// Instance Created
```

---

### 2. **Method Decorators**
Method decorators are applied to a method of a class.

**Example:**
```typescript
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;
    descriptor.value = function (...args: any[]) {
        console.log(`Method ${propertyKey} called with args: ${JSON.stringify(args)}`);
        return originalMethod.apply(this, args);
    };
}

class ExampleClass {
    @LogMethod
    sayHello(name: string) {
        console.log(`Hello, ${name}`);
    }
}

const obj = new ExampleClass();
obj.sayHello("Rehan");
// Output:
// Method sayHello called with args: ["Rehan"]
// Hello, Rehan
```

---

### 3. **Property Decorators**
Property decorators are used to modify or observe the behavior of class properties.

**Example:**
```typescript
function LogProperty(target: any, propertyKey: string) {
    console.log(`Property Decorator Called for: ${propertyKey}`);
}

class ExampleClass {
    @LogProperty
    myProperty: string = "Hello";
}

// Output:
// Property Decorator Called for: myProperty
```

---

### 4. **Accessor Decorators**
Accessor decorators are applied to a getter or setter of a property.

**Example:**
```typescript
function LogAccessor(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    console.log(`Accessor Decorator Called for: ${propertyKey}`);
}

class ExampleClass {
    private _name: string = "Rehan";

    @LogAccessor
    get name() {
        return this._name;
    }

    set name(value: string) {
        this._name = value;
    }
}

// Output:
// Accessor Decorator Called for: name
```

---

### 5. **Parameter Decorators**
Parameter decorators are used to add metadata to method parameters.

**Example:**
```typescript
function LogParameter(target: any, propertyKey: string, parameterIndex: number) {
    console.log(`Parameter Decorator Called for: ${propertyKey} at index ${parameterIndex}`);
}

class ExampleClass {
    sayHello(@LogParameter name: string) {
        console.log(`Hello, ${name}`);
    }
}

// Output:
// Parameter Decorator Called for: sayHello at index 0
```

---

## **Decorator Execution Order**
When multiple decorators are applied, their execution order is as follows:
1. **Parameter decorators** (left-to-right)
2. **Method/Accessor decorators**
3. **Property decorators**
4. **Class decorators**

**Example:**
```typescript
function ClassDecorator(constructor: Function) {
    console.log("Class Decorator");
}

function MethodDecorator(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    console.log("Method Decorator");
}

function PropertyDecorator(target: any, propertyKey: string) {
    console.log("Property Decorator");
}

@ClassDecorator
class ExampleClass {
    @PropertyDecorator
    myProperty: string;

    @MethodDecorator
    myMethod() {}
}

// Output:
// Property Decorator
// Method Decorator
// Class Decorator
```

---

## **Use Cases of Decorators**
1. **Metadata and Dependency Injection**:
   - Example: `@Injectable()` in **NestJS** or Angular.
2. **Validation**:
   - Example: Validate input using `class-validator` in TypeScript classes.
3. **Logging and Debugging**:
   - Intercept methods and log input/output.
4. **Routing and Middleware**:
   - Example: `@Get()` or `@Post()` in **NestJS**.

---

## **Advanced Example: NestJS-style Controller Decorators**
```typescript
function Controller(routePrefix: string) {
    return function (constructor: Function) {
        console.log(`Controller Initialized: ${routePrefix}`);
    };
}

function Get(route: string) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log(`GET Endpoint: ${route}`);
    };
}

@Controller("/users")
class UserController {
    @Get("/")
    getUsers() {
        console.log("Fetching users");
    }
}

// Output:
// Controller Initialized: /users
// GET Endpoint: /
```

---

## **Ambient Decorators**
Ambient decorators are used to augment existing libraries or frameworks without modifying them directly. They require `emitDecoratorMetadata` in `tsconfig.json`:
```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

**Example (with Metadata):**
```typescript
import "reflect-metadata";

function LogType(target: any, propertyKey: string) {
    const type = Reflect.getMetadata("design:type", target, propertyKey);
    console.log(`${propertyKey} type: ${type.name}`);
}

class ExampleClass {
    @LogType
    myProperty: string;
}

// Output:
// myProperty type: String
```

---

## **Best Practices for Decorators**
1. Use decorators primarily for cross-cutting concerns (e.g., logging, validation, security).
2. Avoid excessive use in simple projects—they may increase complexity.
3. Follow patterns established by frameworks like Angular or NestJS for clarity.
4. Use metadata (`reflect-metadata`) to enhance decorator functionality in TypeScript.

---

### **Note on Decorators in ESNext**
While TypeScript supports experimental decorators, the official JavaScript decorator proposal introduces different semantics. Keep track of updates if transitioning to ESNext decorators.
