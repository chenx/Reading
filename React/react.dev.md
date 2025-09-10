# React.dev

https://react.dev/learn


## Quick Start

### Creating and nesting components

React apps are made out of *components*.

React components are JavaScript functions that return markup.

React component names must always start with a capital letter, while HTML tags must be lowercase.

```
function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

### Writing markup with JSX

If you have a lot of HTML to port to JSX, you can use an [online converter](https://transform.tools/html-to-jsx).

### Adding styles 

className

### Displaying data

{ user.name }

### Conditional rendering 

### Rendering lists

### Responding to events

### Updating the screen 

- import useState from React: import { useState } from 'react';
- declare a state variable inside your component:
```
function MyButton() {
  const [count, setCount] = useState(0);
  // ...
```
- If you render the same component multiple times, each will get its own state.
