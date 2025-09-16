# Deep Copy

- https://medium.com/@saikiran-dev/absolute-modern-way-to-deep-clone-object-in-javascript-61f0282db8de
- https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy
- https://developer.mozilla.org/en-US/docs/Web/API/Window/structuredClone
- https://dev.to/hkp22/javascript-shallow-copy-vs-deep-copy-examples-and-best-practices-3k0a

When to Use Shallow Copy

    Flat Objects: When dealing with simple objects without nested properties.
    Performance: When speed is crucial, and you don’t need to handle deeply nested data.
    Temporary Changes: When you intend to modify top-level properties but share nested data.

When to Use Deep Copy

    Complex Structures: For objects with multiple levels of nesting.
    Avoiding Side Effects: When you need to ensure that changes in the copy don’t affect the original.
    State Management: In frameworks like React or Redux, where immutability is critical.

### Methods

Method 1: 

const newObject = JSON.parse(JSON.stringify(oldObject));

However there are things JSON.stringify cannot stringify, so it does not always work.

Method 2:

const newObject = window.structuredClone(oldObject);

This is browser dependent. It allows the options of transferable object. It also cannot handle all cases.

Method 3:

Deep copy by recursive function. May use a library.
