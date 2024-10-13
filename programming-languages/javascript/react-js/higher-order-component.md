Component composition in React refers to the practice of combining smaller, reusable components to build larger and more complex user interfaces. It's a fundamental principle of React development that promotes code reusability, maintainability, and separation of concerns. There are several techniques for achieving component composition in React:

### 1. **Parent-Child Composition**

This is the most basic form of component composition where a parent component renders one or more child components.

**Example:**

```jsx
function ParentComponent() {
  return (
    <div>
      <h2>Parent Component</h2>
      <ChildComponent />
      <ChildComponent />
    </div>
  );
}

function ChildComponent() {
  return <p>Child Component</p>;
}

function App() {
  return <ParentComponent />;
}

export default App;

```

### 2. **Props Composition**

Components can be composed by passing props (properties) to child components. Props are a way of passing data from parent to child components.

**Example:**

```jsx
function ParentComponent() {
  const message = "Hello from Parent";

  return (
    <div>
      <h2>Parent Component</h2>
      <ChildComponent message={message} />
    </div>
  );
}

function ChildComponent(props) {
  return <p>Message from Parent: {props.message}</p>;
}

function App() {
  return <ParentComponent />;
}

export default App;

```

### 3. **Higher Order Components (HOCs)**

Higher Order Components are functions that take a component and return a new enhanced component with additional functionality. They enable component composition by wrapping components with reusable logic.

**Example:**

```jsx
function withLogger(Component) {
  return function WrappedComponent(props) {
    console.log('Props:', props);
    return <Component {...props} />;
  };
}

function MyComponent(props) {
  return <p>Message: {props.message}</p>;
}

const MyComponentWithLogger = withLogger(MyComponent);

function App() {
  return <MyComponentWithLogger message="Hello, World!" />;
}

export default App;

```

### 4. **Render Props**

Render props is a technique where a component's logic is encapsulated in a prop that is a function. This allows components to share code and state.

**Example:**

```jsx
class MouseTracker extends React.Component {
  constructor(props) {
    super(props);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove = (event) => {
    this.setState({ x: event.clientX, y: event.clientY });
  };

  render() {
    return (
      <div style={{ height: '100vh' }} onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    );
  }
}

function App() {
  return (
    <MouseTracker
      render={(mouse) => (
        <p>
          Mouse position: {mouse.x}, {mouse.y}
        </p>
      )}
    />
  );
}

export default App;

```

### 5. **Hooks**

With the introduction of hooks in React, functional components can now use state and other React features without writing a class. This promotes component composition by allowing reuse of stateful logic across components.

**Example:**

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

function App() {
  return (
    <div>
      <h2>Counter Example</h2>
      <Counter />
      <Counter />
    </div>
  );
}

export default App;

```

### Benefits of Component Composition

- **Reusability**: Components can be reused in different parts of the application.
- **Separation of Concerns**: Each component can focus on a specific piece of functionality or presentation.
- **Maintainability**: Smaller components are easier to understand, debug, and maintain.
- **Scalability**: Complex UIs can be built by combining simpler components.

### Conclusion

Component composition is a core concept in React development, enabling developers to build flexible, modular, and maintainable user interfaces. By understanding and leveraging these techniques—such as parent-child composition, props composition, HOCs, render props, and hooks—you can create powerful and reusable components that enhance the structure and scalability of your React applications. Each technique has its use cases and strengths, allowing you to choose the most appropriate approach based on your specific requirements and preferences.