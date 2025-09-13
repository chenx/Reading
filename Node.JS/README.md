# NodeJS

https://www.w3schools.com/nodejs/

- Node.js uses an event-driven, non-blocking model.
- It can handle many connections at once without waiting for one to finish before starting another.
- This makes it great for real-time apps and high-traffic websites.

Here are some examples of what you can build with Node.js:

    Web servers and websites
    REST APIs
    Real-time apps (like chat)
    Command-line tools
    Working with files and databases
    IoT and hardware control

## Basics

- Node.js is a free, open-source JavaScript runtime that runs on Windows, Mac, Linux, and more.
- Built on Chrome's V8 JavaScript engine, Node.js is designed for building scalable network applications efficiently.
- Node.js uses asynchronous (non-blocking) programming.
- Node.js releases a new major version every six months.
  - For stability, use an LTS (Long Term Support) version for production projects.

### Install

Download and Install Node.js

    Go to https://nodejs.org
    Download the LTS (Long Term Support) version
    Run the installer and follow the instructions

Verify installation:

    node --version
    npm --version 

### Run node.js code

Create file server.js:
```
let http = require('http');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World!');
}).listen(8080);
```

```
node server.js
```

### npm

npm is the package manager for Node.js.

### JavaScript fundamentals

    Variables
    Functions
    Objects
    Arrays
    Asynchronous programming (callbacks, promises, async/await)
    ES6+ features

Asynchromous JavaScript

```
// 1. Callbacks (traditional)
function fetchData(callback) {
  setTimeout(() => {
    callback('Data received!');
  }, 1000);
}

// 2. Promises (ES6+)
const fetchDataPromise = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve('Promise resolved!'), 1000);
  });
};

// 3. Async/Await (ES8+)
async function getData() {
  const result = await fetchDataPromise();
  console.log(result);
}

getData(); // Call the async function
```


