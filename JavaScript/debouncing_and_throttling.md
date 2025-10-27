# Debouncing and Throttling (防抖与节流)

Debouncing
- Combines multiple calls into one after the user stops performing actions for a certain time.

Throttling
- Limits the execution of a function to only once in every specified time interval.


## Debounce and Throttling: What They Are and When to Use Them

[Debounce and Throttling: What They Are and When to Use Them](https://medium.com/@bs903944/debounce-and-throttling-what-they-are-and-when-to-use-them-eadd272fe0be)

**Debouncing** is a technique that **delays** the execution of a function until the **user stops** performing a certain action 
**for a specified amount of time**.

**Throttling** is a technique that **limits** the execution of a function to **once in every specified time interval**.

#### Example of Debouncing:

```
// A function that makes an API call with the search query
function searchHandler(query) {
    getSearchResults(query);
}

// A debounce function that takes a function and a delay as parameters
function debounce(func, delay) {
    let timer;

    return function(…args) {
        clearTimeout(timer);
        timer = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// A debounced version of the search handler with 500ms delay
const debouncedSearchHandler = debounce(searchHandler, 500);

// Add an event listener to the search bar input
searchBar.addEventListener("input", (event) => {
    const query = event.target.value;
    debouncedSearchHandler(query);
});
```

#### Debouncing with immediate

Lodash's debounce can do both. You'll have to specify whether it's leading or trailing.

https://lodash.com/docs#debounce

Code below is from https://learnersbucket.com/examples/interview/debounce-function-with-immediate-flag-in-javascript/

```
const debounce = (func, wait, immediate) => {
  let timeout;

  // debounce returns a new anonymous function (closure)
  return function(...args) {
    // should the function be called now? If immediate is true
    // and not already in a timeout then the answer is: Yes
    const callNow = immediate && !timeout;

    clearTimeout(timeout);

    timeout = setTimeout(function() {
      // Inside the timeout function, clear the timeout variable
      // which will let the next execution run when in 'immediate' mode
      timeout = null;

      if (!immediate) {
        func.apply(this, args);
      }
    }, wait);

    // immediate mode and no wait timer? Execute the function immediately
    if (callNow) func.apply(context, args);
  }
}
```

#### Example of Throttling:

```
// A function that updates the layout of the page
function updateLayout() {
    // Update layout logic
}

// A throttle function that takes a function and an interval as parameters
function throttle(func, interval) {
    let isRunning = false;

    return function(…args) {
        if (!isRunning) {
            isRunning = true;

            func.apply(this, args);

            setTimeout(() => {
                isRunning = false;
            }, interval);
        }
    };
}

// A throttled version of the update layout function with 100ms interval
const throttledUpdateLayout = throttle(updateLayout, 100);

// Add an event listener to the window resize event
window.addEventListener("resize", () => {
    throttledUpdateLayout();
});
```

## Demo of the 2

https://web.archive.org/web/20220117092326/http://demo.nimius.net/debounce_throttle/

