# What is Function Currying 🥘 ?

**Currying**, a technique used in functional programming, allows you to turn a function with numerous arguments into a series of nesting functions in JavaScript. It gives back a new function that anticipates the following parameter inline.

In other words, rather than accepting every argument at once, a function accepts the first one and returns a new function, which accepts the second and returns a new function, which accepts the third, and so on, until every argument has been satisfied.

> ***What is JavaScript Currying Function?***
> 

> *In JavaScript, currying converts a function with several arguments into a sequence of nested functions, each of which only accepts one argument. Currying aids in the development of higher order functions and helps you avoid passing the same variable more than once.*
> 

Specifically, when we change a function call from `multiply(1,2,3)` to `multiply(1)(2)(3)`.

<aside>
📎 function’s arity → another word for the number of arguments it accepts

</aside>

```jsx
/**
* two arity function
*/
function multiply(a) {
	return (b) => {
		return a * b;
	}
}

console.log(multiply(1)(2));
// outputs 2
```

```jsx
/**
* three arity function
*/
function multiply(a) {
	return (b) => {
		return (c) => {
			return a * b * c;
		}
	}
}

console.log(multiply(1)(2)(3));
// outputs 6
```

Curried functions are built by chaining closures and simultaneously defining and returning their inner functions.
