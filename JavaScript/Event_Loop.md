# Event Loop

[Event loop in JavaScript, microtask, macrotask, Promise, and common interview questions](https://levelup.gitconnected.com/event-loop-in-javascript-microtask-macrotask-promise-and-common-interview-questions-14b7ee57be94)

[Understanding the Event Loop in JavaScript: Microtasks, Macrotasks, and Asynchronous Execution ](https://dev.to/nishanthan-k/understanding-the-event-loop-in-javascript-microtasks-macrotasks-and-asynchronous-execution-3037)

## Event Loop

Synchronous tasks (console.log())
 |
 V
Microtasks （Promise resolve, reject)
 |
 V
Macrotasks (setTimeout, setInterval)
 |
 V
(loop back)

## Mechanism

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
  
