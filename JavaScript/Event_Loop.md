# Event Loop

[1] [Event loop in JavaScript, microtask, macrotask, Promise, and common interview questions](https://levelup.gitconnected.com/event-loop-in-javascript-microtask-macrotask-promise-and-common-interview-questions-14b7ee57be94)

[2] [Understanding the Event Loop in JavaScript: Microtasks, Macrotasks, and Asynchronous Execution ](https://dev.to/nishanthan-k/understanding-the-event-loop-in-javascript-microtasks-macrotasks-and-asynchronous-execution-3037)

## Event Loop

Call stack is LIFO (stack). It takes tasks in the order of synchronous, Microtasks and Macrotasks.
Some long-running asynchronous tasks are reassigned to web APIs to run in another thread.

```
Synchronous tasks (console.log())
 |
 V
Microtasks （High priority tasks: Promise resolve, reject)
 |
 V
Macrotasks (Low priority tasks: setTimeout, setInterval, event listener, UI updates)
 |
 V
(loop back)
```

```
Call Stack  <-> Web API
|
| <---------->  Microtasks Queue
|
| <---------->  Macrotasks Queue

Event Loop
```


## Mechanism [1]

https://www.youtube.com/watch?v=eiC58R16hb8&t=733s

Basically, the mechanism works like this:

- Event Loop: A continuous loop that runs and executes everything in the Call Stack.
- Task Queue (Macrotask Queue): Holds callbacks for Macrotasks, such as setTimeout, setInterval, etc.
- Microtask Queue: Contains callbacks for Microtasks, such as Promises and MutationObservers.
- Macrotasks: Are only executed after the Call Stack is empty and the Microtask Queue is empty.
- Microtasks: Can trigger other microtasks, which can lead to the Microtask Queue never emptying, potentially causing browser stutter or even freezing. However, Macrotasks don’t have this issue, as each Macrotask is executed in one iteration of the Event Loop (similar to a loop iteration).
- You can directly push a callback into the Microtask Queue using queueMicrotask, for example:

```
queueMicrotask(() => {
    console.log(1)
})
```

Additionally, here are some things we need to know that the video didn’t cover:

- With Workers, they run on a separate thread and have their own event loop. Usually, when we talk about the Main Thread (or UI Thread), we are referring to the main thread used for handling UI. Most of our code executes on this thread, and if the Main Thread gets blocked, our web page will freeze, and Chrome will display a “Page unresponsive” error.
- Note that each thread has its own Event Loop: for example, the Main Thread has one Event Loop, and each Web Worker has its own Event Loop. When we open each browser tab, it represents a separate environment with its own Event Loop.
- All Microtasks must be completed before the browser handles event handling/rendering or before executing the next Microtask.
  

## Summary [2]

JavaScript is a single-threaded language, meaning it can handle only one task at a time in a synchronous manner. However, for tasks that take longer (like fetching data), JavaScript uses Web APIs provided by the browser to manage these tasks asynchronously, preventing the UI from being blocked.

Key components in handling these tasks are:
- Call Stack: Executes synchronous tasks in a Last-In-First-Out (LIFO) manner. If an asynchronous task is encountered, it is sent to the Web API for processing.
- Web APIs: Used to handle asynchronous tasks such as HTTP requests, timers, and DOM events, ensuring JavaScript remains non-blocking.
- Microtasks: High-priority tasks like handling Promises, executed before macrotasks when the call stack is empty.
- Macrotasks (Callback Queue): Lower-priority tasks like timers (setTimeout), event listeners, and UI updates. Executed after all microtasks have finished.
- Event Loop: The mechanism that decides the order of task execution. It continuously checks the call stack, microtask queue, and macrotask queue to manage task execution.


## Example questions

    What is the Event Loop in JavaScript, and how does it work?
    What are microtasks and macrotasks in JavaScript? How are they different?
    Explain how setTimeout and Promises are handled in the Event Loop.

