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
    // Make an API call with search query
    getSearchResults(query);
}
// A debounce function that takes a function and a delay as parameters
function debounce(func, delay) {
    // A timer variable to track the delay period
    let timer;
    // Return a function that takes arguments
    return function(…args) {
        // Clear the previous timer if any
        clearTimeout(timer);
        // Set a new timer that will execute the function after the delay period
        timer = setTimeout(() => {
            // Apply the function with arguments
            func.apply(this, args);
        }, delay);
    };
}
// A debounced version of the search handler with 500ms delay
const debouncedSearchHandler = debounce(searchHandler, 500);
// Add an event listener to the search bar input
searchBar.addEventListener("input", (event) => {
    // Get the value of the input
    const query = event.target.value;
    // Call the debounced search handler with the query
    debouncedSearchHandler(query);
});
```

#### Example of Throttling:

```
// A function that updates the layout of the page
function updateLayout() {
    // Update layout logic
}
// A throttle function that takes a function and an interval as parameters
function throttle(func, interval) {
    // A flag variable to track whether the function is running or not
    let isRunning = false;
    // Return a function that takes arguments
    return function(…args) {
        // If the function is not running
        if (!isRunning) {
            // Set the flag to true
            isRunning = true;
            // Apply the function with arguments
            func.apply(this, args);
            // Set a timer that will reset the flag after the interval
            setTimeout(() => {
                // Set the flag to false
                isRunning = false;
            }, interval);
        }
    };
}
// A throttled version of the update layout function with 100ms interval
const throttledUpdateLayout = throttle(updateLayout, 100);
// Add an event listener to the window resize event
window.addEventListener("resize", () => {
    // Call the throttled update layout function
    throttledUpdateLayout();
});
```

## Demo of the 2

https://web.archive.org/web/20220117092326/http://demo.nimius.net/debounce_throttle/

