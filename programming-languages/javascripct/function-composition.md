> Function composition is a programming concept where two or more functions are combined to produce a new function.
> 

In functional programming, functions are treated as first-class citizens, meaning they can be assigned to variables, passed as arguments to other functions, and returned as values from other functions. 

Function composition is a way to create new functions by combining existing functions.

The composition of two functions, **`f`** and **`g`**, is denoted as **`(f ∘ g)(x)`** and is equivalent to **`f(g(x))`**. In other words, the output of **`g`** becomes the input of **`f`**. This process can be extended to compose multiple functions together.

Here's a simple example in JavaScript:

```jsx
javascriptCopy code// Example functions
const addTwo = x => x + 2;
const multiplyByThree = x => x * 3;

// Function composition utility
const compose = (f, g) => x => f(g(x));

// Compose addTwo and multiplyByThree
const addTwoThenMultiplyByThree = compose(multiplyByThree, addTwo);

// Test the composed function
const result = addTwoThenMultiplyByThree(5); // Equivalent to multiplyByThree(addTwo(5))
console.log(result); 

// Output: 21
```

<aside>
💡 Function composition promotes `code reusability`, `modularity`, and a more `declarative programming style`. It allows you to build complex functionality by combining smaller, focused functions. In functional programming languages, composition is a powerful technique for creating expressive and concise code.

</aside>
