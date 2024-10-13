The `useRef` hook in React provides a way to create a mutable object that persists for the lifetime of the component. It's often used to access or store a DOM element or to keep a mutable value that doesn’t cause a re-render when updated.

### Syntax

```jsx
const refContainer = useRef(initialValue);
```

### Usage

1. **Accessing DOM Elements**:
You can use `useRef` to directly access a DOM element and perform operations like focusing an input or measuring its dimensions.
    
    ```jsx
    import { useRef, useEffect } from 'react';
    
    function MyComponent() {
      const inputRef = useRef(null);
    
      useEffect(() => {
        // Focus the input element on mount
        inputRef.current.focus();
      }, []);
    
      return <input ref={inputRef} type="text" />;
    }
    ```
    
2. **Storing Mutable Values**:
You can also use `useRef` to store any mutable value that you want to persist across renders without causing re-renders.
    
    ```jsx
    import { useRef, useState } from 'react';
    
    function Timer() {
      const intervalRef = useRef(null);
      const [count, setCount] = useState(0);
    
      const startTimer = () => {
        intervalRef.current = setInterval(() => {
          setCount(prevCount => prevCount + 1);
        }, 1000);
      };
    
      const stopTimer = () => {
        clearInterval(intervalRef.current);
      };
    
      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={startTimer}>Start</button>
          <button onClick={stopTimer}>Stop</button>
        </div>
      );
    }
    ```
    

### Key Points

- **Mutable Object**: The object returned by `useRef` will persist for the full lifetime of the component.
- **Doesn’t Cause Re-renders**: Changing the `.current` property of the `useRef` object does not cause the component to re-render.
- **Access DOM Elements**: `useRef` is often used for accessing DOM elements directly.
- **Storing State Across Renders**: It can be used to store any value that needs to persist across renders without triggering a re-render.

### Example

1. **Focusing an Input Field**:
    
    ```jsx
    import { useRef, useEffect } from 'react';
    
    function FocusInput() {
      const inputEl = useRef(null);
    
      useEffect(() => {
        inputEl.current.focus();
      }, []);
    
      return <input ref={inputEl} type="text" />;
    }
    ```
    
2. **Tracking Previous State**:
    
    ```jsx
    import { useRef, useEffect, useState } from 'react';
    
    function PreviousStateExample() {
      const [count, setCount] = useState(0);
      const prevCountRef = useRef();
    
      useEffect(() => {
        prevCountRef.current = count;
      }, [count]);
    
      const prevCount = prevCountRef.current;
    
      return (
        <div>
          <p>Now: {count}, before: {prevCount}</p>
          <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
      );
    }
    ```
    

Using `useRef` effectively allows you to interact with the DOM and manage mutable values in a way that integrates smoothly with React's rendering process.

The refs are used for:
Managing focus, media playback, or text selection.Integrating with DOM libraries by third-party.Triggering the imperative animations.