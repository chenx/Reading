# JavaScript Inheritance

## prototype and \_\_proto\_\_

Each function / class has a prototype field.

Each instance has a \_\_proto\_\_ field pointing to the function / class prototype.

## Prototype Chain

An object looks for an attribute, if not found in current class, then looks upward 
in \_\_proto\_\_.\_\_proto\_\_. ..., until Object.prototype or where prototype is null.

## What happens when a new object is created?
```
function Person(name) {
  this.name = name;
}
const p = new Person('Alice');

console.log(p.__proto__.__proto__.__proto__);  // output: null
console.log(Object.__proto__.__proto__.__proto__);  // output: null
```

What happens:
- create a new object p
- point p.\_\_proto\_\_ to Person.prototype
- execute Person and bind this

## Object.\_\_proto\_\_ and Object.prototype.\_\_proto\_\_

In JavaScript, Object.\_\_proto\_\_ and Object.prototype.\_\_proto\_\_ refer to different aspects of the prototype chain:

- Object.\_\_proto\_\_:
  - This refers to the [[Prototype]] (internal property) of the Object constructor function itself.
  - Since Object is a function, its prototype is Function.prototype. Therefore, Object.\_\_proto\_\_ evaluates to Function.prototype.
  - \_\_proto\_\_ is a deprecated accessor property that exposes the [[Prototype]] of an object. While it's widely supported, it's generally recommended to use Object.getPrototypeOf() for accessing an object's prototype. 

- Object.prototype.\_\_proto\_\_:
  - This refers to the [[Prototype]] of the Object.prototype object.
  - Object.prototype is the base object from which all other objects in JavaScript (unless specifically created with a null prototype) inherit properties and methods.
  - Object.prototype itself does not inherit from any other object, meaning its [[Prototype]] is null. Therefore, Object.prototype.\_\_proto\_\_ evaluates to null. 

In summary:
- Object.proto points to Function.prototype and Object.prototype.proto points to null.

Example:
```
console.log(Object.__proto__ === Function.prototype); // true
console.log(Object.prototype.__proto__ === null);     // true
```
