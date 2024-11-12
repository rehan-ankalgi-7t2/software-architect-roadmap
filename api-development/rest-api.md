> REST API, which stands for Representational State Transfer Application Programming Interface, is a set of architectural principles and constraints for designing and interacting with web services. REST is an architectural style that emerged as an alternative to SOAP (Simple Object Access Protocol) and other RPC (Remote Procedure Call)-based approaches for building web services.
> 

Key principles and characteristics of REST APIs include:

### 1. **Statelessness:**

- Each request from a client to a server contains all the information needed to understand and process the request. The server does not store any information about the client between requests.

### 2. **Client-Server Architecture:**

- The architecture is divided into client and server components, each with specific responsibilities. The client is responsible for the user interface and user experience, while the server is responsible for processing requests and managing resources.

### 3. **Uniform Interface:**

- REST APIs have a uniform and consistent interface, which simplifies interactions. The uniform interface is defined by several constraints:
    - **Resource Identification:** Resources are identified by URIs (Uniform Resource Identifiers).
    - **Resource Manipulation through Representations:** Clients manipulate resources through representations (e.g., JSON or XML).
    - **Self-Descriptive Messages:** Each message includes all the information needed to understand and process it.
    - **Hypermedia as the Engine of Application State (HATEOAS):** Clients interact with the application entirely through hypermedia provided dynamically by the application servers.

### 4. **Stateless Communication:**

- Each request from a client to a server must contain all the information needed to understand and process the request. The server does not store any client state between requests.

### 5. **Cacheability:**

- Responses from the server can be explicitly marked as cacheable or non-cacheable. Caching can be used to improve performance and reduce the load on servers.

### 6. **Layered System:**

- The architecture can be composed of multiple layers, with each layer performing a specific set of functions. Layers can be added or removed without affecting other layers.

### 7. **Resource-Based:**

- Resources, such as data objects or services, are identified by URIs. Resources can be manipulated using standard HTTP methods (GET, POST, PUT, DELETE).

### 8. **Stateful Interactions:**

- Stateful interactions are kept on the client, and each request from the client contains the necessary information to process the request.

### 9. **HTTP Methods:**

- RESTful APIs use standard HTTP methods (GET, POST, PUT, DELETE) to perform operations on resources. Each method has a specific meaning:
    - **GET:** Retrieve a representation of a resource.
    - **POST:** Create a new resource.
    - **PUT:** Update a resource or create it if it doesn't exist.
    - **DELETE:** Remove a resource.

### 10. **Data Formats:**

```
- Data is typically exchanged in standardized formats, such as JSON or XML, to ensure compatibility and ease of use.

```

REST APIs have become widely adopted for building web services due to their simplicity, scalability, and ease of use. They are commonly used in combination with HTTP and are the foundation of many modern web and mobile applications for data exchange between clients and servers.

# Creating a RESTful API using Node.js, Express, MongoDB, and Mongoose step by step.

### 1. **Setup Project:**

Create a new directory for your project and navigate into it:

```bash
mkdir node-express-mongodb-api
cd node-express-mongodb-api

```

Initialize your project and create a `package.json` file:

```bash
npm init -y

```

Install required dependencies:

```bash
npm install express mongoose body-parser

```

### 2. **Create Express App:**

Create an `index.js` file as the entry point for your application:

```jsx
// index.js
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());

// MongoDB connection
mongoose.connect('mongodb://localhost:27017/node-express-mongodb-api', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

// Define a simple model
const Todo = mongoose.model('Todo', { text: String });

// Routes
app.get('/', (req, res) => {
  res.send('Hello, this is the API!');
});

// Create a new todo
app.post('/todos', async (req, res) => {
  try {
    const todo = new Todo({ text: req.body.text });
    const savedTodo = await todo.save();
    res.json(savedTodo);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// Get all todos
app.get('/todos', async (req, res) => {
  try {
    const todos = await Todo.find();
    res.json(todos);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

```

### 3. **Run the Application:**

```bash
node index.js

```

Your API should now be running at `http://localhost:3000`. You can test it using tools like Postman or curl.

### 4. **Test the API:**

- **Create a Todo:**
    - Send a POST request to `http://localhost:3000/todos` with a JSON body:
        
        ```json
        {
          "text": "Learn Node.js and Express"
        }
        
        ```
        
- **Get all Todos:**
    - Send a GET request to `http://localhost:3000/todos`.

### 5. **Mongoose Schema and Validation:**

Define a Mongoose schema with validation for the Todo model:

```jsx
const mongoose = require('mongoose');

const todoSchema = new mongoose.Schema({
  text: {
    type: String,
    required: true,
    trim: true,
  },
});

const Todo = mongoose.model('Todo', todoSchema);

module.exports = Todo;

```

### 6. **Update Routes to Use Mongoose:**

Update the routes in `index.js` to use the Mongoose model:

```jsx
// index.js
const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const Todo = require('./models/todo');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());

// MongoDB connection
mongoose.connect('mongodb://localhost:27017/node-express-mongodb-api', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

// Routes
app.get('/', (req, res) => {
  res.send('Hello, this is the API!');
});

// Create a new todo
app.post('/todos', async (req, res) => {
  try {
    const todo = new Todo({ text: req.body.text });
    const savedTodo = await todo.save();
    res.json(savedTodo);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// Get all todos
app.get('/todos', async (req, res) => {
  try {
    const todos = await Todo.find();
    res.json(todos);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Start the server
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

```

### 7. **CRUD Operations:**

Enhance your API to support CRUD operations (Update and Delete):

```jsx
// Update a todo
app.put('/todos/:id', async (req, res) => {
  try {
    const todo = await Todo.findByIdAndUpdate(req.params.id, { text: req.body.text }, { new: true });
    res.json(todo);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// Delete a todo
app.delete('/todos/:id', async (req, res) => {
  try {
    const todo = await Todo.findByIdAndDelete(req.params.id);
    if (!todo) {
      return res.status(404).json({ error: 'Todo not found' });
    }
    res.json(todo);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

```

Now you can use these routes to perform CRUD operations on your Todo resources.

This example provides a basic structure for building a RESTful API using Node.js, Express, MongoDB, and Mongoose. Depending on your project requirements, you may want to add features such as user authentication, pagination, input validation, and more. Always consider security best practices and keep your dependencies up-to-date.

# Rest Api Design Guidelines

[adidas API Guidelines](https://adidas.gitbook.io/api-guidelines/)

https://github.com/CiscoDevNet/api-design-guide

https://github.com/microsoft/api-guidelines

https://github.com/watson-developer-cloud/api-guidelines

---

# Best Practices

Adhering to best practices is essential when designing and implementing RESTful APIs. Following these practices can enhance the usability, maintainability, and security of your APIs. Here are some REST API best practices:

### 1. **Use Meaningful Resource URIs:**

- Design URIs that are intuitive and reflect the resources they represent.
- Keep URIs lowercase and use hyphens or underscores for readability.

### 2. **Use HTTP Methods Appropriately:**

- Use `GET` for resource retrieval.
- Use `POST` for resource creation.
- Use `PUT` for resource updates (provide the full resource representation).
- Use `PATCH` for partial updates to a resource.
- Use `DELETE` for resource removal.

### 3. **Versioning:**

- Consider versioning your API to ensure backward compatibility.
- Include the version in the URI or headers (e.g., `/api/v1/resource`).

### 4. **Request and Response Formats:**

- Use JSON as the default format for request and response bodies.
- Support content negotiation for other formats (XML, etc.) using the `Accept` and `Content-Type` headers.

### 5. **Use Proper HTTP Status Codes:**

- Return appropriate HTTP status codes with each response.
- Use `200 OK` for successful `GET` requests, `201 Created` for successful `POST` and `PUT` requests, `204 No Content` for successful `DELETE` requests.
- Use `400 Bad Request` for client errors and `404 Not Found` for resources that don't exist.
- Use `401 Unauthorized` for authentication failures and `403 Forbidden` for authorization failures.
- Use `500 Internal Server Error` for server errors.

### 6. **Consistent Resource Naming:**

- Keep resource names consistent throughout the API.
- Use plural nouns for resource names (e.g., `/users` instead of `/user`).

### 7. **Use Proper Pagination:**

- Implement pagination for large sets of data using query parameters (e.g., `?page=1&limit=10`).
- Provide links to the next and previous pages in the response.

### 8. **Filtering, Sorting, and Searching:**

- Allow clients to filter, sort, and search resources using query parameters.
- Use query parameters like `?filter=`, `?sort=`, and `?search=`.

### 9. **Error Handling:**

- Provide detailed error messages with sufficient information for clients to understand and resolve issues.
- Include error codes and descriptions in error responses.

### 10. **Use HATEOAS (Hypermedia as the Engine of Application State):**

- Include links in responses to guide clients on what actions they can perform next.
- Helps in making the API more discoverable and self-explanatory.

### 11. **Implement Rate Limiting:**

- Protect your API from abuse by implementing rate limiting.
- Include rate limit information in headers (e.g., `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`).

### 12. **Security Best Practices:**

- Use HTTPS to encrypt data in transit.
- Authenticate and authorize users using secure methods (e.g., OAuth 2.0).
- Sanitize input to prevent injection attacks.
- Protect against Cross-Site Request Forgery (CSRF) and Cross-Site Scripting (XSS) attacks.

### 13. **Documentation:**

- Provide comprehensive and up-to-date documentation for your API.
- Use tools like Swagger or OpenAPI to generate API documentation.

### 14. **Testing:**

- Implement thorough unit testing and integration testing.
- Consider providing a sandbox environment for developers to test their integrations.

### 15. **Logging and Monitoring:**

- Implement logging to track API usage and errors.
- Use monitoring tools to track performance metrics and detect issues proactively.

### 16. **CORS (Cross-Origin Resource Sharing):**

- Configure CORS headers to allow or restrict cross-origin requests.

### 17. **Use Content Negotiation:**

- Use the `Accept` header to negotiate the response format based on client preferences.

### 18. **Statelessness:**

- Design APIs to be stateless, meaning each request from a client contains all the information needed to fulfill that request.

### 19. **Implement Cache-Control:**

- Use caching headers (e.g., `Cache-Control`) to control caching behavior.

### 20. **Educate API Consumers:**

- Provide documentation, tutorials, and examples to help developers understand how to use your API effectively.

Adhering to these best practices can contribute to the creation of a robust, user-friendly, and secure RESTful API. Keep in mind that best practices may evolve, so it's essential to stay informed about the latest developments in API design and development.

---

# ❌ API Design mistakes and how to avoid them

## 1. Naming conventions

- use lowercase
- avoid verbs as route name
- use plurals as route names ex: /posts
- hyphenate the complicated route names

## 2.Improper Use of HTTP Methods
- Use GET for retrieval.
- Use POST for creating resources.
- Use PUT for full updates or creation if the resource doesn't exist.
- Use PATCH for partial updates.
- Use DELETE for removing resources.
## 3. Not Versioning the API
- Include versioning in the URI (e.g., /api/v1/resource) or headers.
- Use semantic versioning to indicate changes.
## 4. Ignoring Error Handling
- Use meaningful HTTP status codes (e.g., 400 for bad requests, 404 for missing resources).
- Provide detailed error messages with error codes and descriptions.
- Use a consistent error response structure.
## 5. Lack of Pagination, Filtering, and Sorting
- Use query parameters for pagination (e.g., ?page=1&limit=20).
- Enable filtering and sorting with query parameters (e.g., ?filter=name&sort=asc).
## 6. Ignoring Statelessness
- Design APIs to be stateless, where each request contains all necessary information.
- Use tokens for authentication (e.g., JWT).
## 7. Improper Use of HTTP Status Codes
- Return appropriate codes: 201 for creation, 204 for successful deletions, 400 for bad requests, 401 for unauthorized, and 500 for server errors.
## 8. No Proper Documentation
- Use tools like Swagger or OpenAPI for comprehensive and interactive documentation.
- Update the documentation as the API evolves.
## 9. Security Missteps
- Always use HTTPS for secure communication.
- Implement authentication (OAuth 2.0, API keys) and input validation.
- Sanitize inputs to prevent SQL injection and XSS attacks.
## 10. Overloading Endpoints
- Follow a single responsibility principle for endpoints.
- Split logic into different endpoints for clarity and maintainability.
## 11. Ignoring Caching
- Use caching headers (e.g., Cache-Control, ETag) to improve performance.
Implement client-side caching strategies.
## 12. Lack of Consistency
- Standardize naming conventions and response structures.
- Use tools like linters or API style guides to enforce consistency.
## 13. Not Using Hypermedia (HATEOAS)
- Include links in responses for discoverability (e.g., next, previous, related).
## 14. No Rate Limiting
- Implement rate limiting with headers like X-RateLimit-Limit and X-RateLimit-Remaining.
- Return 429 Too Many Requests for exceeded limits.
