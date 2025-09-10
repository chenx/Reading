# React.dev

https://react.dev/learn

https://ecotrust-canada.github.io/markdown-toc/

## 1. Quick Start

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

<br />

## 2. Installation

### Creating a React App

#### Full-stack frameworks

Next.js (App Router)

- Next.js’s App Router is a React framework that takes full advantage of React’s architecture to enable full-stack React apps.
- Next.js is maintained by Vercel.

```
npx create-next-app@latest
```

#### React Router (v7)

React Router is the most popular routing library for React and can be paired with Vite to create a full-stack React framework.

```
npx create-react-router@latest
```

#### Expo (for native apps)

- Expo is a React framework that lets you create universal Android, iOS, and web apps with truly native UIs.
- It provides an SDK for React Native that makes the native parts easier to use.

```
npx create-expo-app@latest
```

#### Start From Scratch

<br/>
### Build a React app from Scratch

https://react.dev/learn/build-a-react-app-from-scratch

#### Step 1: Install a build tool 

The first step is to install a build tool like vite, parcel, or rsbuild.

#### Step 2: Build Common Application Patterns

routing, data fetching, or styling

If you’re fetching data from most backends or REST-style APIs, we suggest using:
- React Query
- SWR
- RTK Query

If you’re fetching data from a GraphQL API, we suggest using:
- Apollo
- Relay

#### Code-splitting 

#### Improving Application Performance

Since the build tool you select only supports single page apps (SPAs), you’ll need to implement other rendering patterns like server-side rendering (SSR), static site generation (SSG), and/or React Server Components (RSC). 

<br/>
### Add React to an Existing Project

#### Using React for an entire subroute of your existing website

#### Using React for a part of your existing page

- Step 1: Set up a modular JavaScript environment 
- Step 2: Render React components anywhere on the page

#### Using React Native in an existing native mobile app

<br/>
## Setup 

### Editor Setup

- VS Code
- WebStorm
- Sublime Text
- Vim

Recommended text editor features
- Linting
- Formatting

### Using TypeScript

https://react.dev/learn/typescript

TypeScript supports JSX and you can get full React Web support by adding @types/react and @types/react-dom to your project.

```
npm install —save-dev @types/react @types/react-dom
```

#### TypeScript with React Components

Every file containing JSX must use the .tsx file extension. This is a TypeScript-specific extension that tells TypeScript that this file contains JSX.

#### Example Hooks

- useState
  - Re-use the value passed in as the initial state to determine what the type of the value should be.
- useReducer
  - A more complex Hook that takes a reducer function and an initial state.
  - The types for the reducer function are inferred from the initial state.
- useContext
  - A technique for passing data down the component tree without having to pass props through components.
  - It is used by creating a provider component and often by creating a Hook to consume the value in a child component.
- useMemo
  - Create/re-access a memorized value from a function call, re-running the function only when dependencies passed as the 2nd parameter are changed.
- useCallback
  - Provide a stable reference to a function as long as the dependencies passed into the second parameter are the same.

#### Useful types:

React’s folder in DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react/index.d.ts)

#### DOM Events

#### Style Props

<br/>
### React Developer Tools

#### Browser extension

React Developer Tools browser extension

#### Mobile (React Native)


<br/>
## React Compiler

### Introduction

React Compiler automatically optimizes your React application at build time. 

#### Installation

#### Incremental Adoption

#### Debugging and Troubleshooting

