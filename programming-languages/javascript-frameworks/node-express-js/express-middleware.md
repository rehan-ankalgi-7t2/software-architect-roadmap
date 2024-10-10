Express middleware are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application’s request-response cycle. Middleware functions can perform various tasks such as executing code, modifying the request and response objects, ending the request-response cycle, and calling the next middleware function.

### Types of Middleware

1. **Application-level middleware**
2. **Router-level middleware**
3. **Error-handling middleware**
4. **Built-in middleware**
5. **Third-party middleware**

### Application-Level Middleware

Application-level middleware is bound to an instance of the `express` object using `app.use()` or `app.METHOD()`.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware function to log request details
app.use((req, res, next) => {
  console.log(`${req.method} request for '${req.url}'`);
  next();
});

// Define a route
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Router-Level Middleware

Router-level middleware works in the same way as application-level middleware, except it is bound to an instance of `express.Router()`.

### Example:

```jsx
const express = require('express');
const app = express();
const router = express.Router();
const PORT = 3000;

// Middleware function to log request details
router.use((req, res, next) => {
  console.log(`${req.method} request for '${req.url}'`);
  next();
});

// Define routes using the router
router.get('/', (req, res) => {
  res.send('Home page');
});

router.get('/about', (req, res) => {
  res.send('About page');
});

// Use the router
app.use('/', router);

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Error-Handling Middleware

Error-handling middleware functions are defined with four arguments: (err, req, res, next). They must be defined after all other app.use() and routes calls.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Route that causes an error
app.get('/error', (req, res, next) => {
  const err = new Error('Something went wrong!');
  err.status = 500;
  next(err);
});

// Error-handling middleware
app.use((err, req, res, next) => {
  res.status(err.status || 500);
  res.send({
    error: {
      message: err.message
    }
  });
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Built-in Middleware

Express comes with several built-in middleware functions. They are:

- `express.static` to serve static files.
- `express.json` to parse incoming JSON requests.
- `express.urlencoded` to parse URL-encoded bodies.

### Example:

```jsx
const express = require('express');
const path = require('path');
const app = express();
const PORT = 3000;

// Use built-in middleware to serve static files
app.use(express.static(path.join(__dirname, 'public')));

// Use built-in middleware to parse JSON requests
app.use(express.json());

// Use built-in middleware to parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

// Define a route
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Third-Party Middleware

You can use third-party middleware to add additional functionality to your Express application. Some popular third-party middleware are:

- `morgan`: HTTP request logger middleware
- `cors`: Middleware to enable Cross-Origin Resource Sharing (CORS)
- `body-parser`: Middleware to parse incoming request bodies

### Example:

```jsx
const express = require('express');
const morgan = require('morgan');
const cors = require('cors');
const bodyParser = require('body-parser');
const app = express();
const PORT = 3000;

// Use third-party middleware
app.use(morgan('dev'));
app.use(cors());
app.use(bodyParser.json());

// Define a route
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Custom Middleware

You can also create your own custom middleware functions to perform specific tasks in your application.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Custom middleware to log the request method and URL
const logRequestDetails = (req, res, next) => {
  console.log(`${req.method} request for '${req.url}'`);
  next();
};

// Use custom middleware
app.use(logRequestDetails);

// Define a route
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Summary

Middleware in Express allows you to execute code, make changes to the request and response objects, end the request-response cycle, and call the next middleware function in the stack. By using different types of middleware, you can create robust and maintainable applications.

- **Application-Level Middleware**: Bound to an instance of `express`.
- **Router-Level Middleware**: Bound to an instance of `express.Router()`.
- **Error-Handling Middleware**: Used for handling errors, defined with four arguments.
- **Built-In Middleware**: Provided by Express for common tasks.
- **Third-Party Middleware**: Added functionality through npm packages.
- **Custom Middleware**: Custom functions created to perform specific tasks.

By effectively using middleware, you can handle various aspects of HTTP requests and responses in your Express applications.