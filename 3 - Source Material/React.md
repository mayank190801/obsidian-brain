
- A Javascript library used to create web application 
- It is not a full blown framework and is only just a library 


The useState() is a built-in React Hook that allows you for having state variables in functional components. It should be used when the DOM has something that is dynamically manipulating/controlling.

#### HOOKS
React Hooks will allow you to use the state and other features of React in which requires a class to be written by you. In simple words, we can say that, React Hooks are the functions that will connect React state with the lifecycle features from the function components.

**React Hooks** are functions that allow you to use React features like state and lifecycle methods inside functional components.


- Keys help react identify which elements were added, changed or removed.
- Keys should be given to array elements for providing a unique identity for each element.
- Without keys, React does not understand the order or uniqueness of each element.
- With keys, React has an idea of which particular element was deleted, edited, and added.
- Keys are generally used for displaying a list of data coming from an API.

JSX stands for JavaScript XML. It allows us to write HTML inside JavaScript and place them in the DOM without using functions like appendChild( ) or createElement( ).
(Syntatic Sugar I would say)


```
import React, { useState, useEffect } from 'react';

function MyComponent() {
  // useState to manage the count state
  const [count, setCount] = useState(0);

  // useEffect to handle componentDidMount and componentDidUpdate logic
  useEffect(() => {
    console.log('Component mounted or updated!');

    // Cleanup function to mimic componentWillUnmount
    return () => {
      console.log('Component is about to be unmounted!');
    };
  }, [count]); // The effect will run when the 'count' state changes

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

export default MyComponent;
```

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log('Component mounted!');
  }

  componentDidUpdate(prevProps, prevState) {
    if (this.state.count !== prevState.count) {
      console.log('Component updated!');
    }
  }

  componentWillUnmount() {
    console.log('Component is about to be unmounted!');
  }

  render() {
    return (
      <div>
        <p>{this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```


#### React Hooks ~ Important ones (understand in depth all the nuances about each)

**1. useState – State Management**

• Manages state in functional components.
```
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // count is the state, setCount updates it

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**2. useEffect – Side Effects (Data fetching, subscriptions, etc.)**

• Runs side effects after render. Can replace componentDidMount, componentDidUpdate, and componentWillUnmount.
```
import React, { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => response.json())
      .then(json => setData(json));

    // Cleanup, runs on unmount
    return () => {
      console.log('Cleanup when component unmounts');
    };
  }, []); // Empty array means it runs only on mount

  return (
    <div>
      {data ? <p>{data.title}</p> : <p>Loading...</p>}
    </div>
  );
}
```

**3. useContext – Context API**

The Context API allows you to share data globally across a component tree without needing to pass props down manually at every level.

```
import React, { createContext, useState } from 'react';

// Creating a context for the theme
const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}  {/* The component tree */}
    </ThemeContext.Provider>
  );
}

export { ThemeContext, ThemeProvider };
```

``` 
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeProvider'; // Import the context

function ThemedComponent() {
  const { theme, toggleTheme } = useContext(ThemeContext);  // Access context value

  return (
    <div style={{ background: theme === 'dark' ? '#333' : '#FFF', color: theme === 'dark' ? '#FFF' : '#000' }}>
      <p>The current theme is {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
}
```

```
import React from 'react';
import ThemeProvider from './ThemeProvider';
import ThemedComponent from './ThemedComponent';

function App() {
  return (
    <ThemeProvider>
      <ThemedComponent />
    </ThemeProvider>
  );
}

export default App;
```


**4. useReducer – More Complex State Management (like Redux)**

• Provides a way to manage complex state, similar to Redux’s reducer pattern.

```
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function CounterWithReducer() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

**5. useRef – References and DOM Manipulation**

• Allows you to create a reference to a DOM element or a value that persists across renders.

```
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null); // Creates a ref

  const handleFocus = () => {
    inputRef.current.focus(); // Focuses on the input element
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

**6. useMemo – Memoization (Performance Optimization)**

• Memoizes expensive calculations to prevent recalculation on every render unless dependencies change.

```
import React, { useState, useMemo } from 'react';

function ExpensiveComponent({ num }) {
  const calculate = useMemo(() => {
    console.log('Expensive calculation');
    return num * 2;
  }, [num]); // Recomputes only when 'num' changes

  return <div>Result: {calculate}</div>;
}
```

**7. useCallback – Memoization for Functions**

• Memoizes functions to avoid unnecessary re-creations between renders.
• The useCallback hook is used to **memoize functions** in React to prevent unnecessary re-creation of functions during re-renders. This can help optimize performance, especially in cases where functions are passed as props to child components, and the child components depend on the stability of the function reference to prevent unnecessary re-renders.

```
import React, { useState, useCallback } from 'react';
import Child from './Child';

function Parent() {
  const [count, setCount] = useState(0);

  // Memoize the increment function to avoid unnecessary re-creations
  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]); // The function will only change when 'count' changes

  console.log('Parent rendered');

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <Child onClick={increment} />
    </div>
  );
}

export default Parent;
```


### Higher Order Components 
- What? When? Why? and How? 

### Life Cycle Methods of Components (fundamentals)
- For class components 
- Mounting, Updating, Unmounting phase 
- componentMount, componentDidMount etc. etc. ... 

### State Management (All about data)
- State/ Props
- Props Drilling 
- React context (highlight of the interview brother)

### Redux / Zustand 
- know about basics and how they work is good enough 
- Why and when
- Do our application even needs it? 
- Redux Toolkit (amazing)

### Custom Hooks 
- When, and write code for this 
- Example - useLocalStorage 

### Lazy Loading 
- code splitting
- code chunking 
- suspense 
- Highly asked 

### Virtual DOM 
- in depth is important 
- Reoncilliation algorithms 
- React Fiber 
- Differ Algorithm 

The **Virtual DOM** was introduced to **optimize DOM updates**. It provides a way to update the UI in an efficient, predictable, and performant manner. Instead of updating the real DOM every time something changes in the application, React (and other frameworks using a Virtual DOM) performs the following steps:

1. **Create a Virtual DOM**: A lightweight, in-memory representation of the actual DOM. It’s essentially a JavaScript object that mirrors the structure of the real DOM.

2. **Update the Virtual DOM first**: When something changes in the UI, instead of updating the real DOM immediately, React updates the Virtual DOM. These updates are very fast because they happen in memory and do not involve the browser’s rendering engine.

3. **Diffing Algorithm**: React then performs a comparison (called **diffing**) between the previous version of the Virtual DOM and the updated version to figure out exactly what has changed. This process is fast because it compares two plain JavaScript objects, not real DOM nodes.

4. **Efficiently Update the Real DOM**: After determining the minimal set of changes that need to be made, React efficiently updates only those specific parts of the real DOM. This process is known as **reconciliation**. Instead of updating the entire DOM, only the nodes that actually need to change are updated.

**Key Principles of the Diffing Algorithm:**

• **Same node type**: If two elements have the same tag and key (if applicable), React considers them the same node, and updates only the necessary attributes.

• **Different node type**: If the nodes have different tags, React will replace the entire subtree rooted at that node, because it assumes that the entire structure has changed.

• **Children diffing**: For child elements, React uses a heuristic approach to compare child nodes and identify which elements can be reused and which need to be added or removed. React uses **keys** (unique identifiers for elements in lists) to optimize the process of matching and reordering child elements.

### SSR vs CSR 
- Hot interview question!!! 
- NextJS hype is there - SSR 
- SEO about react application && performance 

In **React Server-Side Rendering (SSR)**, the React application is rendered on the server. When a user requests a page, the server sends a fully rendered HTML document to the client. Once the HTML is received, it is displayed immediately, and React “hydrates” the static HTML on the client-side to make it interactive.

1. **Initial Request**: A user requests a page.
2. **Server Render**: The server runs the React code and generates the HTML content.
3. **HTML Sent to Client**: The server sends the fully rendered HTML to the client, allowing the page to display quickly.
4. **Hydration**: After the HTML is rendered, React attaches event listeners and other interactive elements to make the page fully interactive.

In **React Client-Side Rendering (CSR)**, the initial HTML document sent from the server is minimal and often empty, except for a <div id="root"></div>. After receiving the HTML, the browser downloads the JavaScript bundle, which is responsible for rendering the React components on the client-side.

**How React CSR Works:**

1. **Initial Request**: The server sends a basic HTML file with a root element 
2. **JavaScript Execution**: The browser downloads and executes the JavaScript bundle.
3. **React Render**: React components are rendered on the client, and the app becomes interactive.

### Routing  (Roles Based Access Control)
- react-router 
- Protected Routes 
- Dynamic Routing 

### Testing 
- React Testing library  
- Hack for interview and flaunt your knowledge 
- Unit Testing 

### Async Tasks 
- API calls 
- Events 
- Promises ( free videos ) - Akshay Saini 

### Reusability, Modularity, Testing (important concepts)

Styling Accessibility 

~ simple as that 

