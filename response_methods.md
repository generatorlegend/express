# Response Methods in Express.js

Express.js provides a rich set of methods to handle HTTP responses. This guide covers the most commonly used response methods, their usage, and examples.

## Table of Contents

1. [Sending Responses](#sending-responses)
2. [Setting Headers](#setting-headers)
3. [Redirects](#redirects)
4. [Rendering Views](#rendering-views)
5. [Sending Files](#sending-files)
6. [Cookies](#cookies)

## Sending Responses

### res.send()

Sends a response of various types.

```javascript
res.send(Buffer.from('whoop'));
res.send({ some: 'json' });
res.send('<p>some html</p>');
res.status(404).send('Sorry, we cannot find that!');
```

### res.json()

Sends a JSON response.

```javascript
res.json(null);
res.json({ user: 'tobi' });
res.status(500).json({ error: 'message' });
```

### res.sendStatus()

Sets the response status code and sends its string representation as the response body.

```javascript
res.sendStatus(200); // equivalent to res.status(200).send('OK')
res.sendStatus(403); // equivalent to res.status(403).send('Forbidden')
res.sendStatus(404); // equivalent to res.status(404).send('Not Found')
res.sendStatus(500); // equivalent to res.status(500).send('Internal Server Error')
```

## Setting Headers

### res.set()

Sets response headers.

```javascript
res.set('Content-Type', 'text/plain');

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  'ETag': '12345'
});
```

### res.type()

Sets the Content-Type HTTP header.

```javascript
res.type('.html');              // => 'text/html'
res.type('html');               // => 'text/html'
res.type('json');               // => 'application/json'
res.type('application/json');   // => 'application/json'
res.type('png');                // => 'image/png'
```

## Redirects

### res.redirect()

Redirects to the URL derived from the specified path.

```javascript
res.redirect('/foo/bar');
res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login');
```

## Rendering Views

### res.render()

Renders a view template.

```javascript
// Send the rendered view to the client
res.render('index');

// Pass a local variable to the view
res.render('user', { name: 'Tobi' });
```

## Sending Files

### res.sendFile()

Transfers the file at the given path.

```javascript
res.sendFile('/path/to/avatar.png');
res.sendFile('filename', { root: __dirname + '/public' });
```

### res.download()

Transfers the file at path as an "attachment".

```javascript
res.download('/report-12345.pdf');
res.download('/report-12345.pdf', 'report.pdf');
```

## Cookies

### res.cookie()

Sets cookie name to value.

```javascript
res.cookie('name', 'tobi', { domain: '.example.com', path: '/admin', secure: true });
res.cookie('rememberme', '1', { expires: new Date(Date.now() + 900000), httpOnly: true });
```

### res.clearCookie()

Clears the cookie specified by name.

```javascript
res.clearCookie('name');
```

Remember that most of these methods are chainable, allowing you to write expressive and concise code:

```javascript
res.status(404)
   .set('Content-Type', 'text/plain')
   .send('Not found');
```

This guide covers the most commonly used response methods in Express.js. For more detailed information and additional methods, refer to the official Express.js documentation.