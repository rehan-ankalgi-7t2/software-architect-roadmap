In React, both state and props are used to manage and pass data, but they serve different purposes and are used in different ways.

### Props

Props (short for properties) are used to pass data from a parent component to a child component. They are read-only and should not be modified by the child component. Props allow you to pass information and event handlers to child components, making your components more reusable and modular.

### Example:

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Greeting name="Alice" />

```

In the example above, the `Greeting` component receives a `name` prop and uses it to display a greeting message.

### Key Points about Props:

1. **Read-Only**: Props cannot be modified by the child component.
2. **Passed from Parent to Child**: Props are used to pass data and event handlers down the component tree.
3. **Reusable**: Components can be reused with different props to render different content.

### State

State is a built-in object that allows a component to keep track of data that can change over time. Unlike props, state is managed within the component and can be modified using the `setState` function in class components or the `useState` hook in functional components.

### Example with Class Component:

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

```

### Example with Functional Component and Hooks:

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

```

In these examples, the `Counter` component manages its own state (`count`). The state is initialized to 0 and can be incremented by clicking the button.

### Key Points about State:

1. **Mutable**: State can be changed using `this.setState` (class components) or `setState` (functional components).
2. **Managed within the Component**: State is private to the component and not accessible from outside.
3. **Triggers Re-render**: Updating the state causes the component to re-render and display the latest state.

### Comparing Props and State

| **Feature** | **Props** | **State** |
| --- | --- | --- |
| **Mutability** | Immutable (read-only) | Mutable (can be changed) |
| **Managed by** | Parent component | Component itself |
| **Purpose** | Pass data and event handlers to children | Manage dynamic data within a component |
| **Triggers Re-render** | No | Yes |

### Using Props and State Together

Often, props and state are used together to create dynamic and interactive components. For example, you might pass an initial value as a prop and use it to set the initial state.

### Example:

```jsx
function Counter(props) {
  const [count, setCount] = useState(props.initialCount);

  const increment = () => {
    setCount(count + 1);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

// Usage
<Counter initialCount={0} />

```

In this example, the `initialCount` prop is used to set the initial state of the `count`. The state can then be updated independently of the props.

Understanding the distinction and proper usage of props and state is crucial for managing data flow and component interactions in React applications.