# Test-Driven Development (TDD) in Java

> **Test-Driven Development (TDD)** is a software development approach where tests are written before the actual code. It emphasizes writing a test for a specific functionality first, then writing the minimal code necessary to pass the test, and finally refactoring the code while ensuring that all tests still pass.

TDD follows a simple, structured cycle called **Red-Green-Refactor**:

1. **Red**: Write a failing test for the next piece of functionality you want to add.
2. **Green**: Write just enough code to make the test pass.
3. **Refactor**: Clean up the code to meet best practices without changing its functionality.

### Steps in TDD:
1. Write a **test** that defines a function or improvement.
2. **Run** the test and watch it fail (since the function does not exist yet).
3. Write the **simplest possible code** that makes the test pass.
4. **Run the test** again to ensure the new code passes the test.
5. **Refactor** the code while ensuring all tests still pass.
6. Repeat the cycle.

---

### Example: TDD in Java Using JUnit

Let’s walk through a TDD example by building a simple calculator that adds two numbers. We'll use **JUnit**, the most popular testing framework for Java.

#### Step 1: Write a Failing Test (Red Phase)

First, we create a test class before writing any functionality. In TDD, this test will fail because no actual code exists yet.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTest {

    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(10, 20);
        assertEquals(30, result); // Test checks if 10 + 20 equals 30
    }
}
```

- **Explanation**: We are writing a test for the `add()` method of a `Calculator` class, which doesn't exist yet. The test expects the result of `add(10, 20)` to be 30. At this point, this test will fail because the `Calculator` class and its `add()` method haven't been implemented.

#### Step 2: Write Minimal Code to Pass the Test (Green Phase)

Now we implement the minimal code to make this test pass.

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;  // Simple implementation to make the test pass
    }
}
```

- **Explanation**: We define the `Calculator` class and the `add()` method that takes two integers and returns their sum. This is just enough code to make the test pass.

#### Step 3: Run the Test

Now, we run the test, and it should pass:

```bash
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
```

The test passes successfully.

#### Step 4: Refactor (Refactor Phase)

At this point, you can clean up the code if needed. Since the implementation is already simple and clear, there might not be much to refactor. However, in more complex cases, you could refactor the code for better readability, performance, or maintainability.

#### Step 5: Extend Functionality with More Tests

We can extend our `Calculator` class with more functionalities by following the TDD cycle again. For instance, let's add a `subtract()` method.

**Write the test first** (Red Phase):

```java
@Test
public void testSubtract() {
    Calculator calculator = new Calculator();
    int result = calculator.subtract(20, 10);
    assertEquals(10, result);  // Expect 20 - 10 to equal 10
}
```

**Write minimal code** to pass the test (Green Phase):

```java
public int subtract(int a, int b) {
    return a - b;  // Simple implementation
}
```

**Run the tests** again. Now both `add()` and `subtract()` should pass:

```bash
Tests run: 2, Failures: 0, Errors: 0, Skipped: 0
```

**Refactor** if necessary, and continue adding new functionalities in the same way.

---

### Advantages of TDD

1. **Improved Code Quality**: Since tests are written before the code, the focus is on writing code that meets specific requirements.
2. **Fewer Bugs**: Writing tests early catches bugs before they occur in production code.
3. **Better Design**: TDD encourages developers to think about interfaces and design from the start, leading to cleaner, more modular code.
4. **Confidence in Refactoring**: With a suite of tests, developers can refactor code confidently, knowing that if the tests pass, functionality is preserved.
5. **Documentation**: The tests act as a form of documentation, as they describe how the code is supposed to behave.
6. **Rapid Feedback**: Tests provide quick feedback on the correctness of the code.

### Challenges of TDD

1. **Steeper Learning Curve**: Developers new to TDD may initially find it difficult to adopt this approach.
2. **Time-Consuming**: Writing tests before the code can be time-consuming in the short term, though it saves time in the long term.
3. **Test Maintenance**: As the code evolves, maintaining the test suite can become complex.

---

### Key TDD Tools in Java

- **JUnit**: The most widely used testing framework for unit tests in Java.
- **Mockito**: A powerful mocking framework for simulating the behavior of dependencies in tests.
- **AssertJ**: A library for fluent assertions in testing, providing more readable test assertions.

---

### Full TDD Example (Complete Class and Tests)

#### `Calculator.java`:

```java
public class Calculator {

    // Method to add two numbers
    public int add(int a, int b) {
        return a + b;
    }

    // Method to subtract two numbers
    public int subtract(int a, int b) {
        return a - b;
    }

    // Method to multiply two numbers
    public int multiply(int a, int b) {
        return a * b;
    }

    // Method to divide two numbers
    public int divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Division by zero is not allowed.");
        }
        return a / b;
    }
}
```

#### `CalculatorTest.java`:

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTest {

    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        assertEquals(30, calculator.add(10, 20));
    }

    @Test
    public void testSubtract() {
        Calculator calculator = new Calculator();
        assertEquals(10, calculator.subtract(20, 10));
    }

    @Test
    public void testMultiply() {
        Calculator calculator = new Calculator();
        assertEquals(200, calculator.multiply(10, 20));
    }

    @Test
    public void testDivide() {
        Calculator calculator = new Calculator();
        assertEquals(5, calculator.divide(20, 4));
    }

    @Test(expected = IllegalArgumentException.class)
    public void testDivideByZero() {
        Calculator calculator = new Calculator();
        calculator.divide(10, 0); // Should throw IllegalArgumentException
    }
}
```

---

### Conclusion

Test-Driven Development (TDD) is a development methodology that ensures code is written to meet specific, tested requirements. It leads to cleaner, more reliable code and provides confidence in future changes through its robust test suite. In Java, tools like **JUnit** and **Mockito** play a key role in implementing TDD effectively.