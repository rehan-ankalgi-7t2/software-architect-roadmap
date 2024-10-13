# Java Cheat Sheet

### 1. **Basic Syntax**
```java
// Hello World
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### 2. **Data Types**

| Type      | Size       | Example                |
|-----------|------------|------------------------|
| `int`     | 4 bytes    | `int age = 30;`        |
| `float`   | 4 bytes    | `float pi = 3.14f;`    |
| `double`  | 8 bytes    | `double e = 2.71828;`  |
| `char`    | 2 bytes    | `char grade = 'A';`    |
| `boolean` | 1 bit      | `boolean isValid = true;` |
| `String`  | depends    | `String name = "John";`|

### 3. **Variables**

```java
// Declaration and Initialization
int number = 10;
final int CONSTANT = 100;  // Constant

// Type Inference (from Java 10 onwards)
var num = 5;  // Compiler infers type as int
```

### 4. **Operators**

| Operator   | Description           | Example               |
|------------|-----------------------|-----------------------|
| `+`        | Addition              | `a + b`               |
| `-`        | Subtraction           | `a - b`               |
| `*`        | Multiplication        | `a * b`               |
| `/`        | Division              | `a / b`               |
| `%`        | Modulo (Remainder)    | `a % b`               |
| `&&`       | Logical AND           | `a && b`              |
| `||`       | Logical OR            | `a || b`              |
| `==`       | Equal to              | `a == b`              |
| `!=`       | Not equal to          | `a != b`              |

---

### 5. **Control Flow**

#### **If-Else**
```java
if (condition) {
    // code if condition is true
} else if (otherCondition) {
    // code if otherCondition is true
} else {
    // code if none of the conditions are true
}
```

#### **Switch Statement**
```java
int day = 3;
switch(day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    default: System.out.println("Other day");
}
```

#### **For Loop**
```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

#### **While Loop**
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

#### **Do-While Loop**
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

#### **Enhanced For Loop**
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

---

### 6. **Methods**
```java
// Method Declaration
public int add(int a, int b) {
    return a + b;
}

// Method Call
int result = add(5, 3);  // result = 8
```

#### **Method Overloading** (Same method name with different parameters)
```java
public int add(int a, int b) {
    return a + b;
}

public double add(double a, double b) {
    return a + b;
}
```

---

### 7. **Classes and Objects**

#### **Class Declaration**
```java
class Car {
    String model;
    int year;

    public Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    public void drive() {
        System.out.println(model + " is driving.");
    }
}
```

#### **Object Creation**
```java
Car car1 = new Car("Toyota", 2020);
car1.drive();  // Output: Toyota is driving.
```

---

### 8. **Inheritance**

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}
```

---

### 9. **Interfaces**

```java
interface Animal {
    void eat();
    void sleep();
}

class Dog implements Animal {
    public void eat() {
        System.out.println("Dog eats bones.");
    }

    public void sleep() {
        System.out.println("Dog sleeps.");
    }
}
```

---

### 10. **Abstract Classes**
```java
abstract class Animal {
    abstract void sound();  // Abstract method

    void eat() {
        System.out.println("This animal eats food.");  // Concrete method
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("The dog barks.");
    }
}
```

---

### 11. **Exception Handling**
```java
try {
    int result = 10 / 0;  // This will throw ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
} finally {
    System.out.println("This will always run.");
}
```

---

### 12. **Collections**

#### **ArrayList**
```java
import java.util.ArrayList;

ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Orange");

for (String fruit : list) {
    System.out.println(fruit);
}
```

#### **HashMap**
```java
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();
map.put("Apple", 10);
map.put("Banana", 20);

for (String key : map.keySet()) {
    System.out.println(key + ": " + map.get(key));
}
```

---

### 13. **Streams (Java 8+)**

#### **Lambda Expressions**
```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.forEach(name -> System.out.println(name));
```

#### **Stream API**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream().filter(n -> n % 2 == 0).mapToInt(n -> n).sum();
System.out.println(sum);  // Output: 6 (sum of even numbers)
```

---

### 14. **Multithreading**

#### **Extending `Thread`**
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running.");
    }
}

MyThread t1 = new MyThread();
t1.start();
```

#### **Implementing `Runnable`**
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable is running.");
    }
}

Thread t1 = new Thread(new MyRunnable());
t1.start();
```

---

### 15. **File I/O**
```java
import java.io.FileWriter;
import java.io.IOException;

try {
    FileWriter writer = new FileWriter("output.txt");
    writer.write("Hello, World!");
    writer.close();
} catch (IOException e) {
    e.printStackTrace();
}
```

---

### 16. **Generics**
```java
public class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

Box<Integer> intBox = new Box<>();
intBox.set(123);
System.out.println(intBox.get());  // Output: 123
```

---

### 17. **Annotations**
```java
@Override
public String toString() {
    return "This is an overridden method.";
}

@SuppressWarnings("unchecked")
public void method() {
    // Code with potential unchecked warnings
}
```

---

### 18. **Enums**
```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY
}

Day day = Day.MONDAY;
```

---

This cheat sheet covers the fundamental features of Java. It can be expanded to cover more advanced topics like `synchronization`, `reflection`, `streams`, `annotations`, and `concurrency` based on your needs.