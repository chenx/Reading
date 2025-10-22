# JavaScript Inheritance

## prototype and __proto__

Each function / class has a prototype field.

Each instance has a __proto__ field pointing to the function / class prototype.

## Prototype Chain

An object looks for an attribute, if not found in current class, then looks upward 
in __proto__.__proto__. ..., until Object.prototype or where prototype is null.

