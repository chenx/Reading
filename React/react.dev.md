# React.dev

https://react.dev/learn

https://ecotrust-canada.github.io/markdown-toc/

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

- import useState from React.
- declare a state variable inside your component.
```
import { useState } from 'react';

export default function MyApp() {
  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```
- If you render the same component multiple times, each will get its own state.

### Using Hooks

- Hooks are more restrictive than other functions. You can only call Hooks at the top of your components (or other Hooks). 
- If you want to use useState in a condition or a loop, extract a new component and put it there.

### Sharing data between components

To make both MyButton components display the same count and update together, you need to move the state from the individual buttons “upwards” to the closest component containing all of them.

The information you pass down like this is called props. Now the MyApp component contains the count state and the handleClick event handler, and passes both of them down as props to each of the buttons.

Finally, change MyButton to read the props you have passed from its parent component:

```
import { useState } from 'react';

export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}

function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

### Tutorial: Tic-Tac-Toe

https://react.dev/learn/tutorial-tic-tac-toe

### Thinking in React

https://react.dev/learn/thinking-in-react

#### Start with the mockup

#### Step 1: Break the UI into a component hierarchy

#### Step 2: Build a static version in React

- It’s often easier to build the static version first and add interactivity later.
- In simpler examples, it’s usually easier to go top-down, and on larger projects, it’s easier to go bottom-up.

#### Step 3: Find the minimal but complete representation of UI state 

Props vs State

- Props are like arguments you pass to a function. They let a parent component pass data to a child component and customize its appearance. For example, a Form can pass a color prop to a Button.
- State is like a component’s memory. It lets a component keep track of some information and change it in response to interactions. For example, a Button might keep track of isHovered state.

#### Step 4: Identify where your state should live

#### Step 5: Add inverse data flow


## Installation
