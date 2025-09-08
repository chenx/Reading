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
    < >
      < MyHeader>Welcome!< /MyHeader>
    < />
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
    < >
      < GlobalStyle />
      < h1>Welcome!</h1>
      < p className="myparagraph">This paragraph is styled with global styles.</p>
    < />
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
    < BrowserRouter>
      {/* Your app content */}
    < /BrowserRouter>
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
  return < h1>Home Page< /h1>;
}

function About() {
  return < h1>About Page< /h1>;
}

function Contact() {
  return < h1>Contact Page< /h1>;
}

function App() {
  return (
    < BrowserRouter>
      {/* Navigation */}
      < nav>
        < Link to="/">Home</Link> |{" "}
        < Link to="/about">About</Link> |{" "}
        < Link to="/contact">Contact</Link>
      < /nav>

      {/* Routes */}
      < Routes>
        < Route path="/" element={<Home />} />
        < Route path="/about" element={<About />} />
        < Route path="/contact" element={<Contact />} />
      < /Routes>
    < /BrowserRouter>
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

