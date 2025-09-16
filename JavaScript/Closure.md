# Closure

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
- https://www.w3schools.com/js/js_function_closures.asp

A **closure** is the combination of a function bundled together (enclosed) with references to its surrounding state 
(the **lexical environment**). In other words, a closure gives a function access to its outer scope.

Closures are useful because they let you associate data (the lexical environment) with a function that operates on that data.

## Lexical scoping

The word lexical refers to the fact that lexical scoping uses the location where a variable is declared
within the source code to determine where that variable is available. Nested functions have access to 
variables declared in their outer scope.

Example:
```
function init() {
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() {
    // displayName() is the inner function, that forms a closure
    console.log(name); // use variable declared in the parent function
  }
  displayName();
}
init();
```

### Scoping with let and const

Traditionally (before ES6), JavaScript variables only had two kinds of scopes: function scope and global scope.

In ES6, JavaScript introduced the let and const declarations, which, allow you to create block-scoped variables.

## Closure

```
function makeFunc() {
  const name = "Mozilla";
  function displayName() {
    console.log(name);
  }
  return displayName;
}

const myFunc = makeFunc();
myFunc();
```

Functions in JavaScript form closures. A closure is the combination of a function and the lexical environment
within which that function was declared. 

### Practical closures

Closures are useful because they let you associate data (the lexical environment) with a function that operates on that data.
This has obvious parallels to object-oriented programming, where objects allow you to associate data
(the object's properties) with one or more methods.

Consequently, you can use a closure anywhere that you might normally use an object with only a single method.

