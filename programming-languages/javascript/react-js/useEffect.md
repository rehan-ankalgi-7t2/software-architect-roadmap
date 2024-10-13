The `useEffect` hook in React is used to perform side effects in function components. It serves a similar purpose to lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.

### Syntax

```jsx
useEffect(() => {
  // Effect code here
}, [dependencies]);

```

### Usage

1. **Running on Mount**:
When you want to run an effect only once after the initial render, you can pass an empty array `[]` as the second argument to `useEffect`.
    
    ```jsx
    useEffect(() => {
      // Code to run on mount
    }, []);
    
    ```
    
2. **Running on State or Prop Change**:
If you want the effect to run whenever specific state variables or props change, you can include them in the dependencies array.
    
    ```jsx
    useEffect(() => {
      // Code to run on state or prop change
    }, [someState, someProp]);
    
    ```
    
3. **Running on Every Render**:
If you omit the dependencies array, the effect will run after every render.
    
    ```jsx
    useEffect(() => {
      // Code to run after every render
    });
    
    ```
    
4. **Cleanup**:
If your effect creates resources that need to be cleaned up (like subscriptions or timers), you can return a cleanup function from your `useEffect`.
    
    ```jsx
    useEffect(() => {
      const timer = setTimeout(() => {
        console.log('Timer triggered');
      }, 1000);
    
      // Cleanup function
      return () => {
        clearTimeout(timer);
      };
    }, []);
    
    ```
    

### Examples

1. **Fetching Data on Mount**:
    
    ```jsx
    useEffect(() => {
      fetch('<https://api.example.com/data>')
        .then(response => response.json())
        .then(data => setData(data));
    }, []);
    
    ```
    
2. **Subscribing to an Event**:
    
    ```jsx
    useEffect(() => {
      const handleResize = () => {
        setWindowSize({
          width: window.innerWidth,
          height: window.innerHeight,
        });
      };
    
      window.addEventListener('resize', handleResize);
    
      // Cleanup
      return () => {
        window.removeEventListener('resize', handleResize);
      };
    }, []);
    
    ```
    
3. **Effect with Dependencies**:
    
    ```jsx
    useEffect(() => {
      document.title = `You clicked ${count} times`;
    }, [count]);
    
    ```
    

Understanding and correctly using `useEffect` is crucial for managing side effects in React function components. Be mindful of dependency arrays to avoid unnecessary re-renders or missing updates.