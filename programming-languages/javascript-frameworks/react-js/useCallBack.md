The `useCallback` hook in React is used to memoize callback functions, preventing them from being recreated on every render unless one of their dependencies changes. This can be particularly useful for optimizing performance in components that pass callback functions to child components.

### Syntax

```jsx
const memoizedCallback = useCallback(() => {
  // Callback code here
}, [dependencies]);
```

### Usage

1. **Memoizing Callbacks**:
When you pass a callback to a child component, wrapping the callback in `useCallback` ensures that the function reference remains stable as long as its dependencies don’t change. This can help avoid unnecessary re-renders of the child component.
    
    ```jsx
    import { useCallback, useState } from 'react';
    
    function ParentComponent() {
      const [count, setCount] = useState(0);
    
      const increment = useCallback(() => {
        setCount(prevCount => prevCount + 1);
      }, []);
    
      return <ChildComponent onClick={increment} />;
    }
    
    function ChildComponent({ onClick }) {
      return <button onClick={onClick}>Increment</button>;
    }
    ```
    
2. **Optimizing Expensive Computations**:
If you have a component that performs an expensive computation or operation, using `useCallback` can help ensure the function is only recreated when necessary.
    
    ```jsx
    import { useState, useCallback } from 'react';
    
    function ExpensiveComponent() {
      const [count, setCount] = useState(0);
      const [value, setValue] = useState('');
    
      const computeExpensiveValue = useCallback(() => {
        // Perform expensive computation
        return count * 2;
      }, [count]);
    
      return (
        <div>
          <input value={value} onChange={e => setValue(e.target.value)} />
          <button onClick={() => setCount(count + 1)}>Increment</button>
          <p>Computed Value: {computeExpensiveValue()}</p>
        </div>
      );
    }
    ```
    

### Key Points

- **Memoization**: `useCallback` returns a memoized version of the callback function that only changes if one of its dependencies changes.
- **Dependencies**: The second argument to `useCallback` is an array of dependencies. If any of the dependencies change, the callback function is recreated.
- **Performance Optimization**: Useful for optimizing performance, especially when passing callbacks to child components that rely on reference equality to prevent re-renders.

### Example

1. **Passing Memoized Callbacks to Child Components**:
    
    ```jsx
    import { useCallback, useState } from 'react';
    
    function ParentComponent() {
      const [count, setCount] = useState(0);
    
      const handleIncrement = useCallback(() => {
        setCount(count + 1);
      }, [count]);
    
      return <ChildComponent onIncrement={handleIncrement} />;
    }
    
    function ChildComponent({ onIncrement }) {
      return <button onClick={onIncrement}>Increment</button>;
    }
    ```
    
2. **Memoizing Functions with Dependencies**:
    
    ```jsx
    import { useCallback, useState } from 'react';
    
    function SearchComponent() {
      const [query, setQuery] = useState('');
    
      const handleSearch = useCallback(() => {
        // Perform search with query
        console.log(`Searching for ${query}`);
      }, [query]);
    
      return (
        <div>
          <input value={query} onChange={e => setQuery(e.target.value)} />
          <button onClick={handleSearch}>Search</button>
        </div>
      );
    }
    ```
    

Using `useCallback` effectively helps ensure that your React components only re-render when necessary, leading to better performance and a smoother user experience.