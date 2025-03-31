# Getting Started with Express.js

Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. This guide will walk you through the process of installing Express.js, setting up a basic application, and creating a simple "Hello World" example.

## Installation

Before you begin, make sure you have Node.js installed on your system. Then, follow these steps to install Express.js:

1. Create a new directory for your project and navigate to it:

```bash
mkdir my-express-app
cd my-express-app
```

2. Initialize a new Node.js project:

```bash
npm init -y
```

3. Install Express.js as a dependency:

```bash
npm install express
```

## Creating a Simple Application

Let's create a basic "Hello World" application using Express.js. Create a new file called `app.js` in your project directory and add the following code:

```javascript
'use strict';

const express = require('express');
const app = express();

app.get('/', function(req, res) {
  res.send('Hello World');
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Express started on port ${PORT}`);
});
```

Let's break down this code:

1. We require the `express` module and create an instance of the Express application.
2. We define a route handler for GET requests to the root path ('/').
3. When a request is received, we send the response "Hello World".
4. Finally, we start the server on port 3000.

## Running the Application

To run your application, use the following command in your terminal:

```bash
node app.js
```

You should see the message "Express started on port 3000" in your console. Open a web browser and navigate to `http://localhost:3000`. You should see the "Hello World" message displayed.

## Next Steps

Congratulations! You've created your first Express.js application. Here are some next steps to explore:

1. Learn about routing and how to handle different HTTP methods.
2. Explore middleware and how it can be used to process requests.
3. Integrate with a database to create a full-stack application.
4. Implement error handling and logging for your application.

For more advanced usage and detailed documentation, refer to the official Express.js documentation.

Happy coding with Express.js!