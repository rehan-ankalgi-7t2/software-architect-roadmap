# Simple Todo List ☑️

Here's how you can build a basic **Todo List** in React with "All", "Active", and "Completed" tabs without using any state management library like Redux. We'll manage the state with React's `useState` hook.

### Steps:

1. Create a basic layout with input for new todos.
2. Store todos in state and track their completion status.
3. Implement filtering logic to show todos based on the selected tab (All, Active, Completed).
4. Add buttons to switch between tabs.

### Code Implementation:

```jsx
import React, { useState } from 'react';

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [newTodo, setNewTodo] = useState('');
  const [filter, setFilter] = useState('all'); // 'all', 'active', 'completed'

  const handleAddTodo = () => {
    if (newTodo.trim()) {
      setTodos([
        ...todos,
        { text: newTodo, completed: false, id: Date.now() }
      ]);
      setNewTodo('');
    }
  };

  const handleToggleComplete = (id) => {
    setTodos(
      todos.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  const handleClearCompleted = () => {
    setTodos(todos.filter((todo) => !todo.completed));
  };

  const filteredTodos = todos.filter((todo) => {
    if (filter === 'active') return !todo.completed;
    if (filter === 'completed') return todo.completed;
    return true; // 'all' case
  });

  return (
    <div className="todo-app">
      <h1>Todo List</h1>

      {/* Input Section */}
      <div>
        <input
          type="text"
          value={newTodo}
          onChange={(e) => setNewTodo(e.target.value)}
          placeholder="Add a new todo"
        />
        <button onClick={handleAddTodo}>Add</button>
      </div>

      {/* Todo List Section */}
      <ul>
        {filteredTodos.map((todo) => (
          <li key={todo.id}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => handleToggleComplete(todo.id)}
            />
            <span
              style={{
                textDecoration: todo.completed ? 'line-through' : 'none'
              }}
            >
              {todo.text}
            </span>
          </li>
        ))}
      </ul>

      {/* Filter Section */}
      <div className="filters">
        <button onClick={() => setFilter('all')}>All</button>
        <button onClick={() => setFilter('active')}>Active</button>
        <button onClick={() => setFilter('completed')}>Completed</button>
      </div>

      {/* Clear Completed Button */}
      <div>
        <button onClick={handleClearCompleted}>Clear Completed</button>
      </div>
    </div>
  );
}

export default TodoApp;
```

### Explanation:
1. **State Management**:
   - `todos`: Holds the list of todo items, each item being an object with `text`, `completed`, and `id`.
   - `newTodo`: Holds the value of the input text for adding new todos.
   - `filter`: Stores the current filter (`'all'`, `'active'`, or `'completed'`).

2. **Filtering Logic**:
   - `filteredTodos`: Filters the `todos` array based on the selected tab (All, Active, Completed).

3. **UI**:
   - The todos are rendered as a list, where each todo item has a checkbox to toggle its completion status.
   - Buttons are provided to switch between the "All", "Active", and "Completed" tabs.
   - A "Clear Completed" button removes all completed todos from the list.

### Running this code:
1. Create a new React app using `npx create-react-app todo-list`.
2. Replace the contents of `App.js` with the code above.
3. Run the app using `npm start`.

This is a simple, clean React todo app without any external state management libraries like Redux.