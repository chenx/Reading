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


## React Props (Properties)

- Props are arguments passed into React components.
- Props are passed to components via HTML attributes.

- multiple props
- types
- Object props
- Array props


## Props Destructuring


## Props Children


## React Events

- React has the same events as HTML: click, change, mouseover etc.
- Event handlers have access to the React event that triggered the function.


## React Conditionals


## React Lists


## React Forms

- HTML Forms vs. React Forms
  - In standard HTML, form elements maintain their own value based on user input.
  - In React, the value of the form element is kept in the component's state property and updated only with the setState() function.
- Controlled Components
  - In a controlled component, form data is handled by the React component.
  - When the data is handled by the components, all the data is stored in the component state.
  - We can use the useState Hook to keep track of each input value and provide a "single source of truth" for the entire application.


## React Forms Submit


## React Textarea


## React Select


## React multiple inputs


## React Checkbox


## React Radio


## React Portals

- A Portal is a React method that is included in the react-dom package.
- It is used to render HTML outside the parent component's DOM hierarchy.
- Using the createPortal method

```
import { createPortal } from 'react-dom';

function myChild() {
  return createPortal(
    <div>
      Welcome
    </div>,
    document.body
  );
}
```

Syntax:
```
import { createPortal } from 'react-dom';

// children: any renderable React content, like elements, strings, or fragments.
// domNode:  a DOM element where the portal should be inserted instead.
createPortal(children, domNode)
```

Portals are particularly useful for:
- Modals and dialogs
- Tooltips
- Floating menus
- Notifications


E.g., Creating a Modal with Portal
- Event Bubbling in Portals
  - Even though a portal renders content in a different part of the DOM tree, events from the portal content still bubble up through the React component tree as if the portal wasn't there.

 
## React Suspense

- React Suspense lets you display an alternative HTML while waiting for code or data to load.
  - If a component takes time to load, you can use a Suspense component, and it will display the fallback content while the component is loading.
- The alternative HTML can be a component, text, or any valid content.
- The most common use cases are:
  - Data fetching with suspense-enabled frameworks
  - Loading components dynamically with React.lazy()
    - E.g.: const Cars = lazy(() => import('./Cars'));
- One Suspense component can wrap multiple lazy components


## React CSS styling

- Inline styling
  - < h1 style={{backgroundColor: "lightblue"}}>Hello Style!< /h1>
  - JavaScript object
- CSS stylesheets
  - import './MyStylesheet.css';
- CSS Modules
  - import styles from './my-style.module.css';
  - The CSS inside a module is available only for the component that imported it, and you do not have to worry about name conflicts.


## React CSS modules

- Composing classes
  - CSS Modules allow you to combine classes using the composes keyword
  - Which means that one class can inherit the styles of another class

- Global Classes
  - When using CSS Modules, the classes in the .module.css file can only be used in the component that imports them.
  - Sometimes you want your classes to be available globally, and use them in other components. You can do this with the :global syntax.
  - Combine Global and Local Classes: You can combine global and local classes in the same CSS Module.

E.g.:
```
:global(.myheader) {
  padding: 10px 20px;
  font-size: 50px;
  color: white;
  background-color: dodgerblue;
}
```


## React CSS-in-JS

CSS-in-JS is a styling technique where you can write CSS directly in your JavaScript code.

This approach allows you to:
- Write CSS using JavaScript
- Create component-scoped styles
- Use dynamic styles based on props
- Avoid CSS class name conflicts

CSS-in-JS is not a part of the React core library, but can be installed using many React build tools, like Vite, Webpack, or Create React App.
```
npm install styled-components
```

E.g.:
```
import styled from 'styled-components';

const MyHeader = styled.h1`
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
`;

function App() {
  return (
    <>
      <MyHeader>Welcome!< /MyHeader>
    </>
  );
}
```

- Props in Styled Components
  - Another powerful feature of CSS-in-JS is the ability to use props to make styles dynamic.

- Extending Style
  - Another way of letting multiple elements have the same styles is to extend existing styled components.
 
- Component-Scoped Styles
  - Just like with CSS Modules, styles created in CSS-in-JS are scoped to the component.

- Global Styles

```
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  h1 {
    color: white;
    background-color: purple;
    font-family: Arial, sans-serif;
  }

  .myparagraph {
    font-family: courier, monospace;
    color: blue;
  }
`;

function App() {
  return (
    <>
      <GlobalStyle />
      <h1>Welcome!</h1>
      <p className="myparagraph">This paragraph is styled with global styles.</p>
    </>
  );
}
```

## React Router

- React Router is a library that provides routing capabilities for React applications.
- Routing means handling navigation between different views.

- React Router is the standard routing library for React applications.
  - Create multiple pages in your single-page application
  - Handle URL parameters and query strings
  - Manage browser history and navigation
  - Create nested routes and layouts
  - Implement protected routes for authentication

Install React Router
```
npm install react-router-dom
```

Your application must be wrapped with the BrowserRouter component to enable routing:
```
function App() {
  return (
    <BrowserRouter>
      {/* Your app content */}
    </BrowserRouter>
  );
}
```


### Basic Routing

React Router uses three main components for basic routing:
- Link: Creates navigation links that update the URL
- Routes: A container for all your route definitions
- Route: Defines a mapping between a URL path and a component

```
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function Home() {
  return <h1>Home Page< /h1>;
}

function About() {
  return <h1>About Page< /h1>;
}

function Contact() {
  return <h1>Contact Page< /h1>;
}

function App() {
  return (
    <BrowserRouter>
      {/* Navigation */}
      <nav>
        <Link to="/">Home</Link> |{" "}
        <Link to="/about">About</Link> |{" "}
        <Link to="/contact">Contact</Link>
      </nav>

      {/* Routes */}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}
```

- Nested Routes
  - You can have a Route inside another Route, this is called nested routes.
  - Nested routes allow you change parts of the page when you navigate to a new URL, while other parts is not changed or reloaded, almost like having a page within a page.


### Style Active Links

There is a special version of the Link component called NavLink that knows whether the link's URL is "active" or not.

The NavLink is especially useful for:
- Navigation menus
- Breadcrumbs
- Tabs


### URL Parameters

React Router provides the useParams hook to access these parameters in your components.

```
import { BrowserRouter, Routes, Route, Link, useParams } from 'react-router-dom';

function Info() {
  const { firstname } = useParams();
  return < h1>Hello, {firstname}!< /h1>;
}

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/customer/Emil">Emil</Link> | 
        <Link to="/customer/Tobias">Tobias</Link> |
        <Link to="/customer/Linus">Linus</Link>
      </nav>

      <Routes>
        <Route path="/customer/:firstname" element={<Info />} />
      </Routes>
    </BrowserRouter>
  );
}
```


## React Transitions

### What is useTransition?

- The useTransition hook helps you keep your React app responsive during heavy updates.
- It lets you mark some state updates as "non-urgent", allowing other, more urgent updates to happen first.

### When to Use Transitions?

Use transitions when you have:
- A slow operation that might freeze the UI
- Updates that aren't immediately critical
- Search results that take time to display

```
import { useState, useTransition } from 'react';

function SearchBar() {
  const [text, setText] = useState('');
  const [results, setResults] = useState('');
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    // Urgent: Update input right away
    setText(e.target.value);

    // Non-urgent: Update search results
    startTransition(() => {
      setResults(e.target.value);
    });
  };

  return (
    <div>
      <input value={text} onChange={handleChange} />
      {isPending ? (
        <p>Loading...</p>
      ) : (
        <p>Search results for: {results}</p>
      )}
    </div>
  );
}
```

### useTransition Hook

The useTransition hook returns two items:
- isPending: tells you if a transition is active
- startTransition: function to mark updates as transitions

## React Forward Ref

### What is forwardRef?

forwardRef lets your component pass a reference to one of its children. It's like giving a direct reference to a DOM element inside your component.

Common uses for forwardRef:
- Focusing input elements
- Triggering animations
- Measuring DOM elements
- Integrating with third-party libraries

```
import { forwardRef, useRef } from 'react';

const MyInput = forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));

function App() {
  const inputRef = useRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <MyInput ref={inputRef} placeholder="Type here..." />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```


## React HOC (High Order Components)

### What is a Higher Order Component?

A Higher Order Component (HOC) is like a wrapper that adds extra features to your React components. Think of it like putting a case on your phone - the case adds new features (like water protection) without changing the phone itself.

Note: HOCs are functions that take a component and return an enhanced version of that component.

Note: Often, HOC's can be replaced with React Hooks, but HOC's are still useful for certain cross-cutting concerns like authentication or data fetching patterns.

```
// This is our HOC - it adds a border to any component
function withBorder(WrappedComponent) {
  return function NewComponent(props) {
    return (
      <div style={{ border: '2px solid blue', padding: '10px' }}>
        <WrappedComponent {...props} />
      </div>
    );
  };
}

// Simple component without border
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Create a new component with border
const GreetingWithBorder = withBorder(Greeting);

function App() {
  return (
    <div>
      <Greeting name="John" />
      <GreetingWithBorder name="Jane" />
    </div>
  );
}
```


## React Sass (SASS styling)

### What is Sass?
- Sass is a CSS pre-processor.
- Sass files are executed on the server and sends CSS to the browser.
- Sass adds extra features to CSS like variables, nesting, mixins, and more.

[Sass Tutorial(https://www.w3schools.com/sass/default.asp)

Adding Sass to React:
```
npm install sass
```

Create a Sass file MyStyle.scss:
```
$myColor: red;

h1 {
  color: $myColor;
}
```

Import the Sass file
```
import { createRoot } from 'react-dom/client';
import './MyStyle.scss';

function MyHeader() {
  return (
    <h1>My Header</h1>
  );
}

createRoot(document.getElementById('root')).render(
  <MyHeader />
);
```

Sass Modules
- Sass has many Built-in Modules that you can use to manipulate colors, math, strings, etc.
- One example is the sass:color module.


# React Hooks

- Hooks allow functions to have access to state and other React features without using classes.
- They provide a more direct API to React concepts like props, state, context, refs, and lifecycle.

### What is a Hook?

Hooks are functions that let you "hook into" React state and lifecycle features from functional components.

### Hook Rules

There are 3 rules for hooks:
- Hooks can only be called inside React function components.
- Hooks can only be called at the top level of a component.
- Hooks cannot be conditional

## React useState Hook

- The React useState Hook allows us to track state in a function component.
- State generally refers to data or properties that need to be tracking in an application.

## React useEffect Hooks

- The useEffect Hook allows you to perform side effects in your components.
- Some examples of side effects are: fetching data, directly updating the DOM, and timers.
- useEffect accepts two arguments. The second argument is optional.
  - useEffect(<function>, <dependency>)

### Effect Cleanup

Some effects require cleanup to reduce memory leaks.

Timeouts, subscriptions, event listeners, and other effects that are no longer needed should be disposed.

We do this by including a return function at the end of the useEffect Hook.


## React useContext Hook

React Context is a way to manage state globally.

It can be used together with the useState Hook to share state between deeply nested components more easily than with useState alone.

### Create Context

To create context, you must Import createContext and initialize it:

### Context Provider

Wrap child components in the Context Provider and supply the state value.


## React useRef Hook

The useRef Hook allows you to persist values between renders.
- It can be used to store a mutable value that does not cause a re-render when updated.
- It can be used to access a DOM element directly.

### Does Not Cause Re-renders

If we tried to count how many times our application renders using the useState Hook, we would be caught in an infinite loop since this Hook itself causes a re-render.

To avoid this, we can use the useRef Hook.

### Accessing DOM Elements

The useRef Hook is often used to access DOM elements directly.
- First, we create a ref using the useRef Hook: const inputElement = useRef();.
- Then, we attach the ref to a DOM element using the ref attribute in JSX: <input type="text" ref={inputElement} />.
- Finally, we can access the DOM element using the current property: inputElement.current.

### Tracking State Changes

The useRef Hook can also be used to keep track of previous state values.

This is because we are able to persist useRef values between renders.


## React useReducer Hook

The useReducer Hook is similar to the useState Hook.

It allows for custom state logic.

If you find yourself keeping track of multiple pieces of state that rely on complex logic, useReducer may be useful.

### Syntax

The useReducer Hook accepts three arguments.
```
useReducer(reducer, initialState, init)
```

## React useCallback Hook

The useCallback Hook is used to memoize a callback function.

Memoizing a function means caching the result of a function so that it does not need to be recalculated.

The useCallback function only re-executes when one of its dependencies changes value.

This allows us to isolate resource intensive functions so that they will not automatically run on every render.

### Syntax
```
useCallback(callback, dependencies)
```

The useCallback and useMemo Hooks are similar:

useMemo returns a memoized value.

useCallback returns a memoized function.


## React useMemo Hook

The React useMemo Hook returns a memoized value.

The useMemo Hook only runs when one of its dependencies update.

This can improve performance.

The useMemo Hook can be used to keep expensive, resource intensive functions from needlessly running.


## React Custom Hooks

You can make your own Hooks!

When you have components that can be used by multiple components, we can extract that component into a custom Hook.

Custom Hooks start with "use". Example: useFetch.

### Build a Hook


# React Quiz questions

Question 1:

What is React?
React is a JavaScript library for building user interfaces.    Your answer  
React is a database engine.
React is a programming language.

Question 2:

What does my-react-app refer to in the following command?
npm create vite@latest my-react-app -- --template react

The name you want to use for the new app    Your answer  
The type of app to create
A reference to an existing app

Question 3:

What command is used to start the React local development server?
npm run dev    Your answer  
npm build
npm serve
npm start

Question 4:

What is the default local host port that Vite uses for a React development server?
5173    Your answer  
5000
3000
8080

Question 5:

To develop and run React code, Node.js is required.
True    Your answer  
False

Question 6:

What type of element will be rendered from the following code?
function Car() {
  return <h1>Ford Mustang</h1>;
}

createRoot(document.getElementById('root')).render(
  <Car />
)

h1    Your answer  
Component
div
ReactDom

Question 7:

What is the children prop?
A property that lets you pass data to child components    Your answer  
A property that adds child values to state
A property that lets you nest components in other components    Correct answer  
A property that lets you set an object as a property

Question 8:

Which keyword creates a constant in JavaScript?
const    Your answer  
let
var
constant

Question 9:

A copy of the 'real' DOM that is kept in memory is called what?
Virtual DOM    Your answer  
DOM
React DOM
Shadow DOM

Question 10:

React component names must begin with an uppercase letter.
True    Your answer  
False

Question 11:

Which operator can be used to conditionally render a React component?
&&    Your answer  
::
||
??

Question 12:

When rendering a list using the JavaScript map() method, what is required for each element rendered?
key    Your answer  
id
index
data

Question 13:

What does JSX stand for?
JavaScript XML    Your answer  
JavaScript X-factor
JavaScript Extreme
JavaScript Expressions

Question 14:

How can you optimize performance for a function component that always renders the same way?
Use the useMemo Hook.    Your answer  
Use the useReducer Hook.
Use the shouldComponentUpdate lifecycle method.
Wrap it in the React.memo higher-order component.    Correct answer 

Question 15:

What props will be available to the following component?
<Car {...props} />

all of them    Your answer  
children
only updated ones
only static ones

Question 16:

What is a common use case for ref?
To directly access a DOM node    Your answer  
To refer to another JavaScript file
To bind the function
To refer to a function

Question 17:

How can you combine the following arrays using the spread operator?
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];

const combined = [...array1, ...array2];    Your answer  
const combined = [array1, array2];
const combined = array1 + array2;
const combined = ...array1 + ...array2;

Question 18:

React can only render elements in the root document element.
False    Your answer  
True

Question 19:

What is the correct syntax to export a component named Car from a file?
export default Car;    Your answer  
export Car as Component;
export internal Car;
export Component.Car;

Question 20:

Find the bug in this code:
function car({make, model}) {
  return <h1>{make} {model}</h1>;
};

The first letter of the function must be capitalized    Your answer  
Remove the return statement
Wrap the return in a fragment
Add parenthesis around the return value

Question 21:

React separates the user interface into components. How are components combinded to create a user interface?
By nesting components    Your answer  
By putting them in a folder structure
With code splitting
With webpack

Question 22:

Although React Hooks generally replace class components, there are no plans to remove classes from React.
True    Your answer  
False

Question 23:

Which of the following is NOT a rule for React Hooks?
Hooks can be called in Class or Function components    Your answer  
Hooks can only be called at the top level of a component
Hooks can only be called inside React Function components
Hooks cannot be conditional

Question 24:

What is the output of the following code?
const make = 'Ford';
const model = 'Mustang';
const car = { make, model };
console.log(car);

{{make: 'Ford', model: 'Mustang'}}    Your answer  
{car: 'Ford', car: 'Mustang'}}
{make: 'Ford', model: 'Mustang'}    Correct answer  
{car: {make: 'Ford', model: 'Mustang'}}

Question 25:

Why should you avoid copying the values of props into a component's state?
Because that would create two instances of the same state that could become out of sync    Your answer  
Because you want to allow data to flow back up to the parent
Because you should never mutate state
Because prop values cannot be stored in state



