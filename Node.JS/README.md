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

### Asynchromous JavaScript

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

### Node.JS vs Browser

Node.js and browsers both run JavaScript, but they have different environments and capabilities.

Node.js is designed for server-side development, while browsers are for client-side applications.

    APIs: Node.js provides APIs for file system, networking, and OS, which browsers do not.
    Browsers provide DOM, fetch, and UI APIs not available in Node.js.
    Global Objects: Node.js uses global; browsers use window or self.
    Modules: Node.js uses CommonJS (require) and ES modules (import); browsers use ES modules or plain <script> tags.
    Security: Browsers run in a sandbox with limited access; Node.js has full access to the file system and network.
    Event Loop: Both environments use an event loop, but Node.js has additional APIs for timers, process, etc.
    Environment Variables: Node.js can access environment variables (process.env); browsers cannot.
    Package Management: Node.js uses npm/yarn; browsers use CDNs or bundlers.

### Node Command Line

```
# Run a JavaScript file
node app.js

# Run with additional arguments
node app.js arg1 arg2

# Run in watch mode (restarts on file changes)
node --watch app.js 
```

#### Using REPL

Node.js REPL (Read-Eval-Print Loop) is an interactive shell for executing JavaScript code.

```
node
```

#### Command Line Arguments

Access command line arguments using process.argv

#### Env variables

```
// env.js
console.log('Environment:', process.env.NODE_ENV || 'development');
console.log('Custom variable:', process.env.MY_VARIABLE);
console.log('Database URL:', process.env.DATABASE_URL || 'Not set');

// Example usage with environment variables:
// NODE_ENV=production MY_VARIABLE=test node env.js
```

Debugging

```
# Start with inspector (listens on default port 9229)
node --inspect app.js

# Break on first line of application
node --inspect-brk app.js

# Specify a custom port
node --inspect=9222 app.js

# Enable remote debugging (be careful with this in production)
node --inspect=0.0.0.0:9229 app.js
```

Or Using Chrome DevTools for Debugging.

#### Common CLI Tools
#### Common Command Line Flags

### Node.js V8 Engine

V8 provides the core JavaScript execution environment that Node.js is built upon.

It allows Node.js to:

    Execute JavaScript code outside the browser
    Access operating system functionality (file system, networking, etc.)
    Use the same JavaScript engine that powers Chrome for consistency

V8 implements the ECMAScript and WebAssembly standards.

### Node.js Architecture

Node.js uses a single-threaded, event-driven architecture that is designed to handle many connections at once, efficiently and without blocking the main thread.

This makes Node.js ideal for building scalable network applications, real-time apps, and APIs.

```
1. Client Request Phase

    Clients send requests to the Node.js server
    Each request is added to the Event Queue

2. Event Loop Phase

    The Event Loop continuously checks the Event Queue
    Picks up requests one by one in a loop

3. Request Processing

    Simple (non-blocking) tasks are handled immediately by the main thread
    Complex/blocking tasks are offloaded to the Thread Pool

4. Response Phase

    When blocking tasks complete, their callbacks are placed in the Callback Queue
    Event Loop processes callbacks and sends responses
```

Node.js is particularly well-suited for:

    I/O-bound applications - File operations, database queries, network requests
    Real-time applications - Chat apps, live notifications, collaboration tools
    APIs - RESTful services, GraphQL APIs
    Microservices - Small, independent services

### Node.js Event Loop

The event loop is what makes Node.js non-blocking and efficient.

It handles asynchronous operations by delegating tasks to the system and processing their results through callbacks, allowing Node.js to manage thousands of concurrent connections with a single thread.

Node.js follows these steps to handle operations:

    Execute the main script (synchronous code)
    Process any microtasks (Promises, process.nextTick)
    Execute timers (setTimeout, setInterval)
    Run I/O callbacks (file system, network operations)
    Process setImmediate callbacks
    Handle close events (like socket.on('close'))

#### Event Loop Phases

The event loop processes different types of callbacks in this order:

    Timers: setTimeout, setInterval
    I/O Callbacks: Completed I/O operations
    Poll: Retrieve new I/O events
    Check: setImmediate callbacks
    Close: Cleanup callbacks (like socket.on('close'))

<br/>

# Asynchronous

## Async

Key Takeaways

    ✅ Use async/await for better readability
    ✅ Always handle errors with try/catch
    ✅ Run independent operations in parallel with Promise.all
    ❌ Avoid mixing sync and async code patterns
    ❌ Don't forget to await promises


## Promises

Promise States

    Pending: Initial state, operation not completed
    Fulfilled: Operation completed successfully
    Rejected: Operation failed

Once a promise is settled (either fulfilled or rejected), its state cannot change.

### Basics
```
// Create a new Promise
const myPromise = new Promise((resolve, reject) => {
  // Simulate an async operation (e.g., API call, file read)
  setTimeout(() => {
    const success = Math.random() > 0.5;
    
    if (success) {
      resolve('Operation completed successfully');
    } else {
      reject(new Error('Operation failed'));
    }
  }, 1000); // Simulate delay
});

// Using the Promise
myPromise
  .then(result => console.log('Success:', result))
  .catch(error => console.error('Error:', error.message));
```

### Use Promise.all([]):
```
const fs = require('fs').promises;
const promise1 = Promise.resolve('First result');
const promise2 = new Promise((resolve) => setTimeout(() => resolve('Second result'), 1000));
const promise3 = fs.readFile('myfile.txt', 'utf8'); // Read local file instead of fetch

Promise.all([promise1, promise2, promise3])
  .then(results => {
    console.log('Results:', results);
    // results[0] is from promise1
    // results[1] is from promise2
    // results[2] is the content of myfile.txt
  })
  .catch(error => {
    console.error('Error in one of the promises:', error);
  });
```

### Promise Chaining

### Promise Methods

Instance Methods

    then(onFulfilled, onRejected) : Handles fulfillment or rejection
    catch(onRejected) : Handles rejections
    finally(onFinally) : Runs after promise settles

Static Methods

    Promise.all(iterable) : Waits for all promises to resolve. It fails fast if any promise rejects.
    Promise.race(iterable) : Waits for first promise to settle, whether it's fulfilled or rejected.
    Promise.allSettled(iterable) : Waits for all to settle

Utility Methods

    Promise.resolve(value) : Creates a resolved promise
    Promise.reject(reason) : Creates a rejected promise

### Error Handling in Promises

## Async/Await

Async/await is a modern way to handle asynchronous operations in Node.js, building on top of Promises to create even more readable code.
- Introduced in Node.js 7.6 and standardized in ES2017.
- Async/await is basically Promises with a more readable syntax. This makes your code cleaner and more maintainable.

### Syntax
- async: Used to declare an asynchronous function that returns a Promise
- await: Used to pause execution until a Promise is resolved, can only be used inside async functions

### Example:
```
const fs = require('fs').promises;

async function readFile() {
  try {
    const data = await fs.readFile('myfile.txt', 'utf8');
    console.log(data);
  } catch (error) {
    console.error('Error reading file:', error);
  }
}

readFile();
```

<br/>

### Error Handling with Try/Catch

### Running Promises in Parallel. Use Promise.All([])

### Async/Await vs Promises vs Callbacks

### Best Practices

- Remember that async functions always return Promises
- Use Promise.all for concurrent operations
- Always handle errors
- Avoid mixing async/await with callbacks
- Create clean async functions

## Error Handling

### Basic Error Handling

#### Error-First Callbacks

### Modern Error Handling

Using try...catch with Async/Await

### Global Error Handling

Uncaught Exceptions

### Error Handling Best Practices

Dos and Don'ts

Do

    Handle errors at the appropriate level
    Log errors with sufficient context
    Use custom error types for different scenarios
    Clean up resources in finally blocks
    Validate input to catch errors early

Don't

    Ignore errors (empty catch blocks)
    Expose sensitive error details to clients
    Use try/catch for flow control
    Swallow errors without logging them
    Continue execution after unrecoverable errors

<br/>

# Module Basics

## What is a Module in Node.js?

Modules are the building blocks of Node.js applications, allowing you to organize code into logical, reusable components. They help in:

    Organizing code into manageable files
    Encapsulating functionality
    Preventing global namespace pollution
    Improving code maintainability and reusability

Node.js supports two module systems: CommonJS (traditional) and ES Modules (ECMAScript modules).

### Creating and Exporting Modules

In Node.js, any file with a .js extension is a module. You can export functionality from a module in several ways:

1. Exporting Multiple Items

Add properties to the exports object for multiple exports:

```
// Method 1: Exporting multiple items
exports.getCurrentDate = getCurrentDate;
exports.formatCurrency = formatCurrency;

// Method 2: Exporting an object with multiple properties
// module.exports = { getCurrentDate, formatCurrency };
```

2. Exporting a Single Item

To export a single item (function, object, etc.), assign it to module.exports:

```
// Exporting a single class
module.exports = Logger;
```

3. Using Your Modules

Import and use your custom modules using require() with a relative or absolute path.

### Module Loading and Caching

Node.js caches modules after the first time they are loaded. This means that subsequent require() calls return the cached version.

### Best Practices

Module Organization

    Keep modules focused on a single responsibility
    Use meaningful file and directory names
    Group related functionality together
    Use index.js for module entry points

Export Patterns

    Prefer named exports for utilities
    Use default exports for single-class modules
    Document your module's API
    Handle module initialization if needed

### Summary

Key takeaways:

    Node.js uses CommonJS modules by default
    Use require() to import and module.exports to export
    Modules are cached after first load
    Follow best practices for module organization and structu

<br/>

## ES Modules

https://www.w3schools.com/nodejs/nodejs_modules_esm.asp

### Introduction to ES Modules

- ES Modules (ESM) is the official standard format for packaging JavaScript code for reuse.
- It was introduced in ES6 (ES2015) and is now supported in Node.js.
- Prior to ES Modules, Node.js exclusively used the CommonJS module format (require/exports).
- Now developers can choose between CommonJS and ES Modules based on their project needs.

### CommonJS vs ES Modules

Here's how CommonJS and ES Modules differ:
```
Feature 	            CommonJS 	                ES Modules
------------------------------------------------------------------------------------
File Extension 	        .js (default) 	            .mjs (or .js with proper config)
Import Syntax 	        require() 	                import
Export Syntax 	        module.exports / exports 	export / export default
Import Timing 	        Dynamic (runtime) 	        Static (parsed before execution)
Top-level Await 	    Not supported 	            Supported
File URL in Imports 	Not required 	            Required for local files
```

## NPM

NPM is a package manager for Node.js packages, or modules if you like.
- www.npmjs.com hosts thousands of free packages to download and use.
- The NPM program is installed on your computer when you install Node.js

### Using a package
```
let http = require('http');
let uc = require('upper-case');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.write(uc.upperCase("Hello World!"));
  res.end();
}).listen(8080); 
```

### Global Packages

Packages can be installed globally, making them available as command-line tools anywhere on your system.

Global packages are typically used for CLI tools and utilities.

### Updating Packages

To keep your packages up to date, you can update them using the following commands:

```
npm update package-name
npm update   // Update all packages
npm outdated // Check for outdated packages
```

### Uninstalling a Package

```
npm uninstall package-name
npm uninstall -g package-name  // Remove a global package
npm uninstall --save package-name  // Remove a package and its dependencies
```

### package.json

package.json is a special file that describes your Node.js project.
- It contains information about your app, such as its name, version, dependencies, scripts, and more.
- This file is essential for managing and sharing Node.js projects, especially when using npm (Node Package Manager).

#### Create package.json
```
npm init     // interactive
npm init -y  // with default values
```

#### Example
```
{
  "name": "my-node-app",
  "version": "1.0.0",
  "description": "A simple Node.js app",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "Your Name",
  "license": "ISC"
}
```

#### Adding Dependencies

When you install a package with npm, it is added to the dependencies section of package.json.

### Working with package.json

#### Adding Dependencies
```
# Install and save to dependencies
npm install package-name

# Install and save to devDependencies
npm install --save-dev package-name

# Install exact version
npm install package-name@1.2.3
```

#### Updating Dependencies
```
# Update a specific package
npm update package-name

# Update all packages
npm update

# Check for outdated packages
npm outdated
```

#### Running Scripts
```
# Run a script
npm run script-name

# Run start script (can be called with just 'npm start')
npm start

# Run test script (can be called with just 'npm test')
npm test
```

### Best Practices

    Always specify exact versions in dependencies for production apps
    Use npm ci in CI/CD pipelines for reproducible builds
    Keep your package-lock.json file in version control
    Use .npmignore to exclude unnecessary files from published packages
    Regularly update dependencies to get security patches

<br/>

### NPM Scripts

NPM scripts are commands you define in your package.json file to automate tasks like:

    Running your app
    Testing
    Building
    Cleaning up files

#### Defining Scripts in package.json

Inside package.json, the scripts section lets you name and define commands:
```
{
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Running tests...\" && exit 0",
    "dev": "nodemon index.js"
  }
}
```

#### Common Uses for NPM Scripts

    Start your app
    Run tests
    Use tools like nodemon or webpack
    Build or bundle your code
    Lint or format your code

<br/>

### Managing Dependencies

The key components of Node.js dependency management include:

    The package.json file for declaring dependencies
    Lock files (package-lock.json or yarn.lock) for dependency versioning
    Package manager commands to install, update, and remove packages
    Security tools to identify and fix vulnerabilities

#### Understanding Semantic Versioning

Node.js packages follow semantic versioning (SemVer), using a three-part version number: MAJOR.MINOR.PATCH

    MAJOR: Incremented for incompatible API changes
    MINOR: Incremented for backward-compatible new features
    PATCH: Incremented for backward-compatible bug fixes

#### Installing Dependencies

There are several ways to install dependencies in a Node.js project.

#### Types of Dependencies

Node.js projects can have several types of dependencies, each serving a different purpose:

##### Regular Dependencies
##### Development Dependencies
##### Peer Dependencies
##### Optional Dependencies

#### Package Lock Files

Lock files ensure consistent installations across different environments by recording the exact version of each package and its dependencies.

package-lock.json (npm)
- This file is automatically generated when npm modifies the node_modules tree or package.json.

#### Updating Dependencies

### Security and Auditing

Audit Your Dependencies
- npm audit
- npm audit fix
- npm audit fix --force

### Best Practices

    Use exact versions in production: Pin your dependencies to exact versions to prevent unexpected updates.
    Regularly update dependencies: Keep your dependencies up to date to benefit from security patches and new features.
    Audit your dependencies: Regularly check for known vulnerabilities in your dependencies.
    Use a lock file: Always commit your lock file to version control.
    Minimize dependencies: Only include packages that you actually need.
    Use scoped packages: For internal packages, use scopes to avoid naming conflicts.
    Document your dependencies: Include information about why each dependency is needed in your project's documentation.

### Troubleshooting Common Issues
Clearing the npm Cache
- npm cache clean --force

Deleting node_modules and Reinstalling
- rm -rf node_modules
- rm package-lock.json
- npm install

Checking for Peer Dependency Issues
- npm ls

Fixing Broken Dependencies
- npm rebuild

