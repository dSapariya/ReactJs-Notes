# React Hooks Overview

## Introduction

React Hooks were introduced in version 16.8, providing powerful features that allow function components to manage state and utilize other React functionalities without needing to convert to class components.

## What is a Hook?

Hooks are functions that let you "hook" into React features like state and lifecycle methods directly from function components.

## Hook Rules

There are three fundamental rules for using Hooks in React:

1. **Only Call Hooks Inside React Functions**: Hooks should be called only within React function components or other custom Hooks.
2. **Call Hooks at the Top Level**: Always use Hooks at the top level of your function component. They should not be called inside loops, conditions, or nested functions.
3. **Do Not Call Hooks Conditionally**: Hooks should be used unconditionally to ensure that the state and side effects are applied consistently across renders.

# useState Hook

The `useState` Hook is a built-in React Hook that allows you to manage state in function components.

### What is State?

State generally refers to data or properties that need to be tracked in an application. It can change over time, and React will re-render the component whenever the state is updated.

### How to Use useState

To use `useState`, first import it from React:

```javascript
import { useState } from "react";
```

### Initialize useState

You initialize state by calling `useState` within your function component. `useState` accepts an initial state and returns two values:

1. The current state.
2. A function that allows you to update the state.

### Example

Here's an example of how to use `useState`:

```javascript
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("");
}
```

In this example, `color` is the current state, and `setColor` is the function used to update the state. The initial state is set to an empty string.

# `useEffect` Hook 

## Introduction

The `useEffect` Hook is a powerful feature in React that allows you to perform side effects in your function components. Side effects can include tasks such as fetching data, directly manipulating the DOM, or setting up timers.

## What is a Side Effect?

Side effects are operations that affect something outside the scope of the function being executed. In the context of React, common side effects include:

- **Fetching data** from an API
- **Updating the DOM** directly (e.g., manipulating an element's style or attributes)
- **Setting up timers** or intervals

## How to Use `useEffect`

The `useEffect` Hook takes two arguments:

```javascript
useEffect(<function>, <dependency>)
```

- **First Argument**: A function that contains the side effect logic.
- **Second Argument (Optional)**: An array of dependencies that determines when the effect should run.

### Basic Example

Here’s an example of using `useEffect` to update a counter every second:

```javascript
useEffect(() => {
  setTimeout(() => {
    setCount((count) => count + 1);
  }, 1000);
}, []);
```

In this example, the effect runs once after the initial render because the dependency array is empty (`[]`).

## Effect Cleanup

Some effects require cleanup to avoid issues such as memory leaks. Common examples include:

- **Timeouts**
- **Subscriptions**
- **Event listeners**

To perform cleanup, return a function from within the `useEffect` Hook. This function will be executed when the component unmounts or before the effect runs again.

### Cleanup Example

Here’s an example of using `useEffect` with cleanup:

```javascript
useEffect(() => {
  let timer = setTimeout(() => {
    setCount((count) => count + 1);
  }, 1000);

  return () => clearTimeout(timer);
}, []);
```

In this example, the cleanup function clears the timeout to ensure that it doesn’t continue running unnecessarily.

# useContext` Hook

## Introduction

The `useContext` Hook is a powerful feature in React that allows components to access and share state more efficiently across deeply nested component trees without the need for prop drilling. It works in conjunction with React Context, which provides a way to manage state globally across your application.

## React Context

React Context is a mechanism for managing state at a global level. It enables you to share state between components without having to pass props manually through each level of the component hierarchy.

### The Problem with Prop Drilling

When multiple nested components need access to the same state, you might traditionally pass the state as "props" through each component in the hierarchy. This technique, known as "prop drilling," can become cumbersome and difficult to maintain, especially in large applications with deep component trees.

### Solution: React Context

React Context solves the problem of prop drilling by allowing you to create a context and provide it to any component in the tree, regardless of how deeply nested it is.

## How to Use React Context

### 1. Create Context

To create a context, you use the `createContext` function provided by React:

```javascript
import { useState, createContext } from "react";
import ReactDOM from "react-dom/client";

const UserContext = createContext();
```

### 2. Context Provider

Wrap the components that need access to the state with a Context Provider. The Provider component accepts a `value` prop that contains the state you want to share.

```javascript
function Component1() {
  const [user, setUser] = useState("Jesse Hall");

  return (
    <UserContext.Provider value={user}>
      <h1>{`Hello ${user}!`}</h1>
      <Component2 user={user} />
    </UserContext.Provider>
  );
}
```

In this example, `Component1` provides the `user` state to all of its child components, making the state available without needing to pass it explicitly as props.

### 3. Use the `useContext` Hook

To access the context in a child component, use the `useContext` Hook. This allows you to consume the context value directly.

```javascript
import { useState, createContext, useContext } from "react";

function Component5() {
  const user = useContext(UserContext);

  return (
    <>
      <h1>Component 5</h1>
      <h2>{`Hello ${user} again!`}</h2>
    </>
  );
}
```
# `useRef` Hook 

## Introduction

The `useRef` Hook is a powerful tool in React that allows you to persist values between renders without causing a re-render. It's especially useful for storing mutable values that need to survive across renders and for directly accessing DOM elements.

## Key Features of `useRef`

### 1. Persisting Values Between Renders

The primary purpose of `useRef` is to persist values across renders of a component. Unlike state, updating a `useRef` value does not trigger a re-render of the component.

### 2. Storing Mutable Values

`useRef` is ideal for storing mutable values that don't need to cause a re-render when updated. For example, it can store a counter, a timeout ID, or any other value that may change but doesn't require re-rendering the component.

### 3. Accessing DOM Elements Directly

`useRef` can be used to directly interact with DOM elements. By assigning a `ref` to a DOM element, you can access and manipulate that element's properties directly, such as focusing an input field or changing its value.

## How to Use `useRef`

### Basic Usage

The `useRef` Hook returns an object with a single property, `current`. You can initialize `useRef` like this:

```javascript
const refContainer = useRef(initialValue);
```

- `refContainer.current` will store the initial value, which can be updated without causing a re-render.

### Example: Persisting a Value

Here’s an example where `useRef` is used to persist a value across renders:

```javascript
import React, { useRef, useEffect } from "react";

function RenderCounter() {
  const renderCount = useRef(0);

  useEffect(() => {
    renderCount.current += 1;
  });

  return <h1>Render Count: {renderCount.current}</h1>;
}

export default RenderCounter;
```

In this example, `renderCount.current` increments on every render, but the component itself doesn't re-render due to `useRef` updates.

### Example: Accessing a DOM Element

Here’s an example where `useRef` is used to access a DOM element directly:

```javascript
import React, { useRef } from "react";

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // Access the input element and focus it
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}

export default TextInputWithFocusButton;
```

In this example, clicking the button focuses the input field, demonstrating how `useRef` can be used to interact with the DOM directly.

# `useReducer` Hook

## Introduction

The `useReducer` Hook is a powerful alternative to the `useState` Hook in React, particularly when managing complex state logic. It provides a more structured approach to handling state updates, especially when multiple pieces of state need to be managed together.

## Why Use `useReducer`?

While `useState` is suitable for simple state management, `useReducer` shines in scenarios where state updates involve complex logic or when multiple related states need to be managed cohesively. If you find yourself writing complex `setState` logic or needing to manage state transitions based on various actions, `useReducer` can help organize and simplify your code.

## How `useReducer` Works

### Syntax

```javascript
useReducer(reducer, initialState)
```

- **`reducer`**: A function that defines the logic for updating the state. It receives two arguments: the current state and an action, and it returns the new state.
- **`initialState`**: The initial state value, which can be a simple value or, more commonly, an object containing multiple state variables.

### Return Value

The `useReducer` Hook returns two values:

1. **`state`**: The current state, reflecting the most recent update based on the dispatched action.
2. **`dispatch`**: A function used to send actions to the reducer, triggering state updates.

### Example Usage

#### 1. Defining the Reducer Function

The reducer function encapsulates the logic for updating the state based on different actions. Here's an example:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}
```

#### 2. Using `useReducer` in a Component

You can use `useReducer` in a component to manage the state:

```javascript
import React, { useReducer } from "react";

function Counter() {
  const initialState = { count: 0 };

  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}

export default Counter;
```

In this example, the `Counter` component uses `useReducer` to manage a `count` state. The `dispatch` function is used to trigger actions that the reducer handles to update the state.

## Benefits of Using `useReducer`

- **Organized State Logic**: `useReducer` centralizes state update logic, making it easier to manage complex state transitions.
- **Scalability**: It’s well-suited for components that have multiple, interdependent state variables or where the state update logic is complex.
- **Predictability**: The reducer function’s structure promotes predictable state updates, making debugging and testing easier.

# `useCallback` Hook

## Introduction

The `useCallback` Hook in React is a powerful tool that allows you to return a memoized version of a callback function. Memoization is a technique used to cache a function or value so that it does not need to be recalculated on every render. This can significantly improve the performance of your application, especially when dealing with resource-intensive functions or preventing unnecessary re-renders.

## Why Use `useCallback`?

### 1. Preventing Unnecessary Re-Renders

One common use case for `useCallback` is to prevent a component from re-rendering unless its dependencies have changed. Without `useCallback`, a function inside a component is recreated every time the component re-renders, which can cause child components that depend on that function to re-render unnecessarily.

### 2. Solving Referential Equality Issues

Every time a component re-renders, its functions are recreated. This can cause issues with referential equality, where two function references are considered different even if their logic is identical. This can lead to unwanted re-renders in components that rely on those functions.

## How `useCallback` Works

### Syntax

```javascript
const memoizedCallback = useCallback(() => {
  // Your callback logic here
}, [dependencies]);
```

- **`callback`**: The function you want to memoize.
- **`dependencies`**: An array of dependencies that the callback depends on. The callback will only be recalculated if one of these dependencies changes.

### Example Problem: Unnecessary Re-Renders

Consider the following example where a `Todos` component re-renders even when its state hasn't changed:

```javascript
import React, { useState, memo } from "react";

const Todos = memo(({ todos, addTodo }) => {
  console.log("Todos component re-rendered");
  return (
    <div>
      <h2>My Todos</h2>
      {todos.map((todo, index) => (
        <p key={index}>{todo}</p>
      ))}
      <button onClick={addTodo}>Add Todo</button>
    </div>
  );
});

function App() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["Todo 1", "Todo 2"]);

  const addTodo = () => {
    setTodos([...todos, `Todo ${todos.length + 1}`]);
  };

  return (
    <div>
      <Todos todos={todos} addTodo={addTodo} />
      <hr />
      <div>
        <h2>Count: {count}</h2>
        <button onClick={() => setCount(count + 1)}>Increment Count</button>
      </div>
    </div>
  );
}

export default App;
```

In this example, clicking the "Increment Count" button causes the `Todos` component to re-render, even though its state (`todos`) hasn't changed. This happens because the `addTodo` function is recreated on every render, leading to a change in its reference, which causes `Todos` to re-render.

### Solution: Using `useCallback`

To prevent the `Todos` component from re-rendering needlessly, we can use the `useCallback` Hook:

```javascript
import React, { useState, useCallback, memo } from "react";

const Todos = memo(({ todos, addTodo }) => {
  console.log("Todos component re-rendered");
  return (
    <div>
      <h2>My Todos</h2>
      {todos.map((todo, index) => (
        <p key={index}>{todo}</p>
      ))}
      <button onClick={addTodo}>Add Todo</button>
    </div>
  );
});

function App() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["Todo 1", "Todo 2"]);

  const addTodo = useCallback(() => {
    setTodos([...todos, `Todo ${todos.length + 1}`]);
  }, [todos]);

  return (
    <div>
      <Todos todos={todos} addTodo={addTodo} />
      <hr />
      <div>
        <h2>Count: {count}</h2>
        <button onClick={() => setCount(count + 1)}>Increment Count</button>
      </div>
    </div>
  );
}

export default App;
```

In this updated example, the `addTodo` function is now wrapped in `useCallback`, meaning it will only be recreated if one of its dependencies (`todos`) changes. As a result, clicking the "Increment Count" button no longer triggers a re-render of the `Todos` component, because the `addTodo` function reference remains the same.

## Conclusion

The `useCallback` Hook is an essential tool for optimizing React applications by preventing unnecessary re-renders and solving issues related to referential equality. By using `useCallback`, you can ensure that functions are only recreated when necessary, leading to more efficient and performant components.

