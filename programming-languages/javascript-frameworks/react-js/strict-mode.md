**StrictMode** currently helps with the following issues:

- **Identifying components with unsafe lifecycle methods**: Certain lifecycle methods are unsafe to use in asynchronous react applications. With the use of third-party libraries, it becomes difficult to ensure that certain lifecycle methods are not used.StrictMode helps in providing us with a warning if any of the class components use an unsafe lifecycle method.

- **Warning about the usage of legacy string API**:If one is using an older version of React, callback ref is the recommended way to manage refs instead of using the string refs. StrictMode gives a warning if we are using string refs to manage refs.

- **Warning about the usage of findDOMNode**:Previously, findDOMNode( ) method was used to search the tree of a DOM node. This method is deprecated in React. Hence, the StrictMode gives us a warning about the usage of this method.Warning about the usage of legacy context API (because the API is error-prone