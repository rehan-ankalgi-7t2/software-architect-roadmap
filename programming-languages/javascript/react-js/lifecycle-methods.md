Lifecycle methods in React are special methods that are invoked at different stages of a component's lifecycle. These methods provide hooks into the process of mounting, updating, and unmounting components. Lifecycle methods are primarily used in class components, but the concepts can also be applied to functional components using hooks.

### Lifecycle Phases

1. **Mounting**: When an instance of a component is being created and inserted into the DOM.
2. **Updating**: When a component is being re-rendered as a result of changes to its props or state.
3. **Unmounting**: When a component is being removed from the DOM.

### Mounting Phase Methods

1. **constructor()**
    - Called before the component is mounted.
    - Used to initialize state and bind event handlers.
    
    ```jsx
    constructor(props) {
      super(props);
      this.state = { count: 0 };
    }
    ```
    
2. **static getDerivedStateFromProps()**
    - Invoked right before calling the render method, both on the initial mount and on subsequent updates.
    - Used to update the state based on props.
    
    ```jsx
    static getDerivedStateFromProps(props, state) {
      if (props.someValue !== state.someValue) {
        return {
          someValue: props.someValue
        };
      }
      return null;
    }
    
    ```
    
3. **render()**
    - The only required method in a class component.
    - Returns the JSX that makes up the component.
    
    ```jsx
    render() {
      return <div>{this.state.count}</div>;
    }
    
    ```
    
4. **componentDidMount()**
    - Called immediately after the component is mounted.
    - Used for side-effects such as fetching data, setting up subscriptions, or interacting with the DOM.
    
    ```jsx
    componentDidMount() {
      // Fetch data or perform other side-effects
    }
    
    ```
    

### Updating Phase Methods

1. **static getDerivedStateFromProps()**
    - Called again in the updating phase to update state based on props.
2. **shouldComponentUpdate()**
    - Called before the render method to determine whether the component should re-render.
    - Can be used to optimize performance by preventing unnecessary renders.
    
    ```jsx
    shouldComponentUpdate(nextProps, nextState) {
      return nextProps.someValue !== this.props.someValue;
    }
    
    ```
    
3. **render()**
    - Called to re-render the component.
4. **getSnapshotBeforeUpdate()**
    - Called right before the DOM is updated.
    - Used to capture some information from the DOM (e.g., scroll position) before it changes.
    
    ```jsx
    getSnapshotBeforeUpdate(prevProps, prevState) {
      if (prevProps.list.length < this.props.list.length) {
        return this.listRef.scrollHeight;
      }
      return null;
    }
    
    ```
    
5. **componentDidUpdate()**
    - Called immediately after the component is updated.
    - Used for performing DOM operations or side-effects based on previous props or state.
    
    ```jsx
    componentDidUpdate(prevProps, prevState, snapshot) {
      if (snapshot !== null) {
        this.listRef.scrollTop = this.listRef.scrollHeight - snapshot;
      }
    }
    ```
    

### Unmounting Phase Methods

1. **componentWillUnmount()**
    - Called immediately before the component is unmounted and destroyed.
    - Used for cleanup, such as invalidating timers, canceling network requests, or cleaning up subscriptions.
    
    ```jsx
    componentWillUnmount() {
      // Perform cleanup
    }
    ```
    

### Error Handling Methods

1. **static getDerivedStateFromError()**
    - Called when an error is thrown in a descendant component.
    - Used to update state to display an error message.
    
    ```jsx
    static getDerivedStateFromError(error) {
      return { hasError: true };
    }
    ```
    
2. **componentDidCatch()**
    - Called when an error is thrown in a descendant component.
    - Used to log error information.
    
    ```jsx
    componentDidCatch(error, info) {
      // Log error information
    }
    
    ```
    

### Lifecycle Methods in Functional Components

With the introduction of Hooks, functional components can also manage lifecycle events using `useEffect` and other hooks.

### Example:

```jsx
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  // ComponentDidMount and ComponentDidUpdate
  useEffect(() => {
    document.title = `Count: ${count}`;

    // ComponentWillUnmount
    return () => {
      console.log('Cleanup');
    };
  }, [count]); // Dependency array

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

```

In this example, `useEffect` is used to perform side-effects and cleanup, mimicking the behavior of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

Understanding these lifecycle methods and their hooks counterparts is crucial for managing component behavior and side-effects in React applications.