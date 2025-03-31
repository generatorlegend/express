# Middleware Usage in Express.js

Middleware functions are a fundamental concept in Express.js that allow you to execute code during the request-response cycle. They can perform various tasks, such as modifying request and response objects, ending the request-response cycle, or calling the next middleware function in the stack.

## Table of Contents

1. [Understanding Middleware](#understanding-middleware)
2. [Built-in Middleware](#built-in-middleware)
3. [Custom Middleware](#custom-middleware)
4. [Middleware Order](#middleware-order)
5. [Error-Handling Middleware](#error-handling-middleware)

## Understanding Middleware

In Express.js, middleware functions have access to the request object (req), the response object (res), and the next middleware function in the application's request-response cycle, commonly denoted by a variable named `next`.

Middleware functions can:

- Execute any code
- Make changes to the request and response objects
- End the request-response cycle
- Call the next middleware function in the stack

## Built-in Middleware

Express.js comes with several built-in middleware functions that you can use in your applications. Here are some commonly used ones:

### express.static

Serves static files, such as images, CSS, and JavaScript.

```javascript
app.use(express.static(path.join(__dirname, 'public')));
```

### express.json

Parses incoming requests with JSON payloads.

```javascript
app.use(express.json());
```

### express.urlencoded

Parses incoming requests with URL-encoded payloads.

```javascript
app.use(express.urlencoded({ extended: true }));
```

## Custom Middleware

You can create your own middleware functions to perform custom operations. Here's an example of a simple logging middleware:

```javascript
const loggingMiddleware = (req, res, next) => {
  console.log(`${new Date().toISOString()}: ${req.method} ${req.url}`);
  next();
};

app.use(loggingMiddleware);
```

## Middleware Order

The order in which middleware is added to your application is important. Middleware functions are executed sequentially in the order they are added. For example:

```javascript
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(loggingMiddleware);

// Route handlers
app.get('/', (req, res) => {
  res.send('Hello, World!');
});
```

In this case, the `express.json()` and `express.urlencoded()` middleware will process the request before it reaches the logging middleware and the route handler.

## Error-Handling Middleware

Error-handling middleware functions are defined with four arguments instead of three, specifically with the signature (err, req, res, next):

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something went wrong!');
});
```

Make sure to add error-handling middleware last, after other `app.use()` and routes calls.

By understanding and effectively using middleware in Express.js, you can create more modular, maintainable, and feature-rich web applications.