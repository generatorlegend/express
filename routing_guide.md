# Express.js Routing Guide

Routing is a fundamental concept in Express.js that determines how an application responds to client requests to specific endpoints. This guide will cover basic and advanced routing techniques, route parameters, and route handlers.

## Basic Routing

In Express.js, you define routes using methods that correspond to HTTP verbs. The most common methods are:

- `app.get()`: Handle GET requests
- `app.post()`: Handle POST requests
- `app.put()`: Handle PUT requests
- `app.delete()`: Handle DELETE requests

Here's a basic example of route definition:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.post('/submit', (req, res) => {
  res.send('Form submitted');
});
```

## Route Parameters

Route parameters allow you to capture values specified at specific positions in the URL. You can define route parameters using the colon syntax:

```javascript
app.get('/user/:id', (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});
```

In this example, `:id` is a route parameter. You can access its value using `req.params.id`.

## Route Handlers

Route handlers are functions that are executed when a matching route is found. They have access to the request and response objects, and can perform operations such as sending responses, manipulating data, or calling other middleware.

```javascript
function handleUserRequest(req, res, next) {
  // Perform operations
  next();
}

app.get('/user/:id', handleUserRequest, (req, res) => {
  res.send('User details');
});
```

You can chain multiple handlers for a single route, which is useful for modularizing your code and applying middleware.

## Advanced Routing Techniques

### Route Chaining

Express allows you to chain route handlers for different HTTP methods on the same path:

```javascript
app.route('/book')
  .get((req, res) => {
    res.send('Get a book');
  })
  .post((req, res) => {
    res.send('Add a book');
  })
  .put((req, res) => {
    res.send('Update a book');
  });
```

### Express Router

For larger applications, you can use `express.Router()` to create modular, mountable route handlers:

```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('Home page');
});

router.get('/about', (req, res) => {
  res.send('About page');
});

app.use('/', router);
```

### Regular Expression Routes

You can use regular expressions in your routes for more flexible matching:

```javascript
app.get(/.*fly$/, (req, res) => {
  res.send('URL ends with "fly"');
});
```

## Error Handling in Routes

To handle errors in routes, you can pass them to the `next()` function:

```javascript
app.get('/error', (req, res, next) => {
  const err = new Error('Something went wrong');
  next(err);
});

app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

## Conclusion

Routing is a powerful feature in Express.js that allows you to structure your application's endpoints efficiently. By mastering these routing techniques, you can create more organized and maintainable Express.js applications.

Remember to consult the official Express.js documentation for more detailed information and advanced usage scenarios.