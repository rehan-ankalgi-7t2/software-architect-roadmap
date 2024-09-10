The **`useState`** hook allows you to add state to a functional component.

```jsx
const [state, setState] = useState(initialState);
```

### **Real-World Implementation: Counter Component**

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;
```