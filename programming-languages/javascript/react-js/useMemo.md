The `useMemo` hook in React is used to memoize the result of a computation, preventing it from being recalculated on every render unless its dependencies change. This can help optimize performance, particularly for expensive computations.

### Syntax

```jsx
const memoizedValue = useMemo(() => computeValue(), [dependencies]);
```

### Usage

1. **Memoizing Expensive Computations**:
If you have an expensive computation, you can use `useMemo` to cache the result and recompute it only when necessary.
    
    ```jsx
    import { useMemo, useState } from 'react';
    
    function ExpensiveComponent() {
      const [count, setCount] = useState(0);
      const [input, setInput] = useState('');
    
      const expensiveComputation = (num) => {
        // Simulate an expensive computation
        let result = 0;
        for (let i = 0; i < 1000000000; i++) {
          result += num;
        }
        return result;
      };
    
      const computedValue = useMemo(() => expensiveComputation(count), [count]);
    
      return (
        <div>
          <input value={input} onChange={e => setInput(e.target.value)} />
          <button onClick={() => setCount(count + 1)}>Increment</button>
          <p>Computed Value: {computedValue}</p>
        </div>
      );
    }
    ```
    
2. **Optimizing Performance in Lists**:
When rendering a list of items, you can use `useMemo` to optimize the creation of list elements.
    
    ```jsx
    import { useMemo, useState } from 'react';
    
    function ListComponent({ items }) {
      const renderedItems = useMemo(() => {
        return items.map(item => <li key={item.id}>{item.name}</li>);
      }, [items]);
    
      return <ul>{renderedItems}</ul>;
    }
    ```
    

### Key Points

- **Memoization**: `useMemo` caches the result of a computation and only recomputes it when one of its dependencies changes.
- **Dependencies**: The second argument to `useMemo` is an array of dependencies. If any of the dependencies change, the memoized value is recomputed.
- **Performance Optimization**: Useful for optimizing performance by avoiding unnecessary recalculations.

### Example

1. **Memoizing Computed Values**:
    
    ```jsx
    import { useMemo, useState } from 'react';
    
    function FibonacciComponent() {
      const [num, setNum] = useState(0);
    
      const fibonacci = (n) => {
        if (n <= 1) return n;
        return fibonacci(n - 1) + fibonacci(n - 2);
      };
    
      const computedFibonacci = useMemo(() => fibonacci(num), [num]);
    
      return (
        <div>
          <input
            type="number"
            value={num}
            onChange={(e) => setNum(Number(e.target.value))}
          />
          <p>Fibonacci: {computedFibonacci}</p>
        </div>
      );
    }
    ```
    
2. **Optimizing Component Rendering**:
    
    ```jsx
    import { useMemo, useState } from 'react';
    
    function FilteredListComponent({ items, filter }) {
      const filteredItems = useMemo(() => {
        return items.filter(item => item.includes(filter));
      }, [items, filter]);
    
      return (
        <ul>
          {filteredItems.map((item, index) => (
            <li key={index}>{item}</li>
          ))}
        </ul>
      );
    }
    
    function App() {
      const [filter, setFilter] = useState('');
      const items = ['Apple', 'Banana', 'Orange', 'Mango', 'Grapes'];
    
      return (
        <div>
          <input
            value={filter}
            onChange={(e) => setFilter(e.target.value)}
            placeholder="Filter items"
          />
          <FilteredListComponent items={items} filter={filter} />
        </div>
      );
    }
    ```
    

Using `useMemo` effectively can help optimize your React applications by avoiding unnecessary computations and ensuring that your components render efficiently.