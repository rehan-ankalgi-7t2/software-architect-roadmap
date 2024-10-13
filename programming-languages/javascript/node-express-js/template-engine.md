Template engines in Node.js are tools that allow you to generate HTML markup dynamically by using templates and data. They simplify the process of creating HTML content by separating the structure (HTML) from the data (JavaScript variables). There are several popular template engines available for Node.js:

### 1. **Pug (formerly Jade)**

Pug is a high-performance template engine heavily influenced by Haml and implemented with JavaScript for Node.js. It uses indentation-based syntax and supports includes, mixins, filters, and more.

### Example:

```
// example.pug
html
  head
    title= pageTitle
  body
    h1 Users
    ul
      each user in users
        li= user.name

```

### 2. **EJS (Embedded JavaScript)**

EJS is a simple template language that lets you generate HTML markup with plain JavaScript. It uses `<% %>` tags to embed JavaScript code into your HTML markup.

### Example:

```
<!-- example.ejs -->
<html>
  <head>
    <title><%= pageTitle %></title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      <% users.forEach(function(user) { %>
        <li><%= user.name %></li>
      <% }); %>
    </ul>
  </body>
</html>

```

### 3. **Handlebars**

Handlebars provides a logic-less template syntax that allows you to build semantic templates without extra syntax. It supports helpers and partials for more complex templates.

### Example:

```
<!-- example.handlebars -->
<html>
  <head>
    <title>{{pageTitle}}</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      {{#each users}}
        <li>{{name}}</li>
      {{/each}}
    </ul>
  </body>
</html>

```

### 4. **Mustache**

Mustache is a logic-less template syntax that can be used for HTML, config files, source code, and more. It works by expanding tags in a template using values provided in a hash or object.

### Example:

```
<!-- example.mustache -->
<html>
  <head>
    <title>{{pageTitle}}</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      {{#users}}
        <li>{{name}}</li>
      {{/users}}
    </ul>
  </body>
</html>

```

### Choosing a Template Engine

When choosing a template engine for your Node.js application, consider factors such as syntax preferences, performance, community support, and integration with your existing stack. Each template engine has its own syntax and features, so the choice often depends on personal preference and specific project requirements.

### Integrating Template Engines with Express

To use template engines with Express, you typically set the `view engine` and specify the directory where your views (templates) are located.

### Example with Express and EJS:

```jsx
const express = require('express');
const app = express();
const PORT = 3000;

// Set EJS as the view engine
app.set('view engine', 'ejs');
app.set('views', './views');

// Example route rendering a view with data
app.get('/', (req, res) => {
  const pageTitle = 'User List';
  const users = [
    { name: 'John Doe' },
    { name: 'Jane Doe' },
    { name: 'Alice Smith' }
  ];
  res.render('example', { pageTitle, users });
});

app.listen(PORT, () => {
  console.log(`Server is running on <http://localhost>:${PORT}`);
});

```

In this example, when you visit `http://localhost:3000/`, Express will render the `example.ejs` template (located in the `./views` directory) and pass the `pageTitle` and `users` variables to the template for rendering.

### Summary

Template engines in Node.js like Pug, EJS, Handlebars, and Mustache provide ways to generate dynamic HTML content by separating structure and data. They simplify the process of building web applications and are widely used in conjunction with frameworks like Express for server-side rendering. Choosing the right template engine depends on factors such as syntax preferences, features, and integration requirements with your application stack.