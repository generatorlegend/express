# Error Handling in Express.js

Express.js provides powerful error handling mechanisms to help you manage and respond to errors in your application. This guide will walk you through various error handling techniques, including how to create and use error-handling middleware, and best practices for handling different types of errors.

## Table of Contents

1. [Built-in Error Handler](#built-in-error-handler)
2. [Custom Error-Handling Middleware](#custom-error-handling-middleware)
3. [Handling 404 Errors](#handling-404-errors)
4. [Asynchronous Error Handling](#asynchronous-error-handling)
5. [Best Practices](#best-practices)

## Built-in Error Handler

Express comes with a built-in error handler that takes care of any errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack.

If you pass an error to `next()` and you don't handle it in a custom error handler, it will be handled by the built-in error handler; the error will be written to the client with the stack trace.

```javascript
app.get('/', function (req, res) {
  throw new Error('Something went wrong');
});
```

The built-in error handler will catch this error and send a response to the client.

## Custom Error-Handling Middleware

You can create custom error-handling middleware to handle errors in a way that suits your application's needs. Error-handling middleware are defined in the same way as other middleware functions, except they take four arguments instead of three: `(err, req, res, next)`.

Here's an example of a custom error-handling middleware:

```javascript
app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

In the provided codebase, we can see an example of custom error handling in the `examples/mvc/index.js` file:

```javascript
app.use(function(err, req, res, next){
  // log it
  if (!module.parent) console.error(err.stack);

  // error page
  res.status(500).render('5xx');
});
```

This middleware logs the error stack (when not running as a module) and renders a '5xx' error page.

## Handling 404 Errors

In Express, 404 responses are not the result of an error, so the error-handler middleware will not capture them. To handle 404 responses, you can add a middleware function at the very bottom of the middleware function stack (below all other functions) to handle a 404 response:

```javascript
app.use(function(req, res, next) {
  res.status(404).send("Sorry can't find that!")
});
```

In the provided example (`examples/mvc/index.js`), we see a similar approach:

```javascript
app.use(function(req, res, next){
  res.status(404).render('404', { url: req.originalUrl });
});
```

This middleware renders a '404' view, passing the original URL that was not found.

## Asynchronous Error Handling

For errors returned from asynchronous functions invoked by route handlers and middleware, you must pass them to the `next()` function, where Express will catch and process them. For example:

```javascript
app.get('/', function (req, res, next) {
  fs.readFile('/file-does-not-exist', function (err, data) {
    if (err) {
      next(err); // Pass errors to Express.
    } else {
      res.send(data);
    }
  });
});
```

## Best Practices

1. **Use try-catch blocks**: For synchronous code, use try-catch to catch errors and pass them to Express:

   ```javascript
   app.get('/', function (req, res, next) {
     try {
       // Your code here
     } catch (err) {
       next(err);
     }
   });
   ```

2. **Handle errors in promises**: For promise-based operations, use `.catch()` to handle errors:

   ```javascript
   app.get('/', function (req, res, next) {
     Promise.resolve()
       .then(function () {
         // Your code here
       })
       .catch(next); // Errors will be passed to Express
   });
   ```

3. **Log errors**: Always log errors for debugging purposes. In the provided example, we see error logging:

   ```javascript
   if (!module.parent) console.error(err.stack);
   ```

4. **Set appropriate status codes**: Ensure you're setting the correct HTTP status code for different types of errors.

5. **Consider using a robust error handling library**: For more complex applications, consider using libraries like `express-error-handler` or `http-errors` for more sophisticated error handling.

By following these practices and understanding Express's error handling mechanisms, you can create more robust and maintainable applications that gracefully handle errors and provide a better experience for your users.