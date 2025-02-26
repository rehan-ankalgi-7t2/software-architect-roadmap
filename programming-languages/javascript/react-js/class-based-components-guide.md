### **📌 Guide to Class-Based Components in React**  

React **Class Components** were the primary way to define components before **React Hooks** were introduced in **React 16.8**. They are still widely used in legacy projects and sometimes in complex applications requiring lifecycle methods.

---

## **🔹 1. Creating a Class Component**
A **class component** in React must extend `React.Component` or `React.PureComponent` and must implement a `render()` method.

### **Example: Basic Class Component**
```jsx
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Welcome;
```
✔ **Extends `Component`** from React.  
✔ **Has a `render()` method** that returns JSX.  
✔ **Receives `props`** like a function component.

---

## **🔹 2. State in Class Components**
Class components manage internal data using `this.state`.

### **Example: Using `state`**
```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```
✔ **State is an object stored in `this.state`**.  
✔ **Use `setState()`** to update state (React handles re-renders).  
✔ **Arrow functions (`increment`) automatically bind `this`**.

---

## **🔹 3. Lifecycle Methods in Class Components**
Lifecycle methods control what happens at different stages of a component’s life.

### **🔸 Mounting (Component Creation)**
| Method | Purpose |
|---------|----------|
| `constructor()` | Initialize state & bind methods. |
| `static getDerivedStateFromProps(props, state)` | Sync state with props before rendering. |
| `render()` | Render JSX. |
| `componentDidMount()` | Run code after component is added to the DOM (good for API calls). |

### **Example: `componentDidMount()`**
```jsx
import React, { Component } from 'react';

class DataFetcher extends Component {
  constructor(props) {
    super(props);
    this.state = { data: null };
  }

  componentDidMount() {
    fetch('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => response.json())
      .then(data => this.setState({ data }));
  }

  render() {
    return <div>{this.state.data ? this.state.data.title : 'Loading...'}</div>;
  }
}

export default DataFetcher;
```
✔ Fetches data **after** mounting.  
✔ Updates state → Triggers **re-render**.

---

### **🔸 Updating (Component Re-rendering)**
| Method | Purpose |
|---------|----------|
| `static getDerivedStateFromProps(props, state)` | Sync state when props change. |
| `shouldComponentUpdate(nextProps, nextState)` | Control re-renders (optimize performance). |
| `render()` | Re-render JSX. |
| `getSnapshotBeforeUpdate(prevProps, prevState)` | Capture values before re-render (e.g., scroll position). |
| `componentDidUpdate(prevProps, prevState)` | Run side effects after update. |

### **Example: `componentDidUpdate()`**
```jsx
import React, { Component } from 'react';

class UpdateLogger extends Component {
  componentDidUpdate(prevProps) {
    if (prevProps.count !== this.props.count) {
      console.log(`Count changed from ${prevProps.count} to ${this.props.count}`);
    }
  }

  render() {
    return <h2>Count: {this.props.count}</h2>;
  }
}

export default UpdateLogger;
```
✔ **Triggers only when `props.count` changes**.  
✔ Logs old & new values.

---

### **🔸 Unmounting (Component Removal)**
| Method | Purpose |
|---------|----------|
| `componentWillUnmount()` | Cleanup before the component is removed (good for clearing timers, event listeners, etc.). |

### **Example: `componentWillUnmount()`**
```jsx
import React, { Component } from 'react';

class Timer extends Component {
  componentDidMount() {
    this.interval = setInterval(() => console.log('Tick'), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.interval);
    console.log('Timer stopped');
  }

  render() {
    return <h2>Timer running...</h2>;
  }
}

export default Timer;
```
✔ **Runs cleanup code before unmounting**.  
✔ Prevents **memory leaks**.

---

## **🔹 4. Handling Events in Class Components**
Event handlers require **binding** because class methods don’t auto-bind `this`.

### **Example: Handling Click Events**
```jsx
import React, { Component } from 'react';

class ClickHandler extends Component {
  constructor(props) {
    super(props);
    this.state = { message: 'Hello!' };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState({ message: 'Button Clicked!' });
  }

  render() {
    return (
      <div>
        <h2>{this.state.message}</h2>
        <button onClick={this.handleClick}>Click Me</button>
      </div>
    );
  }
}

export default ClickHandler;
```
✔ `handleClick()` must be bound in the constructor **OR** use an arrow function.

---

## **🔹 5. Using `PureComponent` for Optimization**
- `React.PureComponent` prevents **unnecessary re-renders**.
- It **shallow compares props and state** before re-rendering.

### **Example: Using `PureComponent`**
```jsx
import React, { PureComponent } from 'react';

class OptimizedCounter extends PureComponent {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    console.log('Re-rendering...');
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default OptimizedCounter;
```
✔ **Avoids re-renders if state/props didn’t change**.  
✔ Use for **performance optimization**.

---

## **🔹 6. Converting Class Components to Functional Components**
With **React Hooks**, functional components can now manage state & lifecycle.

### **Converting `Counter` to Functional Component**
**Before (Class Component)**:
```jsx
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```
**After (Functional Component with Hooks)**:
```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```
✔ **Less code, better readability**  
✔ Uses `useState()` instead of `this.state`  
✔ No need for `this` or binding methods  

---

## **🎯 Summary**
- **Class Components** are still useful in legacy projects.
- Use **`state`** and **`setState()`** for managing internal data.
- **Lifecycle methods** (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`) handle side effects.
- **Event handling** requires explicit binding.
- **Use `PureComponent`** for optimization.
- **Hooks (`useState`, `useEffect`) have replaced most class component features**.

Would you like me to cover **advanced topics like Context API, Error Boundaries, or HOCs with class components**? 😊
