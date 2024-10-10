Express is a minimal and flexible Node.js web application framework that provides a robust set of features to build single-page, multi-page, and hybrid web applications. One of the core features of Express is its routing functionality, which allows you to define endpoints and handle requests for your application.

### Setting Up Express

First, you need to install Express. You can do this using npm:

```bash
npm install express

```

### Basic Express Server

Here's a simple example to set up an Express server:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Basic Routing

In Express, routing refers to how an application’s endpoints (URIs) respond to client requests. You can define routes using methods like `app.get()`, `app.post()`, `app.put()`, `app.delete()`, etc.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// GET request to the homepage
app.get('/', (req, res) => {
  res.send('GET request to the homepage');
});

// POST request to the homepage
app.post('/', (req, res) => {
  res.send('POST request to the homepage');
});

// PUT request to /user
app.put('/user', (req, res) => {
  res.send('PUT request to /user');
});

// DELETE request to /user
app.delete('/user', (req, res) => {
  res.send('DELETE request to /user');
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Route Parameters

Route parameters are named URL segments that are used to capture values specified at their position in the URL. You can define route parameters using the colon syntax.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params);
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

If you visit `http://localhost:3000/users/123/books/456`, you will get a response with the route parameters:

```json
{
  "userId": "123",
  "bookId": "456"
}

```

### Query Parameters

Query parameters are key-value pairs that appear after the question mark in a URL. They can be accessed using `req.query`.

### Example:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/search', (req, res) => {
  res.send(req.query);
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

If you visit `http://localhost:3000/search?keyword=nodejs&sort=asc`, you will get a response with the query parameters:

```json
{
  "keyword": "nodejs",
  "sort": "asc"
}

```

### Handling Different HTTP Methods

Express provides methods for all HTTP verbs. Here’s an example of handling different HTTP methods for the same route:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

app.route('/user')
  .get((req, res) => {
    res.send('GET request to /user');
  })
  .post((req, res) => {
    res.send('POST request to /user');
  })
  .put((req, res) => {
    res.send('PUT request to /user');
  })
  .delete((req, res) => {
    res.send('DELETE request to /user');
  });

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

### Middleware

Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application’s request-response cycle. They can perform various tasks such as executing code, modifying the request and response objects, ending the request-response cycle, and calling the next middleware function.

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

### Using Express Router

Express Router is a class that helps in creating modular, mountable route handlers. A Router instance is a complete middleware and routing system.

### Example:

```jsx
const express = require('express');
const app = express();
const router = express.Router();
const PORT = 3000;

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

### Summary

- **Setting Up Express**: Install and require Express, create an application instance.
- **Basic Routing**: Define routes using methods like `app.get()`, `app.post()`, etc.
- **Route Parameters**: Capture values from the URL using route parameters.
- **Query Parameters**: Access query parameters from the URL.
- **Handling Different HTTP Methods**: Use `app.route()` to handle multiple HTTP methods for a single route.
- **Middleware**: Use middleware functions for tasks like logging, modifying requests and responses, etc.
- **Express Router**: Create modular route handlers using `express.Router()`.

By leveraging these features, you can create complex and efficient routing structures in your Express applications.