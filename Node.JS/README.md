# 1. NodeJS

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

# 2. Asynchronous

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

# 3. Module Basics

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

<br/>

## Publish a Package

Publishing a package means making your Node.js module or project available for others to install and use via the npm registry.
- This is how open-source libraries and tools are shared with the Node.js community.
- When you publish a package, it becomes available for anyone to install using npm install your-package-name.

### Steps

    Preparing Your Package
    Creating an npm Account
    Publishing Your Package
    Updating Your Package
    Managing Published Packages

### Best Practices

    Follow Semantic Versioning - Use MAJOR.MINOR.PATCH version numbers appropriately
    Write Good Documentation - Include clear usage examples in your README
    Add Tests - Include unit tests and document how to run them
    Use .npmignore - Only publish necessary files
    Add Keywords - Help others discover your package
    Choose the Right License - Make your terms clear to users
    Maintain a Changelog - Document changes between versions
    Use Continuous Integration - Automate testing and publishing

<br/>

# 4. Core Modules

<br/>

# 5. JS & TS Features

## ES6+ Features

ES6 (ECMAScript 2015) and later versions add powerful new features to JavaScript that make your code more expressive, concise, and safer.

Node.js has excellent support for modern JavaScript features.

### Async/Await

Async/await (introduced in ES2017) provides a cleaner syntax for working with promises, making asynchronous code look and behave more like synchronous code.

### ES Modules

ES Modules (ESM) provide a standardized way to organize and share code. They were introduced in ES2015 and are now supported natively in Node.js.

Key benefits of ES Modules:

    Static module structure (imports are analyzed at compile time)
    Default and named exports/imports
    Better dependency management
    Tree-shaking (eliminating unused code)

### Summary

ES6+ introduced numerous features that have transformed JavaScript programming, making code more readable, maintainable, and robust:

    let/const: Block-scoped variables with clearer semantics
    Arrow functions: Concise syntax and lexical this binding
    Template literals: String interpolation and multi-line strings
    Destructuring: Extract values from objects and arrays easily
    Spread/rest operators: Work with collections more efficiently
    Default parameters: Simpler function definitions
    Classes: Cleaner syntax for object-oriented programming
    Promises and async/await: Better asynchronous code management
    ES Modules: Standardized code organization
    Enhanced object literals: More concise object syntax
    Optional chaining & nullish coalescing: Safer property access and defaults

These modern features are fully supported in current Node.js versions, allowing you to write cleaner, more expressive code while avoiding common JavaScript pitfalls.

## Process Management

Process management in Node.js is about controlling your application's lifecycle.

It includes:

    Starting and stopping applications
    Restarting after crashes
    Monitoring performance
    Handling system signals
    Managing environment variables

### Key Takeaways

    Process Object: Access system and process information
    Process Control: Start, stop, and manage application lifecycle
    Environment Variables: Configure app behavior across different environments
    Child Processes: Run system commands and other scripts
    Error Handling: Handle uncaught exceptions and rejections
    Signals: Respond to system signals like SIGINT and SIGTERM
    PM2: Essential for production process management
    Performance Monitoring: Track memory and CPU usage

## TypeScript

## Advanced TypeScript

### Key Takeaways:

    Leverage TypeScript's advanced type system for better code safety and developer experience
    Use generics to create flexible and reusable components without losing type safety
    Implement decorators for cross-cutting concerns like logging, validation, and performance monitoring
    Utilize utility types to transform and manipulate types without code duplication
    Create type-safe abstractions for Node.js-specific patterns like event emitters and streams

### Performance Considerations:

    Be mindful of complex types that might impact compilation time
    Use type over interface for complex type operations
    Consider using as const for literal types when appropriate
    Use unknown instead of any for type-safe dynamic typing

## Linting & Formatting

### ESLint: JavaScript/TypeScript Linting

ESLint is the most popular JavaScript/TypeScript linting tool that helps identify and report on patterns found in your code. It's highly configurable and supports.

```
npm install --save-dev eslint
```

### Prettier: Code Formatter

Prettier is an opinionated code formatter that enforces a consistent style by parsing your code and re-printing it with its own rules. It supports:

    JavaScript, TypeScript, JSX, CSS, SCSS, JSON, and more
    Opinionated defaults with minimal configuration
    Integration with ESLint and other tools
    Support for editor integration

Installation
```
npm install --save-dev --save-exact prettier
```

# 6. Building Applications

## Frameworks

### Types of Node.js Frameworks

#### Full-Stack Frameworks

These frameworks provide solutions for both front-end and back-end development, often with integrated templating engines, ORM systems, and more.
- Examples: Meteor, Sails.js, AdonisJS
- Use When: Building complete web applications with both frontend and backend components

#### Minimalist/Micro Frameworks

These frameworks focus on being lightweight and provide only the essential features, letting developers add what they need.
- Examples: Express.js, Koa, Fastify
- Use When: Building APIs or simple web services where you want maximum control

#### REST API Frameworks

Specialized frameworks designed for building RESTful APIs with features like automatic validation, documentation, and versioning.
- Examples: LoopBack, NestJS, Restify
- Use When: Building robust, production-ready APIs with minimal boilerplate

#### Real-Time Frameworks

Frameworks optimized for real-time applications with built-in support for WebSockets and server-sent events.
- Examples: Socket.io, Sails.js, FeathersJS
- Use When: Building chat applications, live updates, or any real-time features


### Popular Node.js Frameworks

Framework Selection Criteria

When choosing a framework, consider these factors:

    Project Requirements: Does the framework support your specific needs?
    Learning Curve: How quickly can your team become productive?
    Performance: Does it meet your performance requirements?
    Community & Support: Is there active development and community support?
    Ecosystem: Are there plugins and middleware available?

#### Express.js

Express is the most popular and widely used Node.js framework, known for its simplicity and flexibility.

#### Nest.js

Nest.js is a progressive framework inspired by Angular, built with TypeScript, and designed for building efficient, scalable server-side applications.

#### Fastify
#### Koa.js
#### Hapi.js
#### Adonis.js
#### Socket.io
#### Meteor
### Loopback

### API-Focused Frameworks

These frameworks are designed specifically for building APIs and RESTful web services.

#### Restify
#### Strapi

#### Choosing the Right Framework

<br/>

## Express.js

https://www.w3schools.com/nodejs/nodejs_express.asp

## Middleware

Middleware is a key part of Node.js web applications, particularly in Express.js.

It provides a way to add and reuse common functionality across your application's routes and endpoints.

Key Characteristics of Middleware:

    Executes during the request-response cycle
    Can modify request and response objects
    Can end the request-response cycle
    Can call the next middleware in the stack
    Can be application-level, router-level, or route-specific

It acts as a bridge between the raw request and the final intended route handler.

At its core, middleware is a function that has access to:

    The request object (req)
    The response object (res)
    The next middleware function in the application's request-response cycle

Middleware functions can perform a variety of tasks:

    Execute any code
    Modify request and response objects
    End the request-response cycle
    Call the next middleware function in the stack

### Comprehensive Guide to Middleware Types

1. Application-level Middleware

2. Router-level Middleware

3. Error-handling Middleware

#### Built-in Middleware

#### Third-party Middleware

#### Creating and Using Custom Middleware

#### Error-Handling Middlewar

#### Middleware Execution Order

##
# Best Practices

1. Keep Middleware Focused

2. Use Next() Properly

    Always call next() unless you're ending the response
    Never call next() after sending a response
    Call next() with an error parameter to trigger error handling

3. Handle Async Code Properly

Always catch errors in async middleware and pass them to next().

4. Don't Overuse Middleware

Too many middleware functions can impact performance. Use them judiciously.

5. Organize by Domain

Group related middleware in separate files based on functionality.

6. Use Conditional Next()

Middleware can decide whether to continue the chain based on conditions.

<br/>

## RESTful API

REST (Representational State Transfer) is an architectural style for designing networked applications that has become the standard for web services.

RESTful APIs provide a flexible, lightweight way to integrate applications and enable communication between different systems.

Core Concepts:

    Resources: Everything is a resource (user, product, order)
    Representations: Resources can have multiple representations (JSON, XML, etc.)
    Stateless: Each request contains all necessary information
    Uniform Interface: Consistent way to access and manipulate resources

RESTful APIs use HTTP requests to perform CRUD operations (Create, Read, Update, Delete) on resources, which are represented as URLs.

REST is stateless, meaning each request from a client to a server must contain all the information needed to understand and process the request.

### Core REST Principles

Key Principles in Practice:

    Resource-Based: Focus on resources rather than actions
    Stateless: Each request is independent and self-contained
    Cacheable: Responses define their cacheability
    Uniform Interface: Consistent resource identification and manipulation
    Layered System: Client doesn't need to know about the underlying architecture

The core principles of REST architecture include:

    Client-Server Architecture: Separation of concerns between the client and the server
    Statelessness: No client context is stored on the server between requests
    Cacheability: Responses must define themselves as cacheable or non-cacheable
    Layered System: A client cannot tell whether it is connected directly to the end server
    Uniform Interface: Resources are identified in requests, resources are manipulated through representations, self-descriptive messages, and HATEOAS (Hypertext As The Engine Of Application State)

### HTTP Methods and Their Usage

### RESTful API Structure and Design

### Building REST APIs with Node.js and Express

### Best Practices Summary

    Follow REST principles and use appropriate HTTP methods
    Use consistent naming conventions for endpoints
    Structure your API logically with resource-based URLs
    Return appropriate status codes in responses
    Implement proper error handling with clear messages
    Use pagination for large data sets
    Version your API to maintain backward compatibility
    Validate all input to prevent security issues
    Document your API thoroughly
    Write comprehensive tests to ensure reliability
    Use HTTPS for all production APIs
    Implement rate limiting to prevent abuse

<br/>

## API Authentication Guide

### Authentication Methods

- 1. Session-Based Authentication
  - Session-based authentication uses cookies to maintain user state.
- 2. Token-Based Authentication (JWT)
  - JSON Web Tokens (JWT) provide a stateless authentication mechanism that's compact and self-contained.
  - Unlike session-based authentication, token-based authentication (JWT) doesn't require a server to store session data.
  - This makes it ideal for stateless API architecture and microservices.
- 3. OAuth 2.0 Authentication
  - OAuth 2.0 is the industry-standard protocol for authorization, enabling applications to obtain limited access to user accounts on HTTP services.
  - It works by delegating user authentication to the service that hosts the user account.
- 4. API Key Authentication
 

### Basic Authentication

HTTP Basic authentication uses encoded credentials in the Authorization header.

### Multi-Factor Authentication (MFA)

Adding an extra layer of security with time-based one-time passwords (TOTP).

### Security Best Practices

When implementing API authentication, follow these security best practices:

    HTTPS Only: Always use HTTPS to encrypt data in transit
    Password Hashing: Store only hashed passwords using bcrypt or Argon2
    Token Management: Keep tokens short-lived and implement refresh tokens
    Rate Limiting: Protect against brute force attacks
    Input Validation: Validate all user inputs to prevent injection attacks
    CORS Configuration: Restrict cross-origin requests appropriately
    Secure Headers: Implement security headers like HSTS and CSP
    Audit Logging: Log authentication events for security monitoring

<br/>

## Node.js with Frontend Frameworks

Node.js provides a backend foundation that integrates with modern JavaScript frontend frameworks, enabling developers to build full-stack applications within just the JavaScript ecosystem.

This approach offers several advantages:

    Unified Language: Use JavaScript/TypeScript across the entire stack
    Code Sharing: Share validation, types, and utilities between frontend and backend
    Developer Experience: Consistent tooling and package management with npm/yarn
    Performance: Efficient data transfer with JSON and modern protocols
    Ecosystem: Access to a vast collection of packages for both frontend and backend

### Common Integration Patterns

1. API-First Architecture

2. Server-Side Rendering (SSR)

3. Micro-Frontends

### Node.js with React

Why Use React with Node.js?

    Component-Based Architecture: Build encapsulated components that manage their own state
    Virtual DOM: Efficient updates and rendering
    Rich Ecosystem: Large community and extensive package ecosystem
    Developer Tools: Excellent debugging and development tools

#### Setting Up a React App with Node.js Backend

1. Create React App (Frontend)
```
npx create-react-app my-app
cd my-app
npm start
```

2. Set Up Node.js Backend
```
mkdir backend
cd backend
npm init -y
npm install express cors
```

### Node.js with Angular

Angular is a comprehensive platform and framework for building scalable single-page applications using TypeScript.

It provides a complete solution with built-in features for routing, forms, HTTP client, and more, making it a robust choice for enterprise applications.

#### Key Features of Angular with Node.js

    TypeScript Support: Built with TypeScript for better tooling and type safety
    Dependency Injection: Built-in DI system for better component organization
    Modular Architecture: Organized into modules, components, and services
    RxJS Integration: Powerful reactive programming with Observables
    Angular CLI: Command-line interface for project generation and build tools

#### Setting Up Angular with Node.js Backend

1. Install Angular CLI
```
npm install -g @angular/cli
```

2. Create New Angular Project
```
ng new angular-nodejs-app
cd angular-nodejs-app
```

### Node.js with Vue.js

Vue.js is a progressive, approachable, and performant JavaScript framework for building user interfaces.

It provides a gentle learning curve and flexible architecture, making it an excellent choice for both small projects and large-scale applications when combined with Node.js backends.

#### Why Choose Vue.js with Node.js?

    Progressive Framework: Scales from a library to a full-featured framework
    Reactive Data Binding: Simple and intuitive two-way data binding
    Component-Based: Build encapsulated, reusable components
    Vue CLI: Powerful command-line interface for project scaffolding
    Vuex: Centralized state management for complex applications

#### Setting Up Vue.js with Node.js Backend

1. Install Vue CLI
```
npm install -g @vue/cli
```

2. Create New Vue Project
```
vue create vue-nodejs-app
cd vue-nodejs-app
```

### Node.js with Svelte

Svelte is a revolutionary approach to building user interfaces that compiles your code to highly efficient vanilla JavaScript at build time, rather than interpreting your application code at runtime.

This results in smaller bundle sizes and better performance compared to traditional frameworks.

#### Why Choose Svelte with Node.js?

    No Virtual DOM: Compiles to vanilla JavaScript for better performance
    Smaller Bundle Size: No framework runtime to ship to the browser
    Simpler Code: Less boilerplate than traditional frameworks
    Reactive by Default: Automatic updates without complex state management
    Scoped CSS: Component-scoped styles without CSS-in-JS

### Best Practices for Node.js with Frontend Frameworks

<br/>

# 7. Database Integration

## MySQL

## MongoDB

One of the most popular NoSQL database is MongoDB.

### MongoDB

To be able to experiment with the code examples, you will need access to a MongoDB database.
- You can download a free MongoDB database at https://www.mongodb.com.
- Or get started right away with a MongoDB cloud service at https://www.mongodb.com/cloud/atlas.

```
npm install mongodb
```

A collection in MongoDB is the same as a table in MySQL
- Important: In MongoDB, a collection is not created until it gets content!
- MongoDB waits until you have inserted a document before it actually creates the collection.

<br/>

# 8. Advanced Communication

## GraphQL

https://www.w3schools.com/nodejs/nodejs_graphql.asp

GraphQL is a query language for APIs and a runtime for executing those queries against your data. It was developed by Facebook in 2012 and publicly released in 2015.

### Key Features

    Client-specified queries: Request exactly what you need, nothing more
    Single endpoint: Access all resources through one endpoint
    Strongly typed: Clear schema defines available data and operations
    Hierarchical: Queries match the shape of your data
    Self-documenting: Schema serves as documentation

### Getting Started with GraphQL in Node.js

```
npm install express express-graphql graphql
```

## Socket.IO

Socket.IO is a powerful JavaScript library that enables real-time, bidirectional, and event-based communication between web clients and servers. It's designed to work on every platform, browser, or device, focusing equally on reliability and speed.

## WebSockets

WebSockets provide a persistent connection between client and server, allowing for real-time, bidirectional communication.

This is different from traditional HTTP, which follows a request-response model.
Key Benefits of WebSockets

    Real-time updates: Instantly push data to clients
    Efficient: No need for repeated HTTP requests
    Bidirectional: Both client and server can send messages
    Low latency: Messages are sent immediately

<br/>

## Socket.IO vs Websockets

WebSocket is a communication protocol that provides full-duplex, persistent communication channels over a single TCP connection. It is a standardized protocol enabling real-time, bidirectional communication between a client and a server, making it suitable for applications requiring low-latency data exchange.

Socket.IO is a JavaScript library that builds on top of WebSockets, providing a layer of abstraction and additional features. While it utilizes WebSockets as its primary transport mechanism when available, it also includes fallback options like HTTP long-polling for environments where WebSockets are not supported or blocked.

### Key Differences:

#### Protocol vs. Library:
    WebSocket is a low-level communication protocol, while Socket.IO is a higher-level library that utilizes and extends WebSocket functionality.

#### Features:

    Socket.IO offers numerous features out-of-the-box that are not inherent in plain WebSockets, including:

        Automatic Reconnection: Handles connection drops and attempts to re-establish the connection.
        Event-based Communication: Simplifies message handling by allowing custom events to be emitted and listened for.
        
        Fallbacks: Provides alternative transport mechanisms (like long-polling) when WebSockets are unavailable.
        Rooms and Namespaces: Facilitates organizing and targeting specific groups of clients for message broadcasting. 

    Overhead:
    
    Socket.IO introduces some overhead due to its additional features and proprietary framing, which can slightly increase message size and latency compared to raw WebSockets in highly performance-sensitive scenarios.

    Compatibility:
    
    WebSocket is a standard protocol supported across various platforms and programming languages. Socket.IO primarily targets JavaScript/Node.js environments, although community-supported implementations exist for other languages.

#### When to choose which:

Choose WebSocket:

For scenarios requiring maximum performance, minimal overhead, and fine-grained control over the communication, such as high-frequency trading or highly optimized real-time games, especially when operating outside of a JavaScript/Node.js ecosystem.

Choose Socket.IO:

For building scalable and resilient real-time web applications with features like chat, collaborative tools, or dashboards, particularly within a JavaScript/Node.js environment, where the convenience and built-in features outweigh the slight performance overhead.

