---
layout: default
title: "JavaScript: Node.js"
date: 2022-01-26 22:00:00
categories: JavaScript
---

### What is Node.js?

- Node.js is a platform for interpreting JS code and running apps.

- Google Chrome's JavaScript engine, and able to support JS as a server-side language.

### Overview: Client-side(front-end) VS Server-side(back-end) in Web dev

- Client-side : refers to the code you write that results in something the user sees in his web browser.

- Sever-side : refers to code which is responsible for authenticating users on a login page, running scheduled tasks, and even ensuring that the client-side code reaches the client.

- Full stack development, using JavaScript, defines the new development in which JavaScript is usezd on the server and client, as well as on devices, hardware, and architectures it didn’t exist on before.

### Node.js Event-loop

- Operates on an event loop using a single thread.

![node.js_loop Image](https://github.com/Hyukjoo-Lee/Hyukjoo-Lee.github.io/blob/main/_posts/images/node.js_loop.png?raw=true "node.js_loop Image")

- REPL commands (Read Eval Print Loop)

- Command examples
  - .break - Exits a block within the REPL session &rarr; if you get stuck in a block of code
  - .editor - Opens an internal editor, ctrl-d &rarr; saves and quit the editor

### Running your js file with Node.js

- Node.js JS engine can interpret your code from the terminal when you navigate to the location of a JS file and preface the filename with the node keyword

- node <filename.js>

- Running individul JS commands

```javascript
let messages = ["message A", "message B", "message C", "message D"];
// .load message.js
// interpret your code from the terminal
// messages.forEach(message => console.log(message));
```

- For your app to stay organized and efficient, JS files need to have access to one another's contents when neccesary.

- Each js files or folder containing a code library is called a <em>module</em>

### npm

- package manager for Node.js which is reponsible for managing the external packages in your application

- Commands

  - init : Intialize a Node.js app and creates a package.json file
  - install : Install a Node.js package
  - publish : Saves and uploads a package you build to the npm package community
  - start : Runs your Node.js application; start a package
  - stop : Quits the running application
  - docs `<package> ` : Opens the likely doc page(web page) for your specified package

- npm install <package>, appending --save to your command, installs the package as a dependency for your application
  e.g. npm install express -S

- Every Node.js app or module contains a 'package.json' file to define the properties of that project

- Typically, this file is where you specify the version of your current release, the name of your app, and the main app file.

**Node.js application structure with node_module**

![node.js structure image](https://github.com/Hyukjoo-Lee/Hyukjoo-Lee.github.io/blob/main/_posts/images/node.jsstructure.png?raw=true "node.js structure")

### Building a simple web server in node.js

**Web servers and HTTP**

- A web server is a software designed to respond to request over the internet by loading or processing data.

- Web servers follow HTTP, a stadardized system observed for the viewing of web pages and sending of data over the internet

  - POST : Request info from a server; such as by clicking a link to see the home page
  - GET : Send info to the server; such as filling out and submitting a sign-up form

- HTTPS : Hypertext transfer protocol secure (HTTPS) is the secure version of HTTP, which is the primary protocol used to send data between a web browser and a website

- e.g. When you enter the URL , you wnat to see in your browser, an HTTP request is sent to a physical computer elsewhere; this request contains some info whether you want to load a web page or send info to that computer.

**Source code**

```javascript
const port = 3000,
  // Require the http and http-status-codes modules
  http = require("http"),
  httpStatus = require("http-status-codes"),
  // Create the server with request and response params
  app = http.createServer((request, response) => {
    console.log("Received an incoming request!");
    response.writeHead(httpStatus, {
      "Content-Type": "text/html",
    });
    // Write the response to the client
    let responseMessage = "<h1>Hello, Universe!</h1>";
    response.write(responseMessage);
    response.end();
    console.log(`Sent a response : ${responseMessage}`);
  });
// Tell the application server to listen on port 3000
app.listen(port);
console.log(`The server has started and is listening on port number: ${port}`);
```

### Callbacks in Node.js

- Part of what makes Node.js so fast and efficient is its use of callbacks.

- A callback is an anonymous function that is set up to be invoked as soon as another function completes.

**Callbacks on the server indicate when to respond to the server**

1. Multiple clients may take a series of requests to the server
2. As requests are received by the server, they are processed asynchronously.
3. The server takes time to process each individual request. A callback may signal when a response is ready.
4. Responses may not be returned in the order requests are received.
5. Clients will receive their responses in time relative to request processing time.

```javascript
const port = 3000,
  http = require("http"),
  httpStatus = require("http-status-codes"),
  app = http.createServer();
// Listen for requests
app.on("request", (req, res) => {
  res.writeHead(httpStatus, {
    "Content-Type": "text/html",
  });
  // Prepare response
  let responseMessage = "<h1>This will show on the screen.</h1>";
  // Respond with HTML
  res.end(responseMessage);
});
app.listen(port);
console.log(`The server has started and is listening on port number: ${port}`);
```

**How you are going to build your routes**

- Routing is the way for your app to determine how to respond to a requesting client.
- Some routes are designed by matching the URL in the request object
- Each request has url property

```javascript
// This code will have a server object that has a callback function, (req,res) => {}
// which is run every time a request is made to the server

// A simple server with a request event listener
const port = 3000,
  http = require("http"),
  httpStatus = require("http-status-codes"),
  app = http.createServer();
// Listen for requests
app.on("request", (req, res) => {
  console.log("method " + req.method);
  console.log("url" + req.url);
  console.log("header" + req.headers);

  const getJSONString = (obj) => {
    return JSON.stringify(obj, null, 2);
  };

  console.log(`Headers: ${getJSONString(req.headers)}`);

  // Test this property and two other properties by logging them
  res.writeHead(httpStatus.OK, {
    "Content-Type": "text/html",
  });
  // Prepare response
  let responseMessage = "<h1>This will show on the screen.</h1>";
  // Respond with HTML
  res.end(responseMessage);
});
app.listen(port);
console.log(`The server has started and is listening on port number: ${port}`);
```
