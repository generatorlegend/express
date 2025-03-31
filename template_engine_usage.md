# Template Engine Usage in Express.js

Express.js provides a powerful and flexible way to render dynamic content using template engines. This guide will walk you through setting up and using template engines in your Express.js applications.

## Setting Up a Template Engine

To use a template engine with Express.js, you need to set it up in your application. Here's how:

1. Install the template engine of your choice. For example, to use EJS:

   ```
   npm install ejs
   ```

2. Set the view engine in your Express application:

   ```javascript
   app.set('view engine', 'ejs');
   ```

3. Optionally, set the directory where your views are located:

   ```javascript
   app.set('views', path.join(__dirname, 'views'));
   ```

## Supported Template Engines

Express.js supports various template engines out of the box. Some popular ones include:

- EJS
- Pug
- Handlebars
- Nunjucks

You can use any template engine that provides a `__express` interface or can be adapted to work with Express.

## Rendering Views

To render a view, use the `res.render()` method in your route handlers. Here's an example:

```javascript
app.get('/', (req, res) => {
  res.render('index', { title: 'Welcome' });
});
```

This renders the `index` view (e.g., `index.ejs` for EJS) and passes a `title` variable to the template.

## Passing Data to Templates

You can pass data to your templates as an object in the second argument of `res.render()`:

```javascript
app.get('/user/:id', (req, res) => {
  const userData = {
    id: req.params.id,
    name: 'John Doe',
    email: 'john@example.com'
  };
  res.render('user', { user: userData });
});
```

In your template, you can then access this data. For example, in EJS:

```ejs
<h1>User Profile</h1>
<p>Name: <%= user.name %></p>
<p>Email: <%= user.email %></p>
```

## Using Different Engines for Different Views

You can use multiple template engines in a single Express application. To do this, specify the engine when calling `res.render()`:

```javascript
app.get('/', (req, res) => {
  res.render('index.pug', { title: 'Home' });
});

app.get('/about', (req, res) => {
  res.render('about.ejs', { title: 'About' });
});
```

## Caching Templates

By default, template caching is enabled in production mode. To enable it in development:

```javascript
app.enable('view cache');
```

To disable it:

```javascript
app.disable('view cache');
```

## Custom Rendering Function

You can create a custom rendering function using `app.engine()`. This is useful for template engines that don't provide a `__express` interface:

```javascript
app.engine('html', require('ejs').renderFile);
```

This allows you to use the `.html` extension with the EJS engine.

Remember to consult the documentation of your chosen template engine for specific usage instructions and features.