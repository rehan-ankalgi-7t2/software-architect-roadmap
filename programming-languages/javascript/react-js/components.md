In React, components are the building blocks of the user interface. They allow you to split the UI into independent, reusable pieces that can be handled separately. React components come in two main types: **Class Components** and **Functional Components**.

### Functional Components

Functional components are simple JavaScript functions that accept props as an argument and return a React element. They are often used for presentational purposes and have become more powerful with the introduction of Hooks.

### Example:

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Greeting name="Alice" />

```

### Class Components

Class components are ES6 classes that extend `React.Component`. They have more features than functional components, such as local state and lifecycle methods.

### Example:

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

// Usage
<Greeting name="Bob" />

```

### State and Lifecycle

State and lifecycle methods are used to manage and respond to changes in a component's data over time.

### Functional Components with Hooks:

```jsx
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

### Class Components:

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

```

### Props

Props (short for properties) are read-only inputs passed to components, allowing data to flow from parent to child components.

### Example:

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Usage
<Welcome name="Sara" />

```

### Component Composition

React allows components to be composed together, making it easy to build complex UIs from simpler components.

### Example:

```jsx
function Avatar(props) {
  return <img src={props.user.avatarUrl} alt={props.user.name} />;
}

function UserInfo(props) {
  return (
    <div>
      <Avatar user={props.user} />
      <div>{props.user.name}</div>
    </div>
  );
}

function Comment(props) {
  return (
    <div>
      <UserInfo user={props.author} />
      <div>{props.text}</div>
      <div>{props.date}</div>
    </div>
  );
}

```

### Controlled vs. Uncontrolled Components

- **Controlled Components**: Form inputs whose values are controlled by the state of a React component.
    
    ```jsx
    class ControlledForm extends React.Component {
      constructor(props) {
        super(props);
        this.state = { value: '' };
    
        this.handleChange = this.handleChange.bind(this);
        this.handleSubmit = this.handleSubmit.bind(this);
      }
    
      handleChange(event) {
        this.setState({ value: event.target.value });
      }
    
      handleSubmit(event) {
        alert('A name was submitted: ' + this.state.value);
        event.preventDefault();
      }
    
      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Name:
              <input type="text" value={this.state.value} onChange={this.handleChange} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    
    ```
    
- **Uncontrolled Components**: Form inputs whose values are managed by the DOM itself.
    
    ```jsx
    class UncontrolledForm extends React.Component {
      constructor(props) {
        super(props);
        this.input = React.createRef();
      }
    
      handleSubmit = (event) => {
        alert('A name was submitted: ' + this.input.current.value);
        event.preventDefault();
      }
    
      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              Name:
              <input type="text" ref={this.input} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    
    ```
    

### Higher-Order Components (HOC)

HOCs are functions that take a component and return a new component, adding additional functionality.

### Example:

```jsx
function withLogger(WrappedComponent) {
  return class extends React.Component {
    componentDidMount() {
      console.log('Component mounted');
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
}

const EnhancedComponent = withLogger(MyComponent);

```

### Render Props

Render props are a technique for sharing code between React components using a prop whose value is a function.

### Example:

```jsx
class DataProvider extends React.Component {
  state = { data: null };

  componentDidMount() {
    fetchData().then(data => this.setState({ data }));
  }

  render() {
    return this.props.render(this.state.data);
  }
}

// Usage
<DataProvider render={data => (
  <div>{data ? `Data: ${data}` : 'Loading...'}</div>
)} />

```

Understanding these concepts will help you build robust and maintainable applications with React.