# Promise

A model of Asynchromous programming. 

In JavaScript, a Promise is an object representing the eventual completion or failure of an asynchronous operation and its resulting value. It allows for more manageable and readable asynchronous code compared to traditional callback-based approaches, helping to avoid "callback hell."

### 3 states of a Promise object

- Pending: The initial state; the operation has not yet completed.
- Fulfilled (or Resolved): The operation completed successfully, and the promise has a resulting value.
- Rejected: The operation failed, and the promise has a reason for the failure (an error).

Once a promise is fulfilled or rejected, it is considered "settled" and its state becomes immutable.

### Async operation

A Promise object is a pending operation to be fulfilled.

```
const myPromise = new Promise((resolve, reject) => {
  // Simulate an asynchronous operation
  setTimeout(() => {
    const success = true; // or false for rejection
    if (success) {
      resolve("Operation successful!");
    } else {
      reject("Operation failed.");
    }
  }, 2000);
});
```

### Chained invocation

Chained invocation by .then(), .catch(), .finally()  functions.

```
myPromise
  .then((message) => {
    console.log(message); // "Operation successful!"
  })
  .catch((error) => {
    console.error(error); // "Operation failed."
  })
  .finally(() => {
    console.log("Promise settled."); // Executed regardless of outcome
  });
```

### Promise.all()

Parallel processing: Promise.all(), continue execution after all promises finish.

Promise.all() in JavaScript is a method used to handle multiple asynchronous operations, specifically Promises, concurrently. It takes an iterable (like an array) of Promises as input and returns a single Promise.
Key characteristics of Promise.all():

- Concurrency:
  - It allows multiple Promises to run in parallel, which can significantly improve performance when dealing with independent asynchronous tasks.
- Aggregation of Results:
  - When all the Promises in the input iterable successfully fulfill, the Promise.all() method returns a new Promise that resolves with an array containing the resolved values of the input Promises, in the same order as they were provided.

- Fast-Fail Behavior:
  - If any of the Promises in the input iterable reject, the Promise.all() method immediately rejects with the reason of the first rejected Promise. It does not wait for other Promises to settle.

```
const promise1 = Promise.resolve(3);
const promise2 = 42; // Non-promise values are treated as resolved promises
const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("foo");
  }, 100);
});

Promise.all([promise1, promise2, promise3])
  .then((values) => {
    console.log(values); // Output: [3, 42, "foo"]
  })
  .catch((error) => {
    console.error("One of the promises rejected:", error);
  });
```

### When to use

When to use `Promise.all()`:

- When you need to perform multiple independent asynchronous operations and wait for all of them to complete before proceeding with further logic.
- When you require all operations to succeed for the overall task to be considered successful.

Alternative:

If you need to know the outcome of every Promise in the input iterable, regardless of whether they fulfill or reject, you should use `Promise.allSettled()`. This method returns a Promise that resolves with an array of objects, each describing the outcome (fulfilled or rejected) of the corresponding input Promise.


### Where to use

Interaction with backend API. 

For example, a HTTP request by axios or fetch returns a Promise object.

# References

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all
- https://dev.to/dperrymorrow/speed-up-your-code-with-promiseall-3d4i
- https://www.w3schools.com/jsref/jsref_promise_all.asp
