# JavaScript Inheritance

## prototype and \_\_proto\_\_

Each function / class has a prototype field.

Each instance has a \_\_proto\_\_ field pointing to the function / class prototype.

## Prototype Chain

An object looks for an attribute, if not found in current class, then looks upward 
in __proto__.__proto__. ..., until Object.prototype or where prototype is null.

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
- point p.__proto__ to Person.prototype
- execute Person and bind this
