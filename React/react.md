# React

https://www.w3schools.com/REACT/react_intro.asp

## Introduciton

### What is React?

- React is a front-end JavaScript library.
- React was developed by the Facebook Software Engineer Jordan Walke.
- React is also known as React.js or ReactJS.
- React is a tool for building UI components.

### How does React Work?

- React creates a VIRTUAL DOM in memory.

Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.

### React.JS History

- Latest version of React.JS is 19.0.0 (December 2024).
- Initial release to the Public (version 0.3.0) was in July 2013.
- React.JS was first used in 2011 for Facebook's Newsfeed feature. 

## Getting started: First App

Node.js

```
node -v
```

Install build tool Vite:

```
npm install -g create-vite
```

Create a React application, install dependency and run the app:
```
npm create vite@latest my-react-app -- --template react
npm install --force
npm run dev
```

index.html --> src/main.jsx --> src/App.jsx

## Render HTML

- Container: <div id="root"></div> element in the index.html
- Function: createRoot() in src/main.jsx
  - render() method

## React ES6

- ES6: ECMAScript 2015
- New features
  - Class, constructor, method, inheritance
  - Arrow function:
    - hello = () => { return 'hello'; }
    - hello = () => 'hello';
    - hello = (name) => { return 'hello ' + name; }
    - hello = name => 'hello ' + name;
    - this:
      - In regular functions the this keyword represented the object that called the function
      - With arrow functions, the this keyword always represents the object that defined the arrow function
  - Variables
    - Before: var (function scope, not block scope)
    - ES6: var, let (block scoped versino of var), const (block scope)
      - const: defines constant reference to a value, not constant value; cannot reassign,
        - but can change elements of a const array, or properties of a constant object
  - map() method on list / array
    - map(currentValue, index, array)
  - Destructuring
    - array
    - object
    - react components: props
    - useState hook 
  - Spread operator
  - Modules: import, export
    - named, or default
  - Ternary operator: ? :
  - Template strings
    - Tagged templates

## JSX intro

- JSX stands for JavaScript XML.
- JSX allows us to write HTML in React (and make it easier).
- You are not required to use JSX, but JSX makes it easier to write React applications.

## JSX Expressions

- You can insert any valid JavaScript expression inside JSX by wrapping it in curly braces { }
- Insert variables in JSX by wrapping it in curly braces { }
- Insert function calls in JSX by wrapping it in curly braces { }
- Access object properties within JSX

## JSX Attributes

## JSX If

## React Components

- Components are like functions that return HTML elements.
- 2 types, Class components and Function components
- Ccomponent's name MUST start with an upper case letter
- Props
- Components in Components
- Components in Files

## React Class Components

- Before React 16.8, Class components were the only way to track state and lifecycle on a React component. Function components were considered "state-less".
- With the addition of Hooks, Function components are now almost equivalent to Class components.
- The differences are so minor that you will probably never need to use a Class component in React.

```
class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}
```

- React Class components have a built-in state object.
  - The state object is initialized in the constructor
  - To change a value in the state object, use the this.setState() method.

### Life cycle of components: Mounting, Updating, and Unmounting

Mountinig:
- constructor()
- getDerivedStateFromProps()
- render()
- componentDidMount()

Updating:
- getDerivedStateFromProps()
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()


## React Props

